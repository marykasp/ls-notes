# Practice Prolems: Easy 1

### Problem 1

```ruby
numbers = [1, 2, 2, 3]
numbers.uniq

# uniq method does not mutate the caller
puts numbers # => [1, 2, 2, 3]

# add a ! to end of uniq method to modify the original array
numbers.uniq!
p numbers
# 1
# 2
# 3
```

`uniq` method is called on the `numbers` array - references an Array object containing integers

`uniq` returns a new array containing only the elements that are not repeated - does not affect the original array

- using `!` operator following a method will cause the method to mutate the original array

### Problem 2

Describe the difference between `!` and `?` in Ruby `!` added to the end of a method will cause the method to mutate the caller `?` indicates that the method returns a boolean value

1. what is `!=` and where should you use it?

- `!=` is a comparison operator meaning not equal to, should be used in a conditional statment

1. put `!` before something, like `!user_name`

- `!` before an expression will negate that expression, so will flip the truthiness or falsiness of whatever expression follows

1. put `!` after something like `words.uniq!`

- this is a naming convention used to show that the method will mutate the caller

1. put `?` before something

- this can occur in a ternary operator, where the first operand after the `?` is the expression that will be executed if the conditional statement returns true

1. put `?` after something

- this can occur with a method, usually denotes that the output will be a boolean

1. put `!!` before something, `!!user_name`

- means `not not` and will result in the object or expression boolean equivalent, its truthiness or faslsiness

### Problem 3

Replace the word "important" with "urgent"

```ruby
advice = "Few things in life are as important as house training your pet dinosaur"
advice.gsub!("important", "urgent") # ! will modify the caller
puts advice
```

### Problem 4

`delete_at` deletes the element at the given index and `deletes` deletes all elements that equal the object passed in as an argument

```ruby
numbers = [1, 2, 3, 4, 5]

numbers.delete_at(1) # will delete the element at index 1, removes 2
p numbers # [1, 3, 4, 5]

numbers.delete(1) # will delete the first occurance of the element with a value of 1 if it is in the array
p numbers # [2, 3, 4, 5]
```

### Problem 5

Determine if 42 lies between 10 and 100

```ruby
(10..100).cover?(42)
```

`cover?` method is invoked on a range of numbers and takes an integer as its argument - check if the integer is found between the range of numbers



### Problem 6

Show two differnt way to put the expected "Four score and " in front

```ruby
famous_words = "seven years ago..."
puts "Four score and " + famous_words
puts "Four score and #{famous_words}"

# shovel operator
puts "Four score and " << famous_words
puts famous_words.prepend("Four score and ")
```

### Problem 7

```ruby
flintstones = ["Fred", "Wilma"]
flintstones << ["Barney", "Betty"] # appends an array into the flintstones array of strings
flintstones << ["BamBam", "Pebbles"]

p flintstones # returns an array containing strings and nested arrays as elements
p flintstones.flatten! # flattens the nested array into one array, modifies the caller
```

### Problem 8

Turn this into an array containing only two elements: Barney's name and Barney's number

```ruby
flintstones = { "Fred" => 0, "Wilma" => 1, "Barney" => 2, "Betty" => 3, "BamBam" => 4, "Pebbles" => 5 }

p flintstones.assoc("Barney")
```

`assoc` searches through the hash and compares the argument object with the key and returns the key-value pairs in an array that matches