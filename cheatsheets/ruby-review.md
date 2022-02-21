# Ruby Review

[TOC]

# Basics

Ruby is a object-oriented language, which means that everything in Ruby is an object. The four basic data types of Ruby: numbers (integers and floats), strings (sequence of characters), symbols, and Booleans (`true`, `false`, and `nil` )

## Numbers

Ruby has all the typical math operators

```ruby
# Addition
1 + 1 #=> 2

# Subtraction
2 - 1 #=> 1

# Multiplication
2 * 2 #=> 4

# Division
10 / 5 #=> 2

# Exponent
2 ** 2 #=> 4
3 ** 4 #=> 81

# Modulus (find the remainder)
8 % 2 #=> 0, no remainder ( 8 / 2 #=> 4)
10 % 4 #=> 2
```

**Integers and Floats**

There are two main types of numbers in Ruby. **Integers** are whole numbers such as 10. Floats are numbers that contain one decimal point, such as 10.5 or 0.45.

Need to keep in mind that when doing calculations with two integers in Ruby, *the result will always be an integer*

```ruby
17 / 5 #=> 3 not 3.4
```

To obtain a more accurate answer just replace one of the integers in the expression with a float

```ruby
17 / 5.0 # => 3.4
```

### Converting Number Types

Ruby makes it easy to convert floats to integers and vice versa

```ruby
# convert an integer to a float
20.to_f #=> 20.0

# convert float to integer: removes decimal places
15.9.to_i #=> 15
15.0.to_i #=> 15
```

When ruby converts a float to an integer, the decimal places are simply cut off. Ruby doesn't do any rounding during this conversion. 

### Number Methods

They are many built in Ruby methods to use on numbers:

`even? odd?`  - instance methods called on numbers, returns a boolean value

```ruby
6.even? #=> true
7.even? #=> false

10.odd? #=> false
13.odd? #=> true
```

## Strings

Strings are a sequence of characters wrapped in quotation marks, single or double. They represent text in data. 

**Double and Single quotation marks**

Strings can be formed with eithere double `""` or single `''` quotation marks, also known as *string literal*. This all becomes important when dealing with string interpolation and the escape characters. If need to use on type of quatotion mark inside the string itself can either use an escape character `\` or use the other quatation marks to wrap the entire string.

```ruby
"hello there 'bob'" # used single quotations inside double
'hello there \'bob\'' # used escape character
```

Escape characteres allow you to type in representations of whitespace characters and to include quotation marks inside your string without accidently throwing an arrow - prematurely ending your string. 

```
\\ # Add a backslash in your string
\b # Backspace
\r # Carriage return
\n # Newline
\s # Space
\t # Tab
\" # Double quotation mark
\' # Single quotation mark
```

### Concatenation

They are many ways to join strings together in Ruby

```ruby
# plus operator
"Welcome " + "to " + "Ruby" #=> Welcome to the RUby Tutorial!

# shovel operator
"Welcome " << "to " << "Ruby"

# concat method
"Welcome ".concat("to ").concat("Ruby!")
```

### Substrings

You can access the characters inside the string by using `String#[index]` method. This uses the index position of a character to retrieve that character from the string. Also can use the `String#slice[]` method to remove a substring from a string. 

- `[0..1]` - slice a string between the index positions listed, inclusive
- `[0, 4]` - the first value indicates the index position, second value equals number of characters to remove
- `[-1]` - removes last character in the string

```ruby
"hello"[0] #=> "h"
"hello"[0..1] #=> he
"hello"[0, 4] #=> "hell"
"hello"[-1] #=> "o"
```

### Interpolation

String interpolations allow you to evaluate a string that contains placeholder variables or Ruby expressions. The evaluated value of the Ruby expression or variable is then converted into a string. 

String interpolation only works on a double-quoted string. Within the string we use the interpolation marker `#{}`. Inside those brackets we can put any variables or Ruby code which will  be evaluated, converted to a string, and output in that spot of the  outer string. Our previous example could be rewritten like this:

```ruby
name = "Maisy"

# need to use double quotes for it to work
puts "Hello, #{name}!" #=> "Hello, Maisy!"
```

### String Methods

