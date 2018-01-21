# Scripting

## Set -eu

```
set -eu
```

## Ignore error

```
cat hoo || true
```

## Or condition

```
if [[ "a" == "a" || "b" == "b" ]]; then
  echo "foo"
else
  echo "bar
fi
```

## And condition

```
if [[ $(some execution 2> /dev/null) && $(others execution) ]]; then
  echo "foo"
else
  echo "bar"
fi
```

## Exist user

```
id -u <username>
# => 1001 if user exists
```

## Exist command

```
command -v <commandname>
```

## Remove function/variable

```
unset -f <function_name>
unset <variable_name>
```

## Check input arguments

```
# Expect arg1 exist
if [ -z $1 ]; then return 1; fi

# Expect 4 args
if [ $# -ne 4]; then return 1; fi
```
