# Ruby

## Show call stack

[Refs](https://ruby-doc.org/core-2.4.2/Kernel.html#method-i-caller)

```
# Kernel#caller

caller
caller(10..30)
```

## Run system command and get output

```
target_files = [ ... ]
res, err, status = Open3.capture3(
  "RAILS_ENV=test bundle exec rubocop --cache false --config .rubocop.yml --fail-level W #{target_files}"
)

res # -> stdout
err # -> stderr
status # -> status object

# You can access exit code
status.exitstatus
```

