# Variables

**Variables** are used to store information to be referenced and manipulated in a computer program - act like containers that label and store data in computer memory

- point to values in memory and are not deeply linked to each each

  ```ruby
  a = 4 # a points to value 4 in memory
  b = a # b points to value 4
  a = 7 # a is reassigned and points to a new value
  b => 4
  ```

## Getting Data

`gets` method stands for "get string"

	1. waits for user to type in information
	1. Press enter key and value entered is returned to the caller

```ruby
name = gets # type in Bob
=> "Bob\n"
name = gets.chomp => "Bob"
```

- the `\n` represents the enter key, can use `chomp` chained to `gets` to remove that new line character



## Types of Variables

- Constants - declared by capitalizing every letter in variable name, used to store data that never needs to change in the program
- global - declared starting variable name with `$` - available throughout the entire program, overriding all scope boundaries 
- class - declared by starting variable name with `@@` - accessible by instances of your class as well as class itself
  - used to declare a variable that is related to a class, but each instance does not need its own value
- instance - declared with `@` - available throughout the current instance of the parent class 
- Local - most common variable and obey all scope boundaries 

## Variable Scope

- determines where in a program a variable is available to use - defined by where the variable is created/defined

- scope is defined by a **method definition or block** 

  - block is a piece of code delimited by `{}` or `do/end` and followed by a method invocation

- methods have self-contained scope - none of the variables initialized by the method are available outside the method body

- **Inner scope can access variables initialized in an outer scope, but not vice versa**

  

  

  

  