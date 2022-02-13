# Working With Blocks

### Example 1

```ruby
[[1, 2], [3, 4]].each do |arr|
	puts arr.first
end
```

1. `Array#each` method is being called on a nested array (multi-dimensional) array
2. Each inner array is passed to the block and assigned to the local variable `arr`
3. `Array#first` method is called on the inner arrays and returns the object at index `0` of the current array - `1 and 3`
4. `puts` method then outputs the string representation of the integer
5. `puts` returns `nil` so the return value of the block is `nil` 
6. `each` doesn’t consider the return value of the `block` but instead returns the original collection that it was called on 

| Line | Action | Object | Side Effect | Return Value | Return value used? |
| --- | --- | --- | --- | --- | --- |
| 1 | method each | The outer array | None | original collection | No |
| 1-3 | block execution | Each sub-array | None | nil | no |
| 2 | method call first | each sub-array | None | element at index 0 of each sub array | Yes by puts |
| 2 | method call puts | Element at index 0 of each sub array  | outputs string representation of object | nil | yes determines return value of block |

### Example 2

```ruby
[[1,2], [3,4]].map do |arr|
	puts arr.first
end
```

1. `Array#map` is called on a multi-dimensional array - takes a block as an argument
2. The subarrays of the outer array are passed into the block and assigned to the local variable `arr`
3. Inside the block `Array#first` method is called on the subarray - retrieves the object at index `0`
4. `puts` method than outputs the string representation of that integer object
5. `puts` returns `nil` so the return value of the block for each iteration is `nil` 
6. `map` does use the block’s return value for transformation and puts that value into a new array
7. `map` will return a new array of the values returns from each iteration:  `[nil, nil]` 

**map performs transformation based on the return value of the block** 

| Line | Action | Object | Side Effect | Return Value | Return Value Used? |
| --- | --- | --- | --- | --- | --- |
| 1 | method call map | Outer array | None | new array [`nil`, nil] | No  |
| 1-3 | block execution | Each sub-array | None | nil | Yes used by map for transformation |
| 2 | method call first | Each sub-array | None | Object at index 0 of sub-array | Yes by puts |
| 2 | method call puts | Object at index 0 of sub-array | Outputs a string representation of object | nil | Yes used to determine block’s return value |

### Example 3

```ruby
[[1, 2], [3, 4]].map do |arr|
	puts arr.first # returns object at 0 index in subarray to puts 
	arr.first # returns object at 0 index in subarray - added to a new collection
end
# [1, 3]
```

1. `Array#map` is called on a multi-dimensional array
2. The subarrays are passed into the block and assigned to the local variable `arr`
3. Inside the block `Array#first` is called on the subarray which returns the element at the `0` index position
    1. That integer is passed to `puts` method which prints out a string representation of the integer and returns `nil`
4. On the last line of the block `Array#first` is called on the subarray - returns the element at index `0`
5. `map` takes the return value of the block and puts those values in a new array
6. Since `arr.first` is the last line of the block that return value will be used - so `1` and `3` will be added to a new array and returned by `map`

| Line | Action | Object | Side Effect | Return Value | Is return value used? |
| --- | --- | --- | --- | --- | --- |
| 1 | method call map | outer array | None | New array [1, 3] | No but shown on in irb |
| 1-4 | block execution | each subarray | None | integer at index 0 of each subarray: 1 first iteration, 3 second iteration | yes used by map for transformation |
| 2 | method call first | each subarray | none | Element at index 0 of subarray | Yes used by puts |
| 2 | method call puts | Element at index 0 of each subarray | Outputs a string represenation | nil | No |
| 3 | method call first | each subarray | None | Element at index 0 of subarray | Yes used to determine return value of block |

### Example 4

```ruby
my_arr = [[18, 7], [3, 12]].each do |arr|
	arr.each do |num|
		if num > 5
			puts num
		end
	end
end
```

1. `Array#each` is called on a multidimensional array
2. The subarray is passed into the code block upon each iteration and assigned to the local variable `arr`
3. the subarray is then iterated through by calling `Array.each`
4. Each integer object is passed into the inner `each` block and assigned to the local variable `num`
5. Conditional `if` statement is used, to check if the integer is `>` than 5
    1. if returns `true` then `num` is passed to `puts` method - prints the string representation of the integer: would print `18` `7` and `12`
    2. returns `nil`
6. The inner `each` code block returns the original subaray - `[18, 7]` and then `[3, 12]`
7. The outer `each` method does not use the blocks return value and just returns the original collection
8. `my_arr` = `[[18, 7], [3, 12]]`

| Line | Action | Object | Side Effect | Return value | Return value used? |
| --- | --- | --- | --- | --- | --- |
| 1 | Variable assignment | [[18, 7], [3, 12]] | None | [[18, 7], [3, 12]] | No |
| 1 | Method call each | Outer array | None | The calling object [[18, 7], [3, 12]] | Yes used by variable assignment to my_arr |
| 1-7 | outer block execution | Each subarray | None | Each sub-array | No |
| 2 | method call each | Each subarray | None | The calling object: subarray in current iteration | Yes, used to determine return value of outer block |
| 2-6 | inner block execution | Element of the subarray of that iteration | None | nil | No |
| 3 | Comparison | Element of the subarray iteration | None | Boolean | Yes evaluated by if |
| 3-5 | conditional if | The result of the expression num > 5 | None | nil | Yes used to determine return value of inner block |
| 4 | method call puts | Element of the subarray of that iteration | Outputs a string | nil | Yes used to determine return value of the conditional statement if the condition is met |

**`each` ignores the blocks return values and returns the original collection** 

### Example 5

```ruby
[[1, 2], [3, 4]].map do |arr|
  arr.map do |num|
    num * 2
  end
end
```

1. Multidimensional array is passed to the `map` method
2. The subarray is then passed into the block and assigned to the local variable `arr`
3. Inside the block the subarray is iterated through using the `map` method
4. The integer object of the subarrays are passed into the inner `map` block and assigned to the local variable `num`
5. Inside the inner `map` method the `num` is multiplied by 2
6. `map` does take into consideration the block’s return value and that value is used for transformation
7. the inner `map` method will return a new array for each subarray that has been transformed - `[2, 4]`, `[6, 8]`
8. the arrays returned by the inner `map` method are then used by the outer `map` method to create a new array collection - `[[2,4], [6,8]]`

| Line | Action | Object | Side Effect | Return Value | Used? |
| --- | --- | --- | --- | --- | --- |
| 1 | Method call map | Outer array | No | new transformed collection [[2,4].[6.8]] | No |
| 1-5 | Outer Block execution | Outer array | No | New array collection | Yes, by map method for transformed new collection |
| 2 | Method call map | Each subarray | No | New subarray with transformed values | Yes, used by outer map method for new transformed array |
| 2-4 | Inner block execution | Element of the subarray of that iteration | No | New transformed subarrays [2,4] [6,8] | Yes, used by outer map method to create new outer array |
| 3 | num * 2 | Element integer of the subarray of that iteration | No | Transformed integer: 2, 4, 6, 8 | Yes, used by inner map method to transform the subarrays |
|  |  |  |  |  |  |

### Example 6

```ruby
[{ a: 'ant', b: 'elephant' }, { c: 'cat' }].select do |hash|
  hash.all? do |key, value|
    value[0] == key.to_s
  end
end
# => [{ :c => "cat" }]
```

1. Array of nested hashes is passed to the `select` method
2. Each nested hash is passed to the block and assigned to the local `hash` variable
3. Inside the block `all?` is called on each nested hash
    1. block takes two arguments `key, value` of the nested hash
4. Inside the `all?` block, the first character of the value `value[0]` is compared to the string value of the `key` using the equallity `==` comparison operator
    1. `all?` will only return `true` if no element passed into the block returns `false`
    2. For the first nested object `{ a: 'ant', b: 'elephant' }` the second `key:value` pair will return `false` so overall `all?` will return `false` for that nested object
    3. upon the next iteration of `select` the second nested object `{c: 'cat'}` will be passed to the `all` method
    4. the condition inside the method returns `true` so `all?` method will return `true`
5. `select` method takes into consideration the return value of the block and will add the element that returns a truthy value to a new array - so `{c: 'cat'}` will be added to a new array and returned 

`select` cares about the truthiness of the block’s return value, so using a method that returns a boolean works well inside the block

### Example 7 - Sorting Nested Data Structures

