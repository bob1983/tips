# Github api

# References
- [Document](https://developer.github.com/v3/guides/getting-started/)

# Make a test request
## Send a request without authentification

```
# -i includes Header
curl -i https://api.github.com/users/bob1983```
```

## OAuth
Create your token

```
# issues
curl -i -H 'Authorization: token <your token>' \
  https://api.github.com/bob1983/repos/dotfiles/issues
```

## Paginate

```
curl -i -H 'Authorization: token <your token>' \
  https://api.github.com/bob1983/repos/dotfiles/issues?page=1&per_page=10
```
