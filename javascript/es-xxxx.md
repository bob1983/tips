# ESxxxx
ESxxxx feature which I've easily forgotten :-(

## Array any?

```
[1, 2, 3].some(d => {
  return d % 2 === 0;
});
# => true
```

## Array every?

```
[1, 2, 3].every(d => {
  return d > 0;
});
# => true
```

## Array distinct ( uniq )

```
const arr = [1, 2, 3, 4, 3, 2, 1];
const uniq = new Set(arr);
const uniqArr = Array.from(uniq);
```

## Object key as variable

```
const myVar = 'foo';
const object = {
  [myVar]: 'bar'
};
# => { foo: 'bar' }

const object2 = {
  [object]: 'baz'
};
# => { [object Object]: 'baz' }
# Seems if key is not string, toString() is called
```
```
