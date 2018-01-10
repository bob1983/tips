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
