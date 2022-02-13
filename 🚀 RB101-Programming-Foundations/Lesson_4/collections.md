# Collections

## Element Reference

### `Strings`



`Strings` use integer based index that represents each character in the string, zero indexed

```ruby
str = "abcdefghi"
str[2] => 'c'

# reference multiple (alternative form of #slice method
str[2, 3] => "cde"
str.slice(2, 3)

# method chaining
str[2, 3][0] 
# first slice method returns "cde", then the indexed reference operator returns 'c'
```

How would you reference `grass` from within this string?

```ruby
str = "The grass is green"
str[4, 5] => 'grass'
str.slice(4, 5)
```

`Strings` are not true collections - collections contain multiple objects while strings contain only a single object, a `character.` 

- `Strings` act like collections since you can access and assign each character individually
- the return value of accessing a single character like `str[2]` is a brand new string value

```ruby
char1 = str[2]
char2 = str[2]
char1.object_id == char2.object.id # false
```

### `Arrays`

Arrays are ordered, zero-indexed collections

Lists of elements that are ordered by index, where each element can be any object. Can reference an element by its indexed position.

```ruby
arr = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
arr[2] #=> 'c'

# Array.slice
arr[2, 3] => ['c', 'd', 'e']
arr.slice(3..3) => ['d']
arr.slice(3) => 'd'

# method chaining
arr[2, 3][0] => 'c'

```

`Array#slice` method returns a new array when passed 2 values

- only returns the element when passed a single index

### `Hash`

Hashes use a key-value pair indexed structure where the key or value an be any type of Ruby object

```ruby
hsh = { 'fruit' => 'apple', 'vegetable' => 'carrot' }

hsh['fruit'] => 'apple'
hsh['fruit'][0] => 'a'
```

- Keys must be **unique** when initializing a hash
    - Common to use symbols as keys which are immutable strings
- Values can be duplicated
- Can access keys or just the values with `#keys` and `#values` methods of `Hash` - return an array

```ruby
country_capitals = { uk: 'London', france: 'Paris', germany: 'Berlin' }
country_capitals.keys      # => [:uk, :france, :germany]
country_capitals.values    # => ["London", "Paris", "Berlin"]
country_capitals.values[0] # => "London"
```

### Out of Bounds Indices

Referencing out of bounds index returns `nil` - which could be a valid return value in an array, so how can we tell the difference between a valid return value and the out of bounds reference?

<aside>
💡 `Array#fetch` - returns the element at position index, but throws an `IndexError` exception if the referenced index lies outside of the array bounds

</aside>

```ruby
arr = [3, 'd', nil]
arr.fetch(2) #=> nil
arr.fetch(3) #=> IndexError
```

### Negative Indices

![Untitled](Collections%209fb2f71b70b845a98f447fa51cd76d2b/Untitled%203.png)

![https://d1b1wr57ag5rdp.cloudfront.net/images/collections/array-negative-index-diagram.png](https://d1b1wr57ag5rdp.cloudfront.net/images/collections/array-negative-index-diagram.png)

Elements in `String` and `Array` objects can be referenced using negative indices - the last element in the collection is at `-1` and working backwards

```ruby
str = 'ghijk'
arr = ['g', 'h', 'i', 'j', 'k']

str[-6] # nil
arr[-6] # nil, out of bounds negative indices

arr.fetch(-6) # IndexError
```

### Invalid Hash Keys

`Hash` also has a `fetch` method - returns the value at that `key` but will return a `KeyError` if the key does not exist

```ruby
hsh = { :a => 1, 'b' => 'two', :c => nil }

hsh['b']       # => "two"
hsh[:c]        # => nil
hsh['c']       # => nil
hsh[:d]        # => nil

hsh.fetch(:c)  # => nil
hsh.fetch('c') # => KeyError: key not found: "c"
               #        from (irb):2:in `fetch'
               #        from (irb):2
               #        from /usr/bin/irb:11:in `<main>'
hsh.fetch(:d)  # => KeyError: key not found: :d
               #        from (irb):3:in `fetch'
               #        from (irb):3
               #        from /usr/bin/irb:11:in `<main>'
```

## Conversion

Number of Ruby methods that facilitate type conversion - `String#chars, String#split, Array#join`

```ruby
str = 'Practice'

arr = str.chars # => ["P", "r", "a", "c", "t", "i", "c", "e"]
```

`String#chars` returns an array of individual characters

```ruby
arr.join # => "Practice"
```

`Array#join` returns a string with the elements of the array joined together 

```ruby
str = 'How do you get to Carnegie Hall?'
arr = str.split # => ["How", "do", "you", "get", "to", "Carnegie", "Hall?"]
arr.join        # => "HowdoyougettoCarnegieHall?"

arr.join(" ") # will add a space between the elements of the array
```

`Hash` has a `#to_a` method that returns an array, nested array with each sub-array being equivalent to a key:value pair 

```ruby
hsh = { sky: "blue", grass: "green" }
hsh.to_a # => [[:sky, "blue"], [:grass, "green"]]

arr = [[:name, 'Joe'], [:age, 10], [:favorite_color, 'blue']]
arr.to_h => { :name => 'Joe', :age => 10, :favorite_color => 'blue }
```

`Array#to_h` would turn each sub-array into a key:value pair of a hash collection 

## Element Assignment

### `String`

Element assignment `Str[index]` in order to change the value of a specific character within the string

```ruby
str = "joe's favorite color is blue"
str[0] = 'J'
str # => "Joe's favorite color is blue"

str[6] = "F"
str[15] = "C"
str[21] = "I"
str[24] = "B"

# do same thing as a loop - map returns a new array
str_arr = str.split.map do |word|
	word.capitalize
end

str_arr.join(" ")
```

### `Array`

Can assign elements of an array by using **element assignment** `Array[index]` 

```ruby
arr = [1, 2, 3, 4, 5]
arr[0] += 1 # => 2
# shorthand for arr[0] = arr[0] + 1
arr         # => [2, 2, 3, 4, 5]

arr[1] += 1
arr[2] += 1
arr[3] += 1
arr[4] += 1

new_arr = arr.map do |num|
	num + 1
end

puts new_arr => [2, 3, 4, 5, 6]
```

### `Hash`

The hash key is used to assign a value

```ruby
hsh = { apple: 'Produce', carrot: 'Produce', pear: 'Produce', broccoli: 'Produce' }

hsh[:apple] = 'Fruit'
hsh # => { :apple => "Fruit", :carrot => "Produce", :pear => "Produce", :broccoli => "Produce" }

hsh[:carrot] = 'Vegetable'
hsh[:pear] = 'Fruit'
hsh[:broccoli] = 'Vegetable'

```