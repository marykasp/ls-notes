# Selection-Transformation

## Introduction

**Selection** - picking certain elements out of the collection depending on some criteria. Ex. pick all the odd integers from an array (`select)`. Returns the same number of elements in a collection or less.

**Transformation** - manipulate every element in the collection. Ex. increment all the elements of an array by 1. (`map`) Returns the same number of elements in the collection modified

Selection and transformation both utilize the basics of looping: `a loop, a counter, a way to retrieve the current value, and way to exit the loop`

### Selection Example

```ruby
alphabet = 'abcdefghijklmnopqrstuvwxyz'
selected_chars.= ''
counter = 0 # counter - track loop iteration/track current element on in collection

loop do # the loop
	current_char = alphabet[counter] # retrieve current value
	
	if current_char == 'g'
		selected_chars << current_char # append character to new collection if pass criteria
	end

	counter += 1
	break if counter == alphabet.size. # way to exit the loop
end
```

### Transformation Example

```ruby
fruits = ['apple', 'banana', 'pear']
transformed_elements = []
counter = 0

loop do
	current_element = fruits[counter]

	transformed_elements << current_element + "s". 
	# modified element then appended to a new array

	counter += 1
	break if counter == fruits.size
end
```

When performing a transformation it is important to pay attention to whether the original collection was mutated or if a new collection was returned (`map` method)

## Extracting to Method

### Selection

Example with hash. Want to select key-value pairs where the value is `Fruit`

```ruby
produce = {
  'apple' => 'Fruit',
  'carrot' => 'Vegetable',
  'pear' => 'Fruit',
  'broccoli' => 'Vegetable'
}

select_fruit(produce) # => {"apple"=>"Fruit", "pear"=>"Fruit"}

def select_fruit(produce_hash)
	produce_keys = produce_hash.keys
	counter = 0
	selected_fruits = {}

	loop do
		break if counter == produce.keys.size

		current_key = produce_keys[counter]
		current_value = produce_hash[current_key]

		if current_value == 'Fruit'
			selected_fruits[current_key] = current_value
		end
		counter += 1
	end

	# return the new selected fruits hash
	selected_fruits
end
```

- original hash is not mutated
- a new hash is returned by the method called `selected_fruits`

### Transformation

<aside>
💡 **Example:** Multiply each element in the collection by 2

</aside>

```ruby
numbers = [2, 3, 4, 5]

def double_numbers(numbers)
	counter = 0
	doubled_number = []

	loop do
		current_number = numbers[counter]
		doubled_number << current_number * 2
		
		counter += 1
		break if counter == numbers.size
	end
	doubled_number
end
```

- does not mutate the original array given to its argument
- returns a new array of the modified numbers

Transformations do not always have to be done to every element of the collection; they can also be performed on a subset of that collection

<aside>
💡 **Example**: only multiply 2 if the value is odd

</aside>

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7]

def double_odd_numbers(numbers)
	doubled_numbers = []
	counter = 0
	
	loop do
		break if counter == numbers.size
		
		current_num = numbers[counter]
		# reassignment - creates a whole new value in memory
		current_num *= 2 if current_num.odd?
		doubled_numbers << current_num

		counter += 1
	end
	doubled_numbers
end
```

- What if we wanted to transform the numbers based on their position in the array rather than their value

<aside>
💡 **Example:** only multiply by 2 if the value index is odd

</aside>

```ruby
def double_odd_indices(numbers)
	doubled_numbers = []
	counter = 0
	
	loop do
		break if counter == numbers.size

		current_num == numbers[counter]
		current_num *= 2 if counter.odd?
		doubled_numbers << current_num

		counter += 1
	end
	
	doubled_numbers
end
```

## More Flexible Methods

<aside>
💡 Example: `select_fruit` method that selects a certain produce out of a `produce_list` hash. We now wish to write a more generic `general_select` so we can specify whether we are interested in selecting fruits or vegetables

</aside>

```ruby
produce = {
  'apple' => 'Fruit',
  'carrot' => 'Vegetable',
  'pear' => 'Fruit',
  'broccoli' => 'Vegetable'
}

def general_select(produce_list, selection_criteria)
	produce_keys = produce_list.keys
	counter = 0
	selected_produce = {}
	
	loop do
		break if counter == produce_keys.size

		current_key = produce_keys[counter]
		current_value = produce_list[current_key]

		if current_value == selection_criteria
			selected_produce[current_key] = current_value
		end
		counter += 1
	end
	selected_produce # return a new hash
end

def general_produce_selection(produce_list, criteria)
	selected_produce = {}
	for key, value in produce_list
		puts "#{key} #{value}"
	end
end
```

By defining methods so that we can pass in additional arguments to alter the logic of the iteration, we can create more flexible and generic methods

<aside>
💡 `double_numbers` method to not only be able to double the values in an array, but to multiply by any number.

</aside>

```ruby
def multiply(numbers, multiple)
	multiplied_numbers = []
	counter = 0
	
	loop do
		break if counter == numbers.size
		current_num = numbers[counter]
		multiplied_numbers << current_num * multiple
		
		counter += 1
	end
	multiplied_numbers
end

my_numbers = [1, 4, 3, 7, 2, 6]
multiply(my_numbers, 3)
```

<aside>
💡 **Example:** Let's write a method called `select_letter`, that takes a string and returns a new string containing only the letter that we specified. We want it to behave like this:

</aside>

```ruby
question = 'How many times does a particular character appear in this sentence?'
select_letter(question, 'a') # => "aaaaaaaa"
select_letter(question, 't') # => "ttttt"
select_letter(question, 'z') # => ""

def select_letter(sentence, character)
	selected_char = ''
	counter = 0

	loop do
		break if counter == sentence.size
		current_char = sentence[counter]
		if current_char == character
      selected_char << current_char
    end
    counter += 1
	end

	selected_char
end
```

```ruby
def select_letter(sentence, character)
	selected_char = ''
	for char in sentence.chars
		if char == character
				selected_char < char
		end
	end
	selected_char
end
```