There are many useful string methods in Ruby. You can easily capitalize a word, reverse a string, and match patterns using regex. You can find all String methods on the [Ruby docs](https://ruby-doc.org/core-3.0.3/String.html). Always good to check the documentation first to see if there is a method that does something for you rather than implementing your own method.

- add `!` to end of method call to mutate the caller for most of these methods

`#capitalize` - capitalizes the first character in the string, does not modify the original, returns a copy 

```ruby
"hello".capitalize
#=> "Hello"
```

`#include?` - takes a substring as an argument, returns a boolean if the substring is in the string it is called on

```ruby
"hello".include?("lo")
#=> true
```

`#upcase`- converts all characters in a string to uppercase, does not modify the original, returns a copy

```ruby
"hello".upcase
#=> "HELLO"

name = "Mary"
name.upcase!
puts name #=> "MARY"
```

`#downcase` - converts all characters to lowercase, does not modify the original

```ruby
"HEllo".downcase #=> "hello"
```

`#empty?` - returns true if the string that is called on is an empty string

```ruby
"hello".empty? #=> false
"".empty? #=> true
```

`#length` - returns the number of characters in a string, also can use `size`

```ruby
"hello".length
#=> 5
```

`#reverse` - returns a reverse copy of the string

```ruby
name = "mary"
name.reverse #=> "yram"
puts name #=> "mary"

name.reverse!
```

`#split` - divides a string into substrings based on a delimeter, returning an array of these substrings

```ruby
"hello world".split # no delimiter given - splits at whitespace
#=> ['hello', 'world']

"hello".split("") # returns an array of characters
#=> ["h", "e", "l", "l", "o"]
```

`#char` - returns an array of characters in a string

```ruby
"hello".chars
#=> 
```

`#strip` - returns a copy of the receiveer with leading and trailing whitespace removed

```ruby
" hello, world ".strip 
#=> "hello, world"
```

`#index` - returns the integer index of the first occurence of a given substring or `nil` if not found

```ruby
'hello'.index('h') #=> 0
'hello'.index('lo') #=> 3
'hello'.index('oo') #=> nil
```

#### Converting other objects to strings

Use `to_s` method to convert pretty much anything to a string

```ruby
5.to_s #=> "5"
nil.to_s #=> ""
:symbol.to_s #=> "symbol"
```

## Symbols

Strings can be mutated/changed, so every time a string is used, Ruby has to store it in memory even if an existing string with the same value already exists. Symbols, on the other hand, are stored in memory only once, making them faster in certain situations. 

Symbols are preferred over strings as keys in **hashes**

#### Create a Symbol

To create a symbol, simply put a `:` colon at the beginning of some text:

```ruby
:my_symbol
```

`#object_id` method returns an integer identifier for an object. 

- strings of the same value will have different integer indetifiers because they are stored in different locations in memory. every time an instance of a string is made, Ruby will store the string object in memory. Variables holding the string objects will point to this location in memory
- :symbols are only stored once in memory so all symbols of the same name will have the same object identifier

```ruby
"string" == "string" #=> true
"string".object_id == "string".object_id #=> false

:symbol.object_id == :symbol.object_id #=> true
```

## Booleans

Booleans are important to help build conditional logic in programming. Booleans just represent yes or no, on or off with `true` or `false`

`nil` - represents nothing. Everything in Ruby has a return value. When an expressions or block of code doesn't have anything to return, it will use nil. 

```ruby
puts "hello there"
'hello there'
#=> nil

'hello'.nil? #=> false
nil.nil? #=> true
```

# Input and Output Data

Need to be able to **output** data to the screen and get **input** from a user. 

## Output Commands

To output information to the console, such as into your irb or REPL environment or into the command line, can use the `print` command. Can test any of this in the `irb` to see what is being printed and what is being returned by the method. 

```ruby
irb(main):001:0> print "Learning Ruby is fun!"
Learning Ruby is fun!=> nil

irb(main):002:0> print "1234"
1234=> nil
```

Can also use the `puts` command

```ruby
irb(main):001:0> print "Learning Ruby is fun!"
Learning Ruby is fun!
=> nil

irb(main):002:0> print "1234"
1234
=> nil
```

As you can see there is a small difference between the two: `puts` appends a new line to the argument passed in, whereas `print` keeps things all on one line. After printing whatever argument they are passed both return `nil` 

`puts` attempts to convert everything into a string by calling `to_s`. This is importatn if you are trying to use `puts` on an array that contains `nil values` since it will return some blank lines

```ruby
puts [1, nil, nil, 2]
1

2
```

- `puts` and `print` will convert the values to strings even if it means printing an empty string

Can debug output to see what data structure a variable contains by using `p` - shows a more raw version of an object.  `p` also returns the object that you give it as an argument 

```ruby
puts [1, 2, 3]
1
2
3
=> nil
p [1, 2, 3]
[1, 2, 3]
=> [1, 2, 3]
```



## Getting Data from User

One way to get information from the user is to call `gets` method - stands for "get string". The program waits for the user to type in information and then press the enter key. `gets` returns the user response as a string, can then store in a variable to use later. 

```ruby
name = gets
Mary
=> "Mary\n"
```

The `\n` at the end is the newline characters and represents the enter key. Can use the `chomp` method chained to `gets` to get rid of that - can put `.chomp` after any string to remove the carriage return characters at the end

```ruby
name = gets.chomp
Mary
=> "Mary"
```



# Variables

**Variables** are used to store information to be referenced and manipulated in a computer program. They act as a container that stores data and provides a way of labeling/naming data with a descriptive name. 

- **Containers that hold information** 
- label and store data in memory
- Reference/point to the location of the object in memory 
- First declare a variable and use the assignment operator to initialize it with a value

## Declaring a Variable

```ruby
age = 30
age = 30 + 5 # reassign value

age = 45
# => 45
```

Variable names are reusable so you can assign a new value to a variable at any point. It will override the original value. 

There will be times where you want to perform an operation on the original value of a variable and then reassign the result of the operation to the same variable.

```ruby
age = 18
age = age + 4
age #=> 22
```

There is a nice shorthand assignment operator to accomplish this `+=`. There are similar assignment operators for all the common math operators.

```ruby
age = 18
age += 4

payment = 100
payment *= 2 # => 200

temperature = 40
temperature /= 10
```

## Variable Scope

A variables scope determines where in a program a variable is available for use. The scope is defined by where the variable is initialized or created. In Ruby, variable scope is defined by a **method definition** or by a **block**

Methods are pieces of reusable code that you can name and use that name to execute the method. A method definition looks like this:

```ruby
name = "Larry David"

# define the method
def display_name(first_name, last_name)
  name = first_name + ' ' + last_name
  puts name
end

# call the method
display_name("John", "Smith")
```

Methods have **self-contained scope** - variables initialized within the method's body can be referenced or modified from within the method body. The variables initialized in a method's body are not available outside the method's body. Therefore names initialized outside the method body cannot be accessed inside the method. Inside `display_name` method a different `name` variable is created that is locally scoped to the method. You can pass data into a method from outside using arguments. If inside the method a destructive method is used on the argument then the object that was passed in can be modified and the changes appear outside the method. 

A block is a piece of code that follows a method's invocation, delimited by `{}` or `do/end` 

```ruby
total = 0
[1, 2, 3].each do { |num| total += num }
```

Blocks can access and modify variables that are defined outside the block. So the block following`Array#each` method is able to access and modify the total variable. In this case `total` is reassigned to a new object upon each iteration. 

Not all `do/end` pairs imply a block - those following a `loop` or a `for` loop is not considered a block in Ruby. They do not create their own inner scope instead they have the same scope as the outer. 

> Inner scope can access variables initalized in an outer scope, but not vice versa

```ruby
a = 5 # variable initalized in outer scope

3.times do |n| # method invocation followed by a code block
  a = 3 # reassign to a new object
end

5.times do |n|
  a = 3
  b = 5
end

puts a # => 3
puts b # => Error - undefined local variable
```

- the **block** does have access to variable `a` outside its inner scope and therefore is able to modify it
- in this case `a` is reassigned to a new object - points to a new location in memory
- variable `b` is initialized in the inner scope of the block and therefore cannot be accessed outside the block

## Variable Types

There are **five** types of variables - constants, global variables, class variables, instance variables, and local variables. 

- **Constants** - declared by capitalizing every letter in the variable name, used to store data that never needs to be changed. Ruby will allow you to change it but it does throw out a warning 

- Global Variables - declared by starting the variable name with the `$`, available throughout the entire app override all scope boundaries (don't use them)

- **Class Variables** - declared by starting name with two `@` signs, accessible by instances of the class as well as the class itself. Used when you need to declare a variable for a class but each instance of the class does not need its own value for the vairable. Must be initialized at class level 

- **Instance Variables** - declared by starting the variable name with one `@` sign. Available thorughout the current instance of the parent class. 

- **Local Variables** - most common, obey all scope boundaries

  ```ruby
  MAX_SCORE = 5 # available throughout the program, even in method definitions
  $var = "available throughout the program"
  @@instances = 0
  @var = "available throughout the current instance of the class"
  ```

# Blocks

Blocks are a powerful concept used frequently in Ruby. Think of them as a way of bundling up a set of instructions or code that performs a specific task. 

```ruby
5.times do 
  puts "hello world"
end
```

The block starts with the keyword `do` and ends with keyword `end`. The `do/end` style of a block is used when the code block has multiple lines. 

**Bracket Blocks** 

When a block contains just a single instruction, use the alternate markers `{}` to begin and end the block

```ruby
5.times { puts "Hello world"}
```

## Blocks Are Passed to Methods

Blocks are normally a paramter passed into a method call. `do/end` and `{}` following a method invocation are known as blocks in Ruby. 

For instance, `5.times` takes a block as a parameter. There are *many* methods that accept blocks. 

## Block Parameters

Often the instructions within the block need to reference the value they are currently working with. When we write a block can specify the block parameter inside pipe characters.

- `times` method block parameter will put in the current iteration of the block run
- `gsub` passes in the string that it found, uses the result of the block as the replacement for the original match
- `each` passes in the current element of the iteration, iterates through each element of the array and passes the element as a parameter to the block

```ruby
5.times do |i|
  puts "#{i} Hello world"
end

"this is a sentence".gsub("e") { |letter| letter.upcase }

[1, 2, 3].each do |num|
  puts "#{num}"
end
```

# Conditional Logic

Controlling the flow of data in your code is an important concept in coding. You have some code that you only want to execute under specific conditions so you need a way for the computer to check whether these conditions have been met or not. Any conditional statement will always have an expression that evaluates to `true` or `false`. Based on this answer, the computer will decide whether or not to execute the code that follows. If it's `true` then the code will be processed; while if its false the code will be skipped and not run. You can also provide some code to run instead. 

## Truthy and Falsy

Conditional statements check expressions for a true or false value, so you need to first understand what Ruby considers to be true or false. In Ruby it is very simple: the only false values are `nil` and `false`. That's it! Everything else is considered true. Even an empty string`""` , the interger `0` are considered true objects in Ruby. 

## Basic Conditional Statement

The simplest way to control the flow of your code is by using conditionals with the `if` statement

```ruby
if statement_to_be_evaluated == true
  # do something
end

if 1 < 2
  puts "Thats great!"
end
```

Since there is only one line of code to be executed if the expression evaluates to true, you can rewrite this code on one line:

```ruby
puts "That's great!" if 1 < 2
```

The statement to be evaluated can be anything that returns true or false. It could be a mathematical expression, a variable value, or a call to a method. 

### Adding `else` and `elsif`

If you want to run some code if the condition is false then you can use an `if...else` statement

```ruby
age = 22

if age >= 21
  puts "That's great, you can drink!"
else
  puts "Not going to work"
end
```

What if we want to check multiple conditions to see if any of them are true then need to use `elsif` clause

```ruby
age = 18

if age >= 21
  puts "That's great, you can drink!"
elsif age == 18
  puts "Too young, but officially an adult"
else
  puts "Not going to work"
end
```

## Boolean Logic

To determine whether an expression evaluates to `true` or `false` you will need to use a comparison operator. Think of**comparison operators** as the building blocks to construct the conditional statements.

`==` equality returns `true` if the values compared are equal (compares value and data type)

```ruby
5 == 5 # => true
5 == 7 # => false
```

!= (not equal) returns `true` if the values compared are not equal

```ruby
5 != 7 #=> true
5 != 5 #=> false
```

`>` greater than returns `true` if the value/operand on the left is larger than the operand on the right

```ruby
7 > 5 # => true
```

`<` less than returns `true` if the value/operand on the left is smaller than the operand on the right

```ruby
5 < 7 # => true
```

`>=` greater or equal to returns `true` if the value on the left is larger than or equal to the value on the right

```ruby
7 >= 7 #=> true
8 >= 7 #=> true
```

`<=` less than or equal to returns true if the value on the left of the operator is smaller than or equal to the value on the right

```ruby
5 <= 5 #=> true
```

`#eql?` checks both the value type and the actual value it holds

```ruby
5.eql?(5.0) # false
5.eql?(5) # true
```

`#equal?` checks whether both values are the exact same object in memory. Variables act as references to values in memory - so they point to the location of the value in memory. If two variables point to the same location then this would return `true`

```ruby
a = 5
b = 5
a.equal?(b) # => true
```

This expression is true because of the way computers store integers in memory. both variables point to the same location in memory - have the same `object_id`. Although two different named variables are holding the number 5, they point to the same object in memory. 

```ruby
a = "hello"
b = "hello"
a.equal?(b) # false
```

This happens because computers can't store strings in the same way they store integers. Although the value of the variables are the same, the computer created two separate string objects in memory. The same is true for complex data structures such as arrays: both variables hold the same array object but point to different locations in memory since the computer created two separate array objects in memory

```ruby
irb(main):008:0> a = [1, 2, 4]
irb(main):009:0> b = [1, 2, 4]
irb(main):010:0> a.object_id
=> 180
irb(main):011:0> b.object_id
=> 200
irb(main):012:0>
```

Ruby also has the **spaceship operator** `<=>` - this returns one of three numerical values:

- `-1` if the value on the left is less than the value on the right
- `0` if the values are equal
- `1` if the value on the left is greater than the value on the right

This operator is used in sorting functions and methods, which will be covered later. 

## Logical Operators

Sometimes you want to write an expression that contains more than one conditions. Can accomplish this by using logical operators which are `&&` (and), `||` (or), and `!` (Not)

The `&&` operator returns `true` if **both** the left and right expressions return `true`

```ruby
if 1 < 2 && 5 < 6
  puts "That is correct"
end
```

Expressions are always evaluated from left to right. In Ruby **short-circuiting** can happen where in the case of `&&` the left expression evaluates to `false` then the second expression is not even evaluated. To Ruby it's pointless to evaluate the second half as the overall expression can never return `true` 

With the `||` operator, only one expression needs to evaluate to true for the whole statement to return `true` 

If the first expression evaluates to `true` then the second expression is never checked because the complete expression is already `true` and the code block is run.

```ruby
if 10 < 2 || 5 < 6 
  puts "This is true"
end
```

Finally, the `!` operator reverses the logic of the expression - so if the expression returns `false` using the `!` Operator makes the expression `true` and the code inside the block will be run

```ruby
if !false #=> true
if !(10 < 5) # => true
```

## Case Statements

Case statements are a clearer way of writing several conditional expressions that would normally result in a long and messy `if...elsif` statement. You can even assign the return value from a case statement to a variable for later use. 

Case statements process each condition in turn, if the condition returns `false` it will move onto the next one until a match is found. An `else` clause can be provided to serve as a default if no matches are found.

```ruby
grade = 'C'

number_grade = case grade
  when 'A' then 90
 	when 'B' then 80
 	when 'C' then 70
  when 'D' then 60
  when 'F' then 50
  else "You shall not pass!"
  end
    
number_grade #=> 70
```

Once a match is found the value of that match is returned, and the case statement stops execution. 

If you need something more complex then just a return value, you can remove the `then` keyword and instead place code to be executed on the next line

```ruby
grade = "F"

case grade
  when 'A'
  	puts "You are a genius"
  	num_grade = 99
 	when 'D'
  	puts "Need to put in more work"
  	num_grade = 60
	else
  	puts "You shall not pass!"
end
  
```

## Unless 

`unless` statements work in the opposite way as an `if` statement: it only processes the code in the block if the expression evaluates to `false`. So it will jump into the code UNLESS the statement is `true` 

```ruby
age = 18
unless age < 17
  puts "Get a job"
end
```

You should use `unless` when you want to **not** do something if the condition is true

## Ternary Operator

This is a one line `if..else` statement that can make your code much more concise. 

`conditional statement ? <execute if true> : <execute if false>`

```ruby
age = 18
response = age < 17 ? "Enjoy your youth!" : "you are an adult"
puts response #=> "you are an adult"
```

Since the expression evaluated to `false` the code after the `:` was assigned to the variable `response` 

# Loops

Loops in Ruby are blocks of code that are continually executed until a certain condition is met, or you `break` out of the loop. Loops come in handy when you have to perform a task over and over again, instead of repeating writing the code where you have a greater chance of introducing bugs into the program you can just insert the code into a loop. 

Use loops when you find yourself needing to repeat an action more than once in your code.

The `loop` will keep going unless you specifically request for it to stop, using the `break`command. Normally `break` is compared with a condition that if evaluated to `true` will break out of the loop.

```ruby
counter = 0

loop do
  puts "iteration is on #{counter}"
  counter += 1 # increment the counter variable
  break if counter == 10
end
```

This type of loop is good to use when you are asking the user if they want to continue or play a game again. You can continue asking the user for their answer and break out of the loop if they enter the correct response. For example:

```ruby
answer = nil
loop do
  prompt "Would you like to continue (y/n)"
  answer = gets.chomp.downcase
  break if answer.starts_with?('y')
  prompt "Please enter a valid choice"
end
```

## While Loop

`while` loop is similar to a `loop` except that you declare the condition that will break out of the loop at the beginning. 

# Arrays

An array is a collection of ordered data. 

An **array** is a number-indexed list. Can access the elements in an array by using its index value. An array allows you to create and manipulate an **ordered and indexed collection of data.** The individual data in an array are known as **elements**. An array can contain any combination of variables, numbers, strings, or other objects (including other arrays).

## Creating Arrays

```ruby
numbers = [1, 2, 3, 4]
strings = ["This", "is", "a", "sentence"]
```

Both arrays have five elemetns separated by commas - the first array contains integers while the second contains strings. 

Arrays are commonly created with an **array literal** which is simply a special syntax used to create an instance of an array object. To create a new array using an array literal use square brackets `[]`

An array can also be created by calling `Array.new` method. Can take two optional arguments (initial size and default value)

```ruby
Array.new # => []
Array.new(3) # => [nil, nil, nil]
Array.new(3, 7) # => [7, 7, 7]
Array.new(3, true) #=> [true, true, true]
```

## Accessing Elements

Every element in an array has an **index** which is a numerical representation of the element's position in the array. Like most other programming languages, Ruby arrays use **zero-based indexing** which means that the index of the first element is 0, the index of the second element is 1, and so on. Accessing a specific element within an array is as simple as calling `#Array[x]` where `x` is the index of the element you want. Calling an invalid position will result in `nil`. 

Ruby also allows the use of negative indices, which return elements starting at the *end* of the an array, starting at `[-1]`

```ruby
str = ["This", "is", "a", "small", "array"]

str[0] # => "This"
str[1] # => "is"
str[4] # => "array"
str[-1] # => "array"
```

Ruby provides the `first` and `last` array methods which return either the first or last element in the array. These methods can also take an integer argument `#Array.first(n)` which will return a new array that contain the first or last `n` elements of the Array it was called on. Calling these methods without the argument just returns the element itself.

```ruby
str = ["This", "is", "a", "small", "array"]

str.first # => "This"
str.first(2) # => ["This", "is"]
str.last(2) # => ["small", "array"]
```

## Adding and Removing Elements

Adding an element to an existing array is as simple as using `push` method or the shovel operator `<<`. Both methods will add elements to the end of an array and return that array with the new elements. The `pop` method will remove the element at the end of an array and return the element that was removed. All these methods **mutate the caller*** and are **destructive methods**

```ruby
numbers = [1, 2]

numbers.push(3, 4) # => [1, 2, 3, 4]
numbers << 5 # => [1, 2, 3, 4, 5]

numbers.pop # => 5
numbers # => [1, 2, 3, 4]
```

The methods `shift` and `unshift` are used to add and remove elements at the beginning of an array. The `unshift` method adds elements at the beginning of an array and returns that modified array (similar to `push`). The `shift` method removes the first element of an array and returns that element (like `pop`)

```ruby
numbers = [2, 3, 4]
numbers.unshift(1) # => [1, 2, 3, 4]
numbers.shift #=> 1
numbers # => [2, 3, 4]
```

Both `pop` and `shift` can also take integer arguments:

```ruby
numbers = [1, 2, 3, 4, 5, 6]

numbers.pop(2) #=> [5, 6]
numbers.shift(3) # => [1, 2, 3]
```

## Adding and Subtracting Arrays

Concatenating two arrays together joins the arrays into one new array. Adding two arrays will return a new array built by concatenating them, similar to string concatenation. Can also use the `concat` method

```ruby
a = [1, 2, 3]
b = [4, 5, 6]

a + b  # => [1, 2, 3, 4, 5, 6]
a.concat(b) # => [1, 2, 3, 4, 5, 6]
```

Can find the difference between two arrays, by using subtraction. This method returns the copy of the first array, removing any elements that appear in the second array.

```ruby
[1, 1, 2, 1, 2, 2, 3, 4] - [1, 4] # => [2, 2, 2, 3]
```

## Multidemnsional Arrays

An array can be composed of other arrays

```ruby
users = [ [1, 'Jack'], [2, 'Betty'] ]
```

To access the first element from the first sub array you can use the `Array#[]` method

```ruby
users[0, 0] # => 1
```

To convert a multidimensional array into a regular array use `flatten` method

```ruby
users.flatten # [1, 'Jack', 2, 'Betty']
```



## Basic Methods

### Iterate Over Arrays

Most of these methods take a block as an argument, code in the block is executed upon each iteration. The method sends the value of the current element to the block in the form of an argument

`each` - iterates through each element of an array and calls a code block on each element, returns the original collection

```ruby
users = ["mary", "linda", "danny", "joe"]
users.each { |item| puts item }
```

`map` - takes a block as an argument: iterates through each element in an array, passes the current element as a parameter to the code block, uses the return value of the block to create a new array with modified elements

- `map!` method will modify the original array directly
- considers the return value of the block
- uses the return value of the block to perform **transformation** 

```ruby
users = users.map { |user| user.capitalize }
users = users.map(&:capitalize)
```

`select` - iterates over an array, passes the current element to the code block, uses the truthiness of the return value of the code block to decide if that element is added to a new array. Only returns elements to a new array if the return value of the code block is truthy. 

```ruby
numbers = [3, 7, 12, 2, 49]
numbers.select { |n| n > 10 }
# => [12, 49]
```

- evaluates the return value of the block
- performs selection based on the truthiness of the block's return value. When an element is selected, its placed in a new collection

# Hashes



## Enumerable Methods

`Enumerable#any?` - looks at the truthiness of the blocks return value in order to determine the methods return value

- if the block returns truthy for any element in the collection, the method will return true

```ruby
[1, 2, 3].any? do |num|
  num > 2
end # => true

{ a: "ant", b: "bear", c: "cat" }.any? do |key, value|
  value.size > 4
end # => false
```

`Enumerable#all?` - looks at truthiness of block's return value but only returns true if the block's return value is **every** iteration is true

```ruby
[1, 2, 3].all? do |num|
	num > 2
end
# => false

{ a: "ant", b: "bear", c: "cat" }.all? do |key, value|
  value.length >= 3
end
# => true
```

`Enumerable#each_with_index` - takes both the value and the index as parameters to the block 

```ruby
users.each_with_index |item idx|
  puts "#{item} with index #{idx}"
end
```

`Enumerable#each_with_object` - takes a method argument that is a **collection object** as well as a code block as an argument. The collection object will be returned by the method. The block itself takes 2 arguments: first represents the current element, second represents the collection object that was passesd in as an argument to the method 

```ruby
[1, 2, 3].each_with_object([]) do |num, array|
  array << num if num.odd?
end
# => [1, 3]

{ a: "ant", b: "bear", c: "cat" }.each_with_object([]) do |pair, array|
  array << pair.last
end
# => ["ant", "bear", "cat"]

{ a: "ant", b: "bear", c: "cat" }.each_with_object({}) do |(key, value), hash|
  hash[value] = key
end
# => { "ant" => :a, "bear" => :b, "cat" => :c }
```

# Sort

