# Flow Control

**conditional flow** where data in a program takes the right path

## Conditionals

- conditional tells data where to go based on some defined parameters 

- `if` statements and comparison operators - always return a boolean

  ```ruby
  puts "Puts in a number "
  a = gets.chomp.to_i
  
  if a == 3
    puts "a is 3"
  elsif a == 4
    puts "a is 4"
  else
    puts "a is neither"
  end
  
  puts "x is 3" if x == 3
  
  # using then keyword
  if x == 3 then puts "x is 3" end
  ```

- `unless` acts as the opposite of `if` 

  ```ruby
  puts "x is not 3" unless x == 3
  ```

- `==` compares the operands to see if they are equal in value and type
- `!=` not equal operator checks to see if the values are not equal to each other
- when comparing strings the comparison is character by character 
- cannot use `<, >` with values of different types returns and ArgumentError

## Logical Operators

1. `&&` and operator, expressions to the left and to the right have to **both** be true for the entire expression to be true
2. `||` or operator, either expression has to be true for the entire expression to be true
3. `!` not operator, changes that boolean value to its opposite

**order of precedence** when evaluating multiple expressions:

1. `<=, <, >, >=` comparison
2. `==, !=` equality
3. `&&` Logical AND
4. `||` Logical OR

## Ternary Operator

- turns an `if/else` statement into one line

```ruby
true ? "this is true" : "this is not true"
```

## Case Statement

- similar to an `if` statement with a different format

- First define a value then compare it against multiple different cases and once a match is found that case clause will run

  ```ruby
  a = 5
  
  # can store return value in a variable
  answer = case a
   when 5
    puts "a is 5"
   when 6
    puts "a is 6"
   else
    puts "a is neither"
  end
  
  puts answer
  ```

  

- **every expressionn evaluates as true when used in flow control, except for `false` and `nil` **

  