# Practice Problems: Easy 2

### Problem 1

```ruby
ages = { "Herman" => 32, "Lily" => 30, "Grandpa" => 402, "Eddie" => 10 }

puts ages.key?("Spot") # false
puts ages.include?("Herman") # true
puts ages.member?("Spot") # false
```

### Problem 2

convert the string in place

```ruby
munsters_description = "The Munsters are creepy in a good way."

puts munsters_description.upcase!
puts munsters_description.downcase!
puts munsters_description.swapcase!
puts munsters_description.capitalize!
```

Use the `!` operator to modify the caller of the method - will mutate the original array

### Problem 3

Merge a hash with another hash

```ruby
ages = { "Herman" => 32, "Lily" => 30, "Grandpa" => 5843, "Eddie" => 10 }

# add a hash to the end of the ages hash
additional_ages = { "Marilyn" => 22, "Spot" => 237 }
ages.merge!(additional_ages)

p ages # modified
p additional_ages # remains unmodified
```

