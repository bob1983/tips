# Resque
WorkerAPI -> [API](https://github.com/resque/resque/blob/master/lib/resque/worker.rb)

## Unregister worker
[Ref](https://stackoverflow.com/questions/7416318/how-do-i-clear-stuck-stale-resque-workers)

```ruby
# Select workers to unregister
workers = Resque.workers.select { |worker|
  worker.to_s =~ /ip-10-0-161-47/
}
workers.each { |w| w.unregister_worker }
```
