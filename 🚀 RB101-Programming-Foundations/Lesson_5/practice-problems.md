# Practice Problems

Focus on:

1. the structure of the collection object
2. return value of the blocks and methods
3. side effects of any methods

### Practice Problem 1

How would you order this array of number strings by descending numeric value?

1. `sort` to sort the elements in the array

```ruby
arr = ['10', '11', '9', '7', '8']

arr.sort do |a, b|
	b.to_i <=> a.to_i
end
```

- first convert the strings to integers in the block
- sort the array in reverse order - switch the order of `b` and `a`

### Practice Problem 2

How would you order this array of hashes on the year of the publication of each book from earliest to latest?

```ruby
books = [
  {title: 'One Hundred Years of Solitude', author: 'Gabriel Garcia Marquez', published: '1967'},
  {title: 'The Great Gatsby', author: 'F. Scott Fitzgerald', published: '1925'},
  {title: 'War and Peace', author: 'Leo Tolstoy', published: '1869'},
  {title: 'Ulysses', author: 'James Joyce', published: '1922'}
]

books.sort_by do |book|
	book[:published]
end
```

- used `sort_by` to access a particular value in each hash by which to sort
- the publication values are `strings` so they can implement the `<=>` method
- since they are all the same length we can compare the strings and not have to convert to integers

### Practice Problem 3

For each of these collection objects demonstrate how you would reference the letter `g`

```ruby
arr1 = ['a', 'b', ['c', ['d', 'e', 'f', 'g']]]

arr2 = [{first: ['a', 'b', 'c'], second: ['d', 'e', 'f']}, {third: ['g', 'h', 'i']}]

arr3 = [['abc'], ['def'], {third: ['ghi']}]

hsh1 = {'a' => ['d', 'e'], 'b' => ['f', 'g'], 'c' => ['h', 'i']}

hsh2 = {first: {'d' => 3}, second: {'e' => 2, 'f' => 1}, third: {'g' => 0}}

# Access letter g
arr1[2][1][3]

arr2[1][:third][0]

arr3[2][:third][0][0]

hsh1['b'][1]

hsh2[:third].key(0) # returns the key of the occurence of a given value
```

`Hash#key` returns a single key based on the value passed to the method

`Hash#keys` returns an array of all the keys in the hash

- `hsh2[:third].keys[0]` - would select the first key from the keys array

### Practice Problem 4

For each of these collection objects where the value `3` occurs, demonstrate how you would change this to `4`

```ruby

arr1 = [1, [2, 3], 4]

arr2 = [{a: 1}, {b: 2, c: [7, 6, 5], d: 4}, 3]

hsh1 = {first: [1, 2, [3]]}

hsh2 = {['a'] => {a: ['1', :two, 3], b: 4}, 'b' => 5}

# change value 3 to 4 - reassignment of an element in a collection
arr1[1][1] = 4

arr2[2] = 4

hsh1[:first][2][0] = 4

hsh2[['a']][:a][2] = 4
```

### Practice Problem 5

Figure out the total age of just the male members of the family

```ruby
munsters = {
  "Herman" => { "age" => 32, "gender" => "male" },
  "Lily" => { "age" => 30, "gender" => "female" },
  "Grandpa" => { "age" => 402, "gender" => "male" },
  "Eddie" => { "age" => 10, "gender" => "male" },
  "Marilyn" => { "age" => 23, "gender" => "female"}
}

total_male_age = 0
# since not using key values from the outer array can just access the values 
munsters.each_value do |details|
	details["age"] += total_male_age if details["gender"] == "male"
end
```

While iterating through the outer hash, we need to access two values from the inner hash

### Practice Problem 6

Print out the name, age, and gender of each family member

```ruby
# (Name) is a (age)-year-old (male or female)

munsters = {
  "Herman" => { "age" => 32, "gender" => "male" },
  "Lily" => { "age" => 30, "gender" => "female" },
  "Grandpa" => { "age" => 402, "gender" => "male" },
  "Eddie" => { "age" => 10, "gender" => "male" },
  "Marilyn" => { "age" => 23, "gender" => "female"}
}

munsters.each do |name, details|
	age = details["age"]
	gender = details["gender"]

	puts "#{name} is a #{age}-year-old #{gender}"
end

munsters.each_pair do |name, details|
	puts "#{name} is a #{details["age"]}-year-old #{details["gender"]}"
end
```

### Practice Problem 7

What would the final values of `a` and `b` 

```ruby
a = 2 # assignment to an integer - a points to the value in memory
b = [5, 8] # b is assigned to an array in memory
arr = [a, b] # array is assigned to a new array that contains values that a and b point to

arr[0] += 2 # reassignment so the value in the array at 0 now points to a new value in memory
arr[1][0] -= a # b points to an array and this effects the element in that collection, so b will also be modified

# a = 2
# b = [3, 8]
# arr = [4, [3, 8]]
```

`arr[0] += 2` was modifying the array, reassigning the object at index `0` - now points to a new location in memory

`arr[1]` selects the inner array `[5, 8]` 

`arr[1][0]` selects the element of that inner array at index 0 which would be `5` 

