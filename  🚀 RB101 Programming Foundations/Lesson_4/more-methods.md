# More Methods

### `Enumerable#any`

```ruby
[1, 2, 3].any? do |num|
	num > 2
end 
# => true

{ a: "ant", b: "bear", c: "cat" }.any? do |key, value|
  value.size > 4
end
# => false
```

- `any?` looks at the truthiness of the **block’s return value** in order to determine the **method’s** return value
    - if block returns *truthy* for any element in the collection, the method will return `true`

### `Enumerable#all?`

Looks at the truthiness of the block’s return value, but the method only returns `true` if the block’s return value in **every** iteration is truthy

```ruby
[1, 2, 3].all? do |num|
	num > 2
end
# => false

{ a: "ant", b: "bear", c: "cat" }.all? do |key, value|
  value.length >= 3
end
# => true
```

### `Enumerable#each_with_index`

`each_with_index` is similar to `each` takes a block as an argument, executes the code within the block upon each iteration, the block’s return value is ignored. But this method also takes a second argument which represents the index of the element

```ruby
[1, 2, 3].each_with_index do |num, index|
  puts "The index of #{num} is #{index}."
end

# The index of 1 is 0.
# The index of 2 is 1.
# The index of 3 is 2.
# => [1, 2, 3]

{ a: "ant", b: "bear", c: "cat" }.each_with_index do |pair, index|
  puts "The index of #{pair} is #{index}."
end

# The index of [:a, "ant"] is 0.
# The index of [:b, "bear"] is 1.
# The index of [:c, "cat"] is 2.
# => { :a => "ant", :b => "bear", :c => "cat" }
```

- on a hash the first argument now represent an **array** containing both the key and value pairs
- **returns the original calling collection**

### `Enumerable#each_with_object`

Takes a method argument that is a **collection object** that will be returned by the method 

The block takes 2 arguments: 

- first represents the current element
- second represents the collection object that was passed in as an argument to the method

Once done iterating the method returns the collection object that was passed in

```ruby
[1, 2, 3].each_with_object([]) do |num, array|
  array << num if num.odd?
end
# => [1, 3]

{ a: "ant", b: "bear", c: "cat" }.each_with_object([]) do |pair, array|
  array << pair.last
end
# => ["ant", "bear", "cat"]

{ a: "ant", b: "bear", c: "cat" }.each_with_object({}) do |(key, value), hash|
  hash[value] = key
end
# => { "ant" => :a, "bear" => :b, "cat" => :c }
```

### `Enumerable#first`

`first` doesn’t take a block, but does take an optional argument which represents the number of elements to return

- When no argument is given it returns the first element in the collection

```ruby
[1, 2, 3].first
# => 1

{ a: "ant", b: "bear", c: "cat" }.first(2)
# => [[:a, "ant"], [:b, "bear"]]
```

1. Hashes are thought of as unordered and values are retrieved by keys - in Ruby 1.9 and later order is preserved for hashes 
2. Return value of calling on a hash with a numeric argument is a nested array
    1. Can turn nested array back to a hash with `to_h` 

### `Enumerable#include?`

`include?` doesn’t take a block, but it requires 1 argument

Returns `true` if argument exists in the collection

When called on a hash will only check the **keys**

```ruby
[1, 2, 3].include?(1) #=> true

{ a: "ant", b: "bear", c: "cat" }.include?("ant")
# => false

{ a: "ant", b: "bear", c: "cat" }.include?(:a)
# => true

```

- `Hash#include?` is the same as `Hash#key?` or `Hash#has_key?`
- `Hash#value?` returns `true` if the value is located in the hash

### `Enumerable#partition`

`partition` divides up elements in the current collection into two collections depending on the block’s return value

```ruby
[1, 2, 3].partition do |num|
	num.odd?
end
# => [[1, 3], [2]]

odd, even = [1, 2, 3].partition do |num|
  num.odd?
end

odd  # => [1, 3]
even # => [2]
```

- **Return value is a nested array** - inner arrays separated based on the return value of the block
    - `true` values will be grouped together followed by `false`

```ruby
long, short = { a: "ant", b: "bear", c: "cat" }.partition do |key, value|
  value.size > 3
end
# => [[[:b, "bear"]], [[:a, "ant"], [:c, "cat"]]]
```

- will return the key:value pairs in an array where the `true` pairs will be nested together

## Summary

Method documentation:

- one or more method signatures (indicates whether the method takes arguments and/or a block and what it returns)
- A brief description of how the method is used
- some code examples

Things to consider:

- Whether the method takes a block as an argument
- How it handles the block’s return value
- What the method returns itself