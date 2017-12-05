# Rails tips

## Make SQL log disable on rails console

```
old_logger = ActiveRecord::Base.logger
ActiveRecord::Base.logger = nil

```
