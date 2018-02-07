# Ruby

## Show call stack

[Refs](https://ruby-doc.org/core-2.4.2/Kernel.html#method-i-caller)

```ruby
# Kernel#caller

caller
caller(10..30)
```

## Run system command and get output

```ruby
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
## Aggregation
### Input data

```ruby
data = [
  { user: "Bob",   "favorite_1": "Apple", "favorite_2": "Orange" },
  { user: "Mike",  "favorite_1": "Apricot", "favorite_2": "Grape" },
  { user: "Jane",  "favorite_1": "Apple", "favorite_2": nil },
]
```

### favorites counts by fruites

```ruby
grouped = data.map { |d|
  [d.dig(:favorite_1), d.dig(:favorite_2)].compact
}.flatten.group_by { |d|
 d
}
# => { "Apple"=>["Apple", "Apple"], "Orange"=>["Orange"], "Apricot"=>["Apricot"], "Grape"=>["Grape"]}
```

```ruby
grouped.map { |k, v|
  [k, v.length]
}

# => [["Apple", 2], ["Orange", 1], ["Apricot", 1], ["Grape", 1]]
```

```ruby
grouped.map { |k, v|
  [k, v.length]
}.to_h

# => {"Apple"=>2, "Orange"=>1, "Apricot"=>1, "Grape"=>1}
```

