# More Practice Problems: Methods

## Practice Problem 1

<aside>
💡 Given the array, turn this array into a hash where the names are the keys and the values are the positions in the array

</aside>

```ruby
flintstones = ["Fred", "Barney", "Wilma", "Betty", "Pebbles", "BamBam"]

flintstones_hash = {}

flintstones.each_with_index do |name, index|
	flintstones_hash[name] = index
end # returns the original collection: 
# => ["Fred", "Barney", "Wilma", "Betty", "Pebbles", "BamBam"]

flintstones_hash # => {"Fred"=>0, "Barney"=>1, "Wilma"=>2, "Betty"=>3, "Pebbles"=>4, "BamBam"=>5}

# using each_with_object followed by with_index
flintsones.each_with_object({}).with_index do |(element, hash), index|
	hash[name] = index
end

```

## Practice Problem 2

Add up all of the ages from the Munster family hash

```ruby
ages = { "Herman" => 32, "Lily" => 30, "Grandpa" => 5843, "Eddie" => 10, "Marilyn" => 22, "Spot" => 237 }

total_ages = 0
ages.each do |_, value|
	total_ages += value
end
total_ages #=> 6174 
```

Assign a variable for the total ages `ages_total` and set to `0` 

Iterate through the hash with `each` and add each value in turn to the total

### Other Solution

```ruby
ages.values.inject(:+) #=> 6174
```

`ages.values` returns an array of the values, then use the `inject` method which is part of the `Enumerable` module

### `inject` method

acts the same as the `reduce` method - takes a range of numbers, passes each element and accumulate each sequentially

- takes first element in collection and uses it as base sum
- takes next element and adds them together
- method then assigns that result to sum and adds in the nex element
- continues until all elements have been passed through the block

```ruby
[3, 6, 10, 13].inject(:+) => (((3 + 6) + 10) + 13) => 32

[3, 6, 10].inject { |sum, number| sum + number } => |3, 6| 3 + 6 => 9

```

## Practice Problem 3

Remove the people with age 100 and greater

```ruby
ages = { "Herman" => 32, "Lily" => 30, "Grandpa" => 402, "Eddie" => 10 }

ages.select! do |k, v|
	v < 100
end

ages.keep_if { |_, value| value < 100 }
```

Returns a new hash consisting of entries for which the block returns `true` 

`keep_if` deletes the values from the hash for which the block evaluates to `false` 

## Practice Problem 4

Pick out the minimum age from our current Munster family hash

```ruby
ages = { "Herman" => 32, "Lily" => 30, "Grandpa" => 5843, "Eddie" => 10, "Marilyn" => 22, "Spot" => 237 }

ages.values.min 

```

## Practice Problem 5

Find the **index** of the first name that starts with “Be”

```ruby
flintstones = %w(Fred Barney Wilma Betty BamBam Pebbles)

flintstones.index { |name| name[0, 2] == "Be" }
```

## Practice Problem 6

Amend this array so that the names are all shortened to just the first 3 characters

```ruby
flintstones = %w(Fred Barney Wilma Betty BamBam Pebbles)

# ! modifies the original collection, does not return a new
flintstones.map! do |name|
	name[0, 3]
end
```

## Practice Problem 7

Create a hash that expressed the frequency with which each letter occurs in this string

```ruby
statement = "The Flintstones Rock"

result = {}
letters = ('A'..'Z').to_a + ('a'..'z').to_a

letters.each do |letter|
	letter_frequency = statement.count(letter)
	result[letter] = letter_frequency if letter_frequency > 0
end

{ "F"=>1, "R"=>1, "T"=>1, "c"=>1, "e"=>2, ... }

```

## Practice Problem 8

What happens when we modify an array while we are iterating over it?

```ruby
numbers = [1, 2, 3, 4]
numbers.each do |number|
  p number
  numbers.shift(1) # removes the second element at index 1
end

# 1 
# 3
```

```ruby
numbers.each_with_index do |number, index|
	p "#{index} #{numbers.inspect} #{number}"
	numbers.shift(1)
end
```

## Practice Problem 9

```ruby
words = "the flintstones rock"

write own version of `titleize`

words.split.map { |word| word.capitalize }.join(" ")

```

## Practice Problem 10

Modify the hash such that each member of the Munster family has n additional age_group key

```ruby
munsters = {
  "Herman" => { "age" => 32, "gender" => "male" },
  "Lily" => { "age" => 30, "gender" => "female" },
  "Grandpa" => { "age" => 402, "gender" => "male" },
  "Eddie" => { "age" => 10, "gender" => "male" },
  "Marilyn" => { "age" => 23, "gender" => "female"}
}

munsters.each do |name, details|
	case details["age"]
	when 0..18
		details["age_group"] = "kid"
	when 18..65
		details["age_group"] = "adult"
	else
		details["age_group"] = "senior"
	end
end

{ "Herman" => { "age" => 32, "gender" => "male", "age_group" => "adult" },
  "Lily" => {"age" => 30, "gender" => "female", "age_group" => "adult" },
  "Grandpa" => { "age" => 402, "gender" => "male", "age_group" => "senior" },
  "Eddie" => { "age" => 10, "gender" => "male", "age_group" => "kid" },
  "Marilyn" => { "age" => 23, "gender" => "female", "age_group" => "adult" } }
```