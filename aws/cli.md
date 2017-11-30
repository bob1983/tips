# Cli
# Reference
- [aws cli + jq example](https://gist.github.com/hummus/8592113)

## Frequently used

### Show running instances

```
aws ec2 describe-instances \
  --filter "Name=instance-state-name,Values=running"
```

### Show runnning instances "xxx" tags

```
aws ec2 describe-instances \
  --filter "Name=instance-state-name,Values=running" \
|jq '.Reservations[].Instances[] | { Tags: .Tags[] | select(.Key == "Stages") }'
```

```
aws ec2 describe-instances \
  --filter "Name=instance-state-name,Values=running" \
|jq '.Reservations[].Instances[] | { Tags: .Tags[] | select(.Key == "Roles") | select(.Value == "app"), .PublicDnsName }'
```



```
# instance id only
aws ec2 describe-instances \
  --filter "Name=instance-state-name,Values=running" \
| jq '.Reservations[].Instances[] | select((.Tags[] | select(.Key == "Stages").Value) | match("staging")) | .InstanceId'
```

```
# some tags
aws ec2 describe-instances\
 --filter "Name=instance-state-name,Values=running" \
| jq '.Reservations[].Instances[] | select((.Tags[] | select(.Key == "Roles").Value) | match("crawler")) | { InstanceId, PublicDnsName, LaunchTime }'
```


### Runnning instances filter by stages

```
aws ec2 describe-instances \
  --filter "Name=instance-state-name,Values=running" \
| jq '.Reservations'
```

### Show images

```
# Fetch a latest ami which name matches "app"
aws ec2 describe-images \
  --owners self \
  --filter "Name=state,Values=available" \
| jq -r '[.Images|sort_by(.CreationDate)|reverse|.[]|select(.Name | match("app"))][0]'

```

### Create an AMI

```
# Fetch a latest ami which name matches "app"
instance_id=$(aws ec2 describe-instances \
  --filter "Name=instance-state-name,Values=running" \
| jq -r '.Reservations[].Instances[] | select((.Tags[] | select(.Key == "Stages").Value) |   match("staging")) | .InstanceId')

current="$(date -u "+%Y-%m-%dT%H-%M-%SZ")"

# Create an AMI with name like: "ami_2017-10-10T08:20:30Z"
result=aws ec2 create-image \
  --instance-id ${instance_id} \
  --reboot \
  --name "ami_${current}"

image_id=$(echo ${result} | jq -r '.ImageId')

# Attach Name tag to the AMI created
aws ec2 create-tags \
  --region us-west-2 \
  --resources ${image_id} \
  --tags Key=Name,Value="My AMI Name" \
  --dry-run
```
