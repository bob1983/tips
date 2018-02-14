# Rails tips

## Make SQL log disable on rails console

```ruby
old_logger = ActiveRecord::Base.logger
ActiveRecord::Base.logger = nil
```

## Use direnv to avoid type "bundle exec"

Add the following to your .envrc

```shell
# Assume exectable is in Rails.root/bin
export PATH=$(pwd)/bin:$PATH
```

Make sure you need to binstub.

```shell
bundle install --path <path to gem file install> --binstubs bin
```
## Output time with formatted string

```ruby
time = Time.now.utc # => 2018-02-14 08:03:09 UTC

# iso8601 formatted time
time.iso8601 # => "2018-02-14T08:04:23Z"
# You could pass a precision as an argument
time.iso8601(3) # => "2018-02-14T08:22:08.109Z"

Time.now.utc.strftime('%Y-%m-%d %H:%M:%S')   # => "2018-02-14 08:06:10"
Time.now.utc.strftime('%Y-%m-%d %H:%M:%S%z') # => "2018-02-14 08:06:15+0000"
Time.now.utc.strftime('%Y-%m-%d %H:%M:%S%Z') # => "2018-02-14 08:06:18UTC"
```
