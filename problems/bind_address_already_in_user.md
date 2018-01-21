# Sockets

## Error

```
bind: Address already in use
```

## Resolve

- Show which process is using the address
  - lsof -i :6379
- kill the pid
