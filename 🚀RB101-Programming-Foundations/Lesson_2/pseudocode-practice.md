# Pseudocode

1. A method that returns the sum of two integers

   ```md
   START
   
   # Given two integers called num1 and num2
   
   num1 + num2
   
   END
   ```

   

2. A method that takes an array of strings and returns a string that is all those strings concatenated together

```md
START

# Given an array of string objects

SET iterator = 0
SET concatenated_string = empty string

WHILE iterator <= length of strings array
	current_string = string at current iterator location - iterator is the 		index position of the element
	concatenated_string += current_string
	
	iterator += 1
	
concatenated_string

END
```

3. A method that takes an array of integers and returns a new array with every other element

```md
START

# Given an array of integer objects

SET iterator = 0
SET new_arr = empty array []

WHILE iterator <= length of numbers array
	if iterator is odd
		new_arr += value at location of iterator of numbers array

new_arr 

END
```

