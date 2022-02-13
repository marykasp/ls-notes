# Basics

## Literal

**Literal** any notation that lets you represent a fixed value in source code

```ruby
'Hello world' # string literal
375 # integer literal
3.14 # float literal
true # boolean literal
{ 'a' => 1, 'b' => 2 } # hash literal
[1, 2, 3] # array literal
:symb # ruby literal
nil # nil literal
```

## Strings

**String** is a sequence of characters wrapped in quotations - text data

- `\` escape character tells computer that the quotes that follow are not meant as syntax 
- **string interpolation** - merges ruby code with strings `#{ruby expression}` the returned expression value will be concatenated with the string

## Symbols

**symbols** are created by placing a `:` colon before a word - used when you want to reference something like a string but don't ever intend to print it to the screen or change it

- Immutable (unchangeable) string - `:name, :a_symbol` 

## Numbers

**numbers** are represented as an **integer** - whole number or a **float** which is a decimal number

## nil	

`nil` represents nothing, or being completely empty - where output is expected but nothing is returned to the caller

- `.nil?`  checks if the caller is nil - returns a boolean value
- in an expression `nil` will be treated as false - represents the absence of content
- `false == nil` returns false - both are treated as negative when evaluated in an expression, but are not equivalent

# Operations

```ruby
1 + 1 # addition
4 - 2 # subtraction
4 * 4 # multiplication
16 / 4 # division
16 % 4 # modulo operator - left value is the dividend, right is the modulus
```

#### Modulo vs. Remainder

`%` modulus computes and returns the remainder but has different rules than the remainder method

- first operand - dividend
- second operand - modulus

`#remainder` method computes and returns the remainder of an integer division operation

```ruby
16.remainder(5) => 1
```

`#divmod` method computes both the integer result of the division and its modulo value

```ruby
16.divmod(5) => \[3, 1\]
```

|  a   |  b   | a % b (modulo) | a.remainder(b) | a.divmod(b) |
| :--: | :--: | :------------: | :------------: | :---------: |
|  17  |  5   |       2        |       2        |   [3, 2]    |
|  17  |  -5  |       -3       |       2        |  [-4, -3]   |
| -17  |  5   |       3        |       -2       |   [-4, 3]   |
| -17  |  -5  |       -2       |       -2       |   [3, -2]   |

```ruby
15.0 / 4 => 3.75 # when you use a float,Ruby returns a float
```

#### Equality comparison

`==` compares operand on left with the operand on the right and returns a boolean value

#### String concatenation

`+` operator to join strings together

```ruby
'foo' + 'foo' => "foofoo"
'one' + 1 => TypeError: no implicit conversion of Integer into a String
```

## Type Conversion

- convert a `String` to a `Integer` with `to_i` 

  ```ruby
  '12'.to_i => 12
  '4 hi there'.to_f => 4.0 # method that converts to a float, number has to be the first character in a string if not will return 0.0
  1.to_s => '1'
  ```

## Data Structures

### Arrays

**array** used to organize information into an **ordered list** - can be made up of any data type `[]` 

```ruby
[1, 2, 3, 4, 5][0] => 1
```

- each element in an array can be accessed by its **index position** - all arrays are zero indexed

### Hashes

**hash** or a **dictionary** is a collection of key:value pairs - `{}` 

- key is represented by a symbol that points to a value (`=>`)
- retrieve values by its key with square bracket notation

```ruby
{:dog => 'barks', :cat => 'meows', :pig => 'oinks'}[:cat] => "meows"
```

## Expressions and Return

- `=>` hash rocket

- **expression** is anything that can be evaluated - always returns something, even if its an error message or `nil` 

## puts vs. return

`puts` method prints something to the screen and returns `nil` 

```ruby
a = puts "stuff"  # returns nil
a => nil
```

