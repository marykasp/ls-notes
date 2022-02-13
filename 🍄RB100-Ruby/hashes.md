# Hashes

**Hash** is a data structure that stores items by associated keys - collection of key:value pairs 

- uses symbols as keys and any data type as values 
- add key:value pairs using `[:symbol]` 
- remove using `.delete(:symbol)` method

```ruby
old_syntax_hash = { :name => "bob" }
new_hash = { name: 'bob' }

new_hash[:hair] = "brown"
new_hash[:age] = 62

new_hash.delete(:age)
person = { :eye_color: 'blue' }

person.merge!(new_hash) # modifies the caller
```

## Iterating Over Hashes

- `each` meethod but assign a variable to both the key and the value

- `empty?` method that detects whether a hash has anything in it

- can pass a hash as an argument to a method, can be wrapped in `{}` or can just be comma separated key value pairs

  ```ruby
  def greeting(name, options = {})
    if options.empty?
      puts "Hi my name is #{name}"
    else
      puts "Hi my name is #{name} and I am #{options[:age]} years old."
    end
  end
  
  greeting("Mary")
  greeting("Mary", { age: 32})
  greeting("Mary", age: 32)
  ```

## Common Hash Methods

1. `key?` method checks if a hash contains a specific key - returns a boolean value

2. `select` allows you to pass a block and will return any key-value pairs that evaluate to true when passed into the block 

3. `fetch` pass a given key and it will return the value for that key if it exists 

   ```ruby
   name_and_age = { "Bob" => 42, "Steve" => 31, "Joe" => 19}
   name_and_age.fetch("Larry") # returns keyerror
   name_and_age.fetch("Larry", "Larry isn't in the hash") # returns the error you passed in
   ```

   

4. `to_a` returns an array version of the hash when called - does not mutate the original hash

   ```ruby
   name_age_age.to_a => [["Bob", 42], ["Steve", 31], ["Joe", 19]]
   ```

5. `keys and values` 

   1. `keys` retrieves all the keys from a hash and returns them in array format
   2. `values` retrieves all the values from a hash and returns them in array format