```ruby
arr = [['1', '8', '11'], ['2', '6', '13'], ['2', '12', '15'], ['1', '8', '9']]

arr.sort_by do |sub_arr|
	sub_arr.map do |num|
		num.to_i
	end
end
```

1. Each of the inner arrays are compared to the other inner arrays

1. The elements inside the inner arrays are compared to the elements in the other inner arrays - element by element
- First need to transform the elements of the inner array before sorting the entire array
- Strings are compared character by character - not a numerical comparison
- First have to carry about a transformation, the transformed elements are then used to perform the comparison

### Example 8

```ruby
[[8, 13, 27], ['apple', 'banana', 'cantaloupe']].map do |arr|
  arr.select do |item|
    if item.to_s.to_i == item    # if it's an integer
      item > 13
    else
      item.size < 6
    end
  end
end
# => [[27], ["apple"]]
```

- first need to access the nested arrays to access the elements to do the selections
1. `map` method is called on the outer array and the subarray is passed into the block
2. Inside the `map` block the `select` method is called on each subarray and the elements of the subarray are assigned to the `item` local variable and passed into the `select` block
    1. `select` returns the element for which the block returns `true`
    2. inside the `select` block a conditional `if/else` statement is used to check if the `element` is an integer `> 13` or a `string` with a `string.length < 6` 
    3. If returns `true` that element is added to a new subarray
3. The new subarrays containing the selected elements are returned from the `select` method and used by the `map` method to return a new multidimensional array containing only the selected elements
- since `select` is the last expression evaluated in the `map` block its return value determines the transformed values used by the `map` outer block

### Example 9

```ruby
[[[1], [2], [3], [4]], [['a'], ['b'], ['c']]].map do |element1|
  element1.each do |element2|
    element2.partition do |element3|
      element3.size > 0
    end
  end
end
# => [[[1], [2], [3], [4]], [["a"], ["b"], ["c"]]]
```

1. Multidimensional array - contains 2 arrays which also contain arrays. `map` method is called on the nested array and the subarrays are asssigned to `element1`
2. `each` method inside the block is called on the subarrays 
3. Inside the `each` method the inner arrays of the subarray are passed to the `partition method`
4. Inside the `partition` method the inner array length is checked to see if it is greater than 0
5. The return value of the `partition` method will have no effect on the `each` method though - since `each` just returns the original collection
6. The original subarrays will be returned from the `map` block and assigned to a new array

### Example 10

```ruby
[[[1, 2], [3, 4]], [5, 6]].map do |arr|
  arr.map do |el|
    if el.to_s.size == 1    # it's an integer
      el + 1
    else                    # it's an array
      el.map do |n|
        n + 1
      end
    end
  end
end
```

1. `map` method is called on a Multidimensional array - 2 elements (an array that contains 2 nested arrays) and an array of integers 
2. The subarrays are passed to the `map` block and assigned to the local variable `arr` for each iteration
3. Inside the `map` block the `map` method is called on the subarrays and the elements are passed to the inner block
    1. `if` conditional converts the element to a string and then checks it length, if equal to 1 then the the block will be executed - this is checking to see if the element is an integer or an array
        1. if `true` then 1 will be added to the element and that value will be returned to the inner `map` method and added to a new subarray
        2. If `false` then another `map` method will be called on the element (inner array) and the integer objects that make up the inner array will be passed to the block
            1. the `map` method then adds 1 to the integer object and that integer is then returned to the innermost `map` method and added to a inner array
            
4. The return value from the second `map` block will be used by the outer `map` block to transform the multidimensional array 

```ruby
[[[2, 3], [4, 5]], [6, 7]] 
```

### Mutating Collections While Iterating

***Do not mutate the collection that you’re iterating through***

Iteration is the basis of selection and transformation, don’t mutate the original collection instead create a new collection with either the selected or transformed values (`map`, `select`)

- don’t use destructive methods while iterating through the collection to perform a transformation ont he collection

```ruby
# will modify the original object in the collection
# create a clone of the collection - the elements in the collection still refer to the same location as the elements in the original
# iterate over the cloned array with each method, delete the number from the array collection
# can still track the index order in the cloned_arr
def remove_evens!(arr)
  cloned_arr = arr.dup 
  cloned_arr.each do |num|
    if num % 2 == 0
      arr.delete(num)
    end
  end
  arr
end
```