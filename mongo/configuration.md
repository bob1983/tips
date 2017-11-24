# Confirm log level

```
mongo
use admin;
db.runCommand({getParameter: 1, logLevel: 1});
# => { "logLevel": 0, "ok": 1 }

# https://docs.mongodb.com/manual/reference/log-messages/#view-current-log-verbosity-level
db.getLogComponents()
# => {
        "verbosity" : 0,
        "accessControl" : {
...
        }
```

## Note

- -1 means inherit parent setting
