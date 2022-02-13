# Introduction to PEDAC

```ruby

```

A problem solving approach to coding: lets you solve complex problems efficiently 

**`P`** - [Understand the] **Problem**

`**E**`  - **Examples** / Test Cases

`**D` - Data Structure**

`**A**` - Algorithm

`**C**` - Code

### `P` - [Understand the] Problem

Understanding the problem has three steps: 

1. Read the problem description
2. Check the test cases if any
3. If any part of the problem is unclear; ask the interviewer or problem requester to clarify the matter

- Need to write down what the **inputs and outputs for the problem** are.
- Should also describe the rules that you must follow. The rules should encapsulate all the explicit and implicit requirements in the problem.
- Identify what the explicit requirements are, write them down, and repeat the process for the implicit requirements.
- Should also ask the interviewer if not explicitly stated if you are returning the same object or an entirely new one? So are you modifying the object or not?

<aside>
💡 **Example Problem:** Given a string, write a method `change_me` which returns the same string but with all the words in it that are palindromes uppercases

</aside>

```ruby
# input: string
# output: string (not the same object)
# rules:
#      Explicit requirements:
#        - every palindrome in the string must be converted to
#          uppercase. (Reminder: a palindrome is a word that reads
#          the same forwards and backward).
#        - Palindromes are case sensitive ("Dad" is not a palindrome, but "dad" is.)

#      Implicit requirements: things that are implied 
#        - the returned string shouldn't be the same string object.
#        - if the string is an empty string, the result should be an empty
#          string
```

### `E` - Examples / Test Cases

Think of potential examples and test cases: think of the potential input and what should be the expected output 

```ruby
change_me("my mom and dad are amazing!") # => "my MOM and DAD are amazing!"
```

### `D` - Data Structure

Should one use an array or a hash?

Start writing your pseudo-code

```ruby
input: string, array, hash, etc.
ouput: string, array, hash, etc.
rules: explain the rules that must be followed, both explicit and implicit.
```

### `A` - Algorithm

Use pseudo-code: outline the logic of the code with possible variable names. Break up the code into separate logical pieces - the separate logical bits can be written as individual methods

### `C` Code

Write the code

<aside>
💡 Example: Given a string, write a method `palindrome_substrings` which returns all the substrings from a given string which are palindromes. Consider palindrome words case sensitive

</aside>

```markdown
# input: string
# output: array of substrings

# rules:
	# Explicit requirements:
	- every palindrome substring (word same backwards as is forward) in the string must be returned
	- palindromes are case sensitive ("Mom" is not a palindrome since there is not all lowercase)

	# Implicit requirements:
	- the returned value should be a list of the substrings not a string
	- empty strings should return an empty array
	- strings without palindromes should return an empty array

```

Could split the string into an array of words and then loop through that array, use an array method that returns a new array that meets the requirements of the problem

```markdown
# Algorithm 
- initialize a result variable to an empty array
- create an array named substring_arr that contains all of the substrings of the input string 
are at least 2 characters long `substring` method
- loop through the words in the substring_arr array
- if the word is a palindrome, append it to the result array
- return the result array

# isPalindrome method
- insside is_palindrome check whether the string value is equal to its reversed value. 
#string.reverse method
```

Algorithm for the subprocess of finding substrings inside a string

```markdown
# Substring method
- create an empty array called result that will contain all required substrings
- create a `starting_index` variable (value of `0`) for the starting index of a substring
- start a loop that iterates over `starting_index` from `0` to the length of the string minus 2
-- the last letter in a string is not long enough to create a substring (characters >= 2)
	# inner loop
	- create a `num_chars` variable (value of `2`) for the length of the substring
	- start an inner loop that iterates over `num_chars` from 2 to `string.length - starting_index`
		- extract a substring of length `num_chars` from `string` starting at `starting_index`
		- append the extracted substring to the `result` array
		- increment the `num_chars` variable by 1
	- end the inner loop
	- increment the `starting_index` by 1
- end the outer loop
- return the `result` array
```

Formal Pseudo-code

```markdown
# Start
/* Given a string name `string` */

SET result = []
SET starting_index = 0

WHILE starting_index <= length of string - 2
	SET num_chars = 2
	WHILE num_chars <= length of string - starting_index 
		SET substring = num_chars characters from string starting at index starting_index append
		substring to result array 
		SET num_chars += 1

	SET starting_index += 1

Return result

# End
```

```ruby
def substrings(str)
	result = []
	starting_index = 0
	
	while starting_index <= str.length - 2
		num_chars = 2
		while (num_chars <= str.length - starting_index)
			substring = str.slice(starting_index, num_chars)
			result << substring
			num_chars += 1
		end
		starting_index += 1
	end
	return result
end
```

```ruby
def is_palindrome?(str)
	return str == str.reverse
end
```

```ruby
def palindrome_substring(string)
	result = []
	substring_arr = substrings(string)
	
	substring_arr.each do |substring|
		result << substring if is_palindrome?(substring) 
	end
	result
end
```

**Complete pseudocode:**

```ruby
# input: a string
# output: an array of substrings
# rules: palindrome words should be case sensitive, meaning "abBA"
#        is not a palindrome

# Algorithm:
#  substrings method
#  =================
#    - create an empty array called `result` that will contain all required substrings
#    - create a `starting_index` variable (value `0`) for the starting index of a substring
#    - start a loop that iterates over `starting_index` from `0` to the length of the string minus 2
#      - create a `num_chars` variable (value `2`) for the length of a substring
#      - start an inner loop that iterates over `num_chars` from `2` to `string.length - starting_index`
#        - extract a substring of length `num_chars` from `string` starting at `starting_index`
#        - append the extracted substring to the `result` array
#        - increment the `num_chars` variable by `1`
#      - end the inner loop
#      - increment the `starting_index` variable by `1`
#    - end the outer loop
#    - return the `result` array

#  is_palindrome? method
#  =====================
# - Inside the `is_palindrome?` method, check whether the string
#   value is equal to its reversed value. You can use the
#   String#reverse method.

#  palindrome_substrings method
#  ============================
#  - initialize a result variable to an empty array
#  - create an array named substring_arr that contains all of the
#    substrings of the input string that are at least 2 characters long.
#  - loop through the words in the substring_arr array.
#  - if the word is a palindrome, append it to the result
#    array
#  - return the result array
```