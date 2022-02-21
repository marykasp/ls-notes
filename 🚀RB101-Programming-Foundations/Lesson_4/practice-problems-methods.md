# Practice Problems: Methods

## Practice Problem 1


💡 What is the return value of the `select` method below? Why?

```ruby
[1, 2, 3].select do |num|
	num > 5
	'hi'
end
# => [1, 2, 3]
```

`select` examines the block’s return value and if it is **truthy** then `select` will take the element of the current iteration and add it to a new collection 

- In this case the last expression of the block **always** returns true (since the last line is a string `hi` which is a truthy value)
- since the last expression of the block is truthy upon every iteration, `select` will return a new array containing all of the elements of the original array `[1, 2, 3]`

## Practice Problem 2


💡 How does `count` treat the block’s return value? How can we find out?

```ruby
['ant', 'bat', 'caterpillar'].count do |str|
	str.length < 4
end
#=> 2
```

If the block returns a `true` value for the current element, the `count` method will count that element. `count` considers the truthiness of the block’s return value and returns an integer value

- `count` counts the number of elements for which the block returns a `true` value

## Practice Problem 3


💡 What is the return value of `reject` in the following code? Why?

```ruby
[1, 2, 3].reject do |num|
	puts num
end
# => [1, 2, 3] puts returns nil which is a false value, so each element in the array is returned
```

`reject` returns an array for all ements for which the given block returns `false` 

- In this case the block expression uses `puts` which returns `nil`
- `nil` is a false value so `reject` will return a new array of all the elements of the original array

## Practice Problem 4


💡 What is the return value of `each_with_object` in the following code? Why?




```ruby
['ant', 'bear', 'cat'].each_with_object({}) do |value, hash|
	hash[value[0]] = value
end

# => {"a" => 'ant', "b" => 'bear', "c" => 'cat' }
```

`each_with_object` method takes a **collection object** as its method argument and also takes a code block as an argument. The first argument in the code block is the current element in the array/hash being called on. While the second argument refers to the collection object passed in to the method. 

- upon each iteration of the code block, the updated value will be added to the collection object
- will return the initially given object which now contains all of the updates

## Practice Problem 5


💡 What does `shift` do in the following code? How can we find out?




```ruby
hash = { a: 'ant', b: 'bear' }
hash.shift # => [:a, 'ant']

hash # => { b: 'bear' }
```

`shift` based on the ruby-docs is an `Array` and `Hash` method that removes the first element of the caller and returns it, mutating the caller

- for an array it returns the element
- for a hash it returns the key:value pair as an array `[key,value]`

## Practice Problem 6


💡 What is the return value of the following statement? Why?




```ruby
['ant', 'bear', 'caterpillar'].pop.size # => 11
```

`pop` returns the last element of the collection, mutates the caller - modifies the original collection

`size` returns the length of the `String` or `Array` it is called on

- in this case `pop` returns a `String` element from the array caller - “`caterpillar`"
- `"caterpillar".size` returns `11`

## Practice Problem 7


💡 What is the **block’s** return value in the following code? How is it determined? Also what is the return value of `any?` ? What is the code output




```ruby
[1, 2, 3].any? do |num|
	puts num
	num.odd? # last expression evaluated
end
# 1
# => true

# iteration will only occur once since the first element evaluates to true
# puts num will occur on that first iteration printing 1
# any? will return true since the code block returned a truthy value
```

**block’s** return value is a boolean value based on if the current element in the iteration is an odd number - `true`, `false, true`

The return value of `any?` is a boolean value - will return `true` if the block ever returns a value other than `false` and `nil` 

After the first iteration `any?` returns `true` and stops iterating since there is no need to evaluate the remainder of the array 

## Practice Problem 8


💡 How does `take` word? Is it destructive?




Returns the first number of elements from the array based on the integer argument. Will need to test in `irb` to see if it is a destructive method 

```ruby
arr = [1, 2, 3, 4, 5]
arr.take(2) #=> [1, 2]

arr #=> [1, 2, 3, 4, 5}
```

Not a destructive method, does mutate the caller. The original array remains the same

## Practice Problem 9

What is the return value of `map` in the following code? Why?

```ruby
{ a: 'ant', b: 'bear' }.map do |key, value|
  if value.size > 3
    value
  end
end
# => [nil, 'bear']
```

`map` returns a new array based on the modifed value returned from the block

- When none of the conditions in the `if` statement evaluates as true, `if` statement itself returns `nil`
- So since the first element does not pass the `if` statement, `nil` is returned upon the first iteration
- The second element does pass the conditional and the value is returned so that value becomes the second element in the array returned from `map` method

## Practice Problem 10

What is the return value of the following code? Why?

```ruby
[1, 2, 3].map do |num|
	if num > 1
		puts num
	else
		num
	end
end

# => [1, nil, nil]
```

Can determine the block’s return value by looking at the return value of the last expression evaluated within the block

- For the first element, the `if` condition evaluates to false, which means `num` is the block’s return value for that iteration
- For teh second and third elements the `if` condition is true and the last statement is `puts num` which returns `nil`