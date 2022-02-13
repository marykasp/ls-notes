# Sorting

Sorting is mostly performed on arrays; since items in an array are accessed via their index, the order in which those items appear is important

- `Strings` don’t have access to sorting methods - but can be easily converted into arrays
- `Hash` objects now can be sorted; but generally don’t need to since can access values via their keys

<aside>
💡 Sorting is setting the order of the items in a collection according to a certain criterion



```ruby
[2, 5, 3, 4, 1].sort
[1, 2, 3, 4 ,5] # ordered numerically
```

`sort` is called on an array and **returns a new array** with the same elements from the original sorted - integers ordered sequentially according to their value

How does `sort` apply criterion in order to return an ordered collection?

### Comparison

Sorting is carried out by *comparing* the items in a collection with each other and ordering them based on the result of that comparison. 

```ruby
['c', 'a', 'e', 'b', 'd'].sort # => ['a', 'b', 'c', 'd', 'e']
```

`sort` on an array of characters returns a new array of characters ordered alphabetically 

### `<=>` method

Any object in a collection we want to sort **must** implement the `<=>` method - performs comparisons between two objects of the same type and returns `-1, 0, 1` depending upon whether the first object is less than, equal to, or greater than the second object 

- `nil` is returned if trying to compare two different types of objects

```ruby
2 <==> 1 # 1
1 <==> 2 # -1
2 <==> 2 # 0

'b' <==> 'a' # 1
'a' <==> 'b' # -1
"b" <==> "b" # 0
1 <==> 'a' 
```

The return value of `<=>` method is used by `sort` method to determine the order in which to place the items 

- `<=>` returns `nil` the `sort` method throws an **ArgumentError**

`String#<=>` 

- `String` order is determined by the character’s position in the ASCII table:
    - Uppercase letters come before lowercase letters
    - Digits and punction comes before letters (most not all)
    - Extended table that contains accented and other characters - comes after the main ASCII table

### The `sort` method

Call `sort` on an array returns a **new array of ordered items** - comparisons are carried out using the `<=>` method on the items being sorted 

- call `sort` with a *block passed as argumen*t - control how the items are being sorted - block needs to return `-1, 0 1`

```ruby
[2, 5, 3, 4, 1].sort do |a, b|
	puts "#{a} compared to #{b} equals #{a <==> b}"
	a <=> b
end
# => [1, 2, 3, 4, 5] Ascending Order

[2, 5, 3, 4, 1].sort do |a, b|
	b <=> a
end
# => [5, 4, 3, 2, 1] Descending Order
```

```ruby
['arc', 'bat', 'cape', 'ants', 'cap'].sort
# => ['ants', 'arc', 'bat', 'cap', 'cape']
```

`String#<=>` compares multi-line strings character by character, if both characters are the same the next character in the string is compared 

- `cape` is longer than `cap` and so is considered *greater*

### Nested Array `<==>`

Each object in an array is compared in an element wise manner - so the first object in all the arrays is compared initially

- first element in each subarray is compared, then the second, and so on

### The `sort_by` method

Usually called with a **block** - it determines how the items are compared

```ruby
['cot', 'bed', 'mat'].sort_by do |word|
	word[1] # compare based on the second character in the multiline string
end
# => ['mat', 'bed', 'cot']
```

Used to sort `hashes` - **two arguments need to be passed to the block** - the key and the value 

`sort_by` returns a new array even when called on a `hash` - key:value pairs are grouped in a nested array 

```ruby
people = { Kate: 27, john: 25, Mike:  18 }

people.sort_by do |_, age|
	age
end
# => [[:Mike, 18], [:john, 25], [:Kate, 27]]

people.sort_by do |name, _|
	name.capitalize # since john is not a capital "J" will come after the other two names
end
# => [[:John, 25], [:Mike, 18], [:Kate, 27]]
```

- always returns an **array** - result would be a new array with the key:value pairs as objects in nested arrays
    - can convert back to a hash using `Array#to_h`
    

## Summary

- Sorting is complex to carry out algorithmically on your own, but can use both `sort` an `sort_by` methods to do the complex work for us
- *Comparison* is at the heart of sorting. When sorting collections you need to know if the objects you want to sort on implement `<=>` method and how that method is defined for that object type
- Methods other than `sort` and `sort_by` also use comparison as the basis for how they work
    - `min`
    - `max`
    - `minmax`
    - `min_by`
    - `max_by`