since `b` points to an array and this element reference modifies the object inside that array the entire collection would then be modified - assigning a new value at index 0 of that array 

### Practice Problem 8

Using `each` method write some code to output all of the vowels from the strings

```ruby
hsh = {first: ['the', 'quick'], second: ['brown', 'fox'], third: ['jumped'], fourth: ['over', 'the', 'lazy', 'dog']}

hsh.each do |_, arr|
	arr.each do |str|
		str.chars.each do |character|
			puts character if 'aeiou'.include?(character)
		end
	end
end
```

- first iterate through the hash to access the values (arrays)
- iterate through each array to access each `string`
- `String#chars` to conver the string into an array of characters
- then iterate over the array of characters and print the character to the string with `puts` if the condition is met - check if the character is included in the `aeiou` string
- can create a `vowels` variable that contains the `aeiou` string before iteration

### Practice Problem 9

Return a **new array** of the same structure but with each sub array being ordered in descending order

```ruby
arr = [['b', 'c', 'a'], [2, 1, 3], ['blue', 'black', 'green']]

arr.map do |subarr|
	subarr.sort do |a, b|
		b <=> a
	end
end
```

### Practice Problem 10

Without modifying the original array, use the `map` method to return a new array identical in structure to the original but where the value of each integer is incremented by 1

```ruby
[{a: 1}, {b: 2, c: 3}, {d: 4, e: 5, f: 6}].map do |hash|
	incremented_hash = {}
	hash.each do |key, num|
		incremented_hash[key] = num + 1
	end
	incremented_hash
end
```

```ruby
[{a: 1}, {b: 2, c: 3}, {d: 4, e: 5, f: 6}].each_with_object([]) do |hsh, arr|
	incremented_hash = {}
	hsh.each do |key, value|
		incremented_hash[key] = value + 1
	end
	arr << incremented_hash
end
```

- `map` is called on the array of nested hashes - `map` returns an array, on a hash will return an array of key:value pairs rather than a new hash
    - so first need to create a new hash with the transformed values to be returned by the block so `map` can use to create a new array collection
    - inside the `map` block call `each` method on the nested hashes
        - add the key with the new value to the newly transformed hash
    - last line in the `map` block should return the incremented_hash

### Practice Problem 11

Use a combination of methods, `select` or `reject` to return a new array identical in structure to the original but containing only the integers that are multiples of 3

```ruby
arr = [[2], [3, 5, 7], [9], [11, 13, 15]]

# need to access the inner subarrays
arr.map do |subarr|
	subarr.select do |num|
		num % 3 == 0
	end
end

# => [[], [3], [9], [15]]
```

Since we want to return a new array can use `map` to call on the original array

Use `select` on the subarrays to iterate through the integer objects to check if they are divisible by 3, if returns `true` that value will be added to a new array

### Practice Problem 12

Without using the `Array#to_h` method write code that returuns a hash where the key is the first item in each subarray and the value is the second item

```ruby
arr = [[:a, 1], ['b', 'two'], ['sea', {c: 3}], [{a: 1, b: 2, c: 3, d: 4}, 'D']]
# expected return value: {:a=>1, "b"=>"two", "sea"=>{:c=>3}, {:a=>1, :b=>2, :c=>3, :d=>4}=>"D"}

new_hash = {}
arr.each do |subarr|
	key = subarr[0]
	value = subarr[1]

	new_hash[key] = value
end

p new_hash
```

### Practice Problem 13

Return a new array containing the same sub-arrays as the original but ordered logically by only taking into consideration the odd numbers they contain

```ruby
arr = [[1, 6, 9], [6, 1, 7], [1, 8, 3], [1, 5, 9]]

# only sort the odd numbers 

# return a new array with same subarrays that are ordered
arr.sort_by do |subarr|
	subarr.select do |num|
		num.odd?
	end
end
```

### ⭐Practice Problem 14

Write code that returns a new array containing the colors of the fruits and the sizes of the vegetables - sizes should be UPCASE and colors Capitalized

```ruby
hsh = {
  'grape' => {type: 'fruit', colors: ['red', 'green'], size: 'small'},
  'carrot' => {type: 'vegetable', colors: ['orange'], size: 'medium'},
  'apple' => {type: 'fruit', colors: ['red', 'green'], size: 'medium'},
  'apricot' => {type: 'fruit', colors: ['orange'], size: 'medium'},
  'marrow' => {type: 'vegetable', colors: ['green'], size: 'large'},
}

hsh.map do |_, hash|
	if hash[:type] == 'fruit'
		hash[:colors].map do |color|
			color.capitalize!
		end
	elsif hash[:type] == "vegetable"
			hash[:size].upcase
	end
end

```

- want to return an array where each item in the outer hash is represented by a particular value from within each nested hash

### Practice Problem 15

Return an array which contains only the hashes where **ALL** integers are **even**

```ruby
arr = [{a: [1, 2, 3]}, {b: [2, 4, 6], c: [3, 6], d: [4]}, {e: [8], f: [6, 10]}]

arr.select do |hash|
	hash.all? do |_, value|
		value.all? do |num|
			num.even?
		end
	end
end
```