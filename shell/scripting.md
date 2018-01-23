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

## Get function name

```
${FUNCNAME[0]}
```

## Set a default value

```shell
SOME=$1
DEFAULT_VALUE_FOR_SOME="some"
: ${SOME:=${DEFAULT_VALUE_FOR_SOME}}
# Assings DEFAULT_VALUE_FOR_SOME to SOME if SOME is empty
```

## Get a path to script itself

```shell
#!/bin/bash

echo "First arg $0"
echo "Dirname $(dirname $0)"
echo "Absolute path for the file's parent dir $(dirname $(readlink -f $0))"
echo "Absolute path for the script itself $(readlink -f $0)"
echo "Absolute path for the script itself 2 $(cd "$(dirname $0)"; pwd -P)"

```
