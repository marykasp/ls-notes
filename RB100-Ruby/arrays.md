# Arrays

**array** is an ordered list of elements of any data type, an array literal `[]` 

- `first` method returns the first element of an array
- `last` method returns the last element
- **indexed lists** - zero indexed, can retrieve/access an element from an array using its index position

## Modifying Arrays

- `pop` method removes last item from array, returns that element, mutates the caller

- `push` method takes an argument and adds that value to end of array, returns the array

  - `<<` shovel operator also works like push
  - mutate the caller, original array is modified 

- `map` method iterates over an array applying a code block to each element of the array and returns a new array with those results - does not modify the original

  - `collect` method is an alias to map

  ```ruby
  a = [1, 2, 3, 4]
  a.map { |num| num**2 } => [1, 3, 9, 16]
  ```

- `delete_at` method eliminates a value at a certain index - modifies the original array

  ```ruby
  a.delete_at(1) => 2
  a => [1, 3, 4]
  ```

- `delete` method removes a value from the array, permanently deletes all instances of the provided value from the array

- `uniq` method iterates through an array, deletes any duplicate values that exist, then retuns the result as a new array - does not mutate the caller

  ```ruby
  b = [1, 1, 2, 2, 3, 3, 4]
  b.uniq => [1, 2, 3, 4]
  b => [1, 1, 2, 2, 3, 3, 4]
  ```

  - Adding `!` Bang suffix to this method, the method will act destructively and modify the original array 

## Iteration

`select` method iterates over and array and returns a new array that includes any items that return `true` to the expression provided (similar to the `filter` array method in JS)

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.select { |number| number > 4} => [5, 6, 7, 8, 9, 10]
numbers # remains unchanged
=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

## Methods with `!`

- `!` suffix at end of method name indicates the method will change (mutate) the caller permanently - modifies the original array

## Mutating the Caller

- some methods mutate the original array while others return a new array and do not change the original

## Nested Arrays

- arrays can also contain other arrays will have to use 2 `[]` notations to retrieve an element inside the nested array

  ```ruby
  teams = [['joe', 'steve'], ['frank', 'molly'], ['dan', 'sara']]
  
  teams[1] => ['frank', 'molly']
  ```

## Comparing Arrays

- compare arrays with the equality `==` operator 
- `unshift` adds values to the start of the list



#### `to_s`

- used to create a string representation of an array

  ```ruby
  a = [1, 2, 3]
  puts "It's easy as #{a}" # ruby calls to_s method on the array before concatenating it to the string
  ```

## Array Methods

1. `include?` checks to see if the argument passed in is included in the array - returns a boolean value (**predicates**)

2. `flatten` used to take an array that contains nested arrays and create a one-dimensional array - does NOT mutate the caller

3. `each_index` iterates through the array, the variable represents the index numbers as opposed to the element - passes the index of the ellement into the code block, original array is returned as in `each` method

4. `each_with_index` can manipulate both the value and the index by passing in two parameters to the code block (first value, second index)

5. `sort` orders an array, returns a sorted array - does NOT mutate the caller

6. `product` returns an array that is a combination of all elements from all arrays, is called on an array and takes an array as an argument 

   ```ruby
   a = [1, 2, 3, 4, 5]
   a.include?(3) => true
   
   b = [1, 2, [3, 4, 5], [6, 7]] # nested arrays - returns new array
   b.flatten => [1, 2, 3, 4, 5, 6, 7]
   
   a = [1, 2, 3, 4, 5]
   a.each_index { |i| puts "This is index #{i}"}
   
   a.each_with_index { |val, idx| puts "#{idx + 1}: #{val}"}
   
   [1, 2, 3].product([4, 5])
   => [[1, 4], [1, 5], [2, 4], [2, 5], [3, 4], [3, 5]]
   ```

   

## each vs. map

`each` iterates over a collection and is preferred over the `for` loop - runs the code in the block once for each element and returns the collection it is called on

- with no code block with returns #<Enumerator:..>

`map` when given a block it invokes the block once for each element in the collection - it differs from the `each` method since it creates and returns a new array containing new values, does not modify the caller or return the caller