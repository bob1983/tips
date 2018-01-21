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

