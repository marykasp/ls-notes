# Loops

If you want to perform a single action on each element in a collection, you can use a loop 

```ruby
arr = [1, 2, 3, 4, 5]
counter = 0

# increments each element in the array by 1
loop do
  arr[counter] += 1
  counter += 1
  break if counter == arr.size
end

arr # => [2, 3, 4, 5, 6]
```

`Kernel#loop` takes a block as its argument - any code within the block will be executed upon each iteration of the loop

- `break` keyword will exit out of the loop, can use a conditional statement following so `break` is only executed when a specific condition occurs

```ruby
loop do
  number = rand(1..10)   # a random number between 1 and 10
  puts 'Hello!'
  break if number == 5 # will break ouf the loop if the random number is 5
end
```

## Iteration

Can track the number of iterations the loop performs by using a `counter` variable - 

- initialize the `counter` before the loop is implemented
- inside the loop increment the counter by 1 during each iteration

```ruby
counter = 0

loop do # prints 'Hello' 5 times
  puts 'Hello!'
  counter += 1
  break if counter == 5
end
```

## `Break` Placement

`break` on the last line of the loop mimics a `do/while` loop - **the code within the block is guaranteed to execute at least once**

`break` is first line in the loop will mimic a `while loop` - if the condition evaluates to true, the loop block will be executed, if not the loop will stop 

### `Next`

`next` tells the loop to skip the rest of the current iteration and begin the next one

```ruby
counter = 0

# skips all the odd numbers, prints even numbers up to 6
loop do
  counter += 1
  next if counter.odd?
  puts counter
  break if counter > 5
end
```

## Iterating Over Collections

### `String`

Use a `counter` variable to keep track of the position within the string, use it in the element assignment to retrieve the character from the string - `str[counter]`

- `counter` represents the index value for each character

`break` out of the loop when the `counter` is equal to or greater than the `str.size` 

`str.size` returns the number of characters in a given string

```ruby
alphabet = 'abcdefghijklmnopqrstuvwxyz'
counter = 0

loop do
  break if counter >= alphabet.size
  puts alphabet[counter]
  counter += 1
end
```

### `Array`

```ruby
colors = ['green', 'blue', 'purple', 'orange']
counter = 0

loop do
  break if counter >= colors.size
  puts "I'm the color #{colors[counter]}!"
  counter += 1
end

# different type of objects in the array
objects = ['hello', :key, 10, []]
counter = 0

loop do
	break if counter >= objects.size
	puts objects[counter].class # returns the type class of each element
	counter += 1
end
```

### `Hash`

Using loop to iterate over a hash requires a couple more steps - uses key:value pairs instead of index values so can’t use the `counter` variable to retrieve an element 

```ruby
number_of_pets = {
  'dogs' => 2,
  'cats' => 4,
  'fish' => 1
}
pets = number_of_pets.keys # => ['dogs', 'cats', 'fish']
counter = 0

loop do
  break if counter == number_of_pets.size
  current_pet = pets[counter]
  current_pet_number = number_of_pets[current_pet]
  puts "I have #{current_pet_number} #{current_pet}!"
  counter += 1
end
```

1. create an array containing all the keys in the hash `Hash#keys` - returns an array containing all of the keys in the hash
2. Use the new array of keys to iterate over the hash
- iterate over the array of keys using the `counter variable` and saving each key into a new variable
- then use that new variable key to retrieve the value out of the pets hash