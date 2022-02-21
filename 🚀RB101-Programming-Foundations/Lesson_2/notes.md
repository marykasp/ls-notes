# Lesson 2: Small Problems

Notes for Lesson 2 of Launch School's RB101 course

## Contents

- [Ruby Style](#ruby-style)
- [Truthiness](#truthiness)
- [Pseudocode](#pseudocode)
- [Flowcharts](#flowcharts)
- [Rubocop](#rubocop)
- [Debugging](#debugging)
- [Precedence](#precedence)
- [Coding Tips](#coding-tips)
- [Variable Scope](./variable-scope.md)
- [Pass By Reference](./pass-by-reference.md)

## Ruby Style

- Text editor should use two spaces for tabs and indenting should be set to use spaces

- `#` sign at the beginnning of a line signifies a comment - not executed by Ruby interpreter

- Use `snake_case` formatting to define or initialize a method, variable, or file name

  ```ruby
  # Naming a file
  this_is_a_snake_cased_file.rb
  
  # Assigning a variable
  forty_two = 42 # references an integer object
  
  # Define a method
  def this_method
    # code
  end
  ```

- Define a **constant variable** ( all uppercase ) when value will not change

  ```ruby
  FOUR = "four"
  FIVE = 5
  ```

- Prefer `{}` over `do/end` block when the entire code expression fits on one line

```ruby
[1, 2, 3].each { |i| puts i } # single line

[1, 2, 3].each do |num| # multiline
  num * 2
  puts num
end
```

- Use PascalCase when naming classes

  ```ruby
  class MyFirstClass
  end
  ```

## Truthiness

- ability to express "true" or "false" in a language 
- Helps build conditional logic and understand the state of an object or expression 
- **Boolean** is an object whose purpose is to express `true` or `false`
- Booleans are classes with associated methods - like Strings, Arrays, Hashes, Integers

```ruby
true.class # => TrueClass
true.nil? # => false
true.to_s # => "true"
true.methods # => returns a list of methods you can call on the true object

false.class # => FalseClass
false.nil? # => false
false.to_s # => "false"
false.methods # => list of methods
```

**Logical Operators** 

- `&&` and operator will return `true` only if both expressions evaluate to `true`
  - Ruby's order of precedence considers `>` operators higher precedence than `&&` 
  - can chain as many expressions together, evaluated from left to right
- `||` or operator will return `true` if either one of the expressions evaluate to `true` - both expressions must return `false` to evaluate to `false` 
- **Short Circuiting** - it will stop evaluating expressions once it guarantees the return value
  - `&&` will short circuit when it encounters the first `false` expression
  - `||` will short circuit when it encounters the first `true` expression 

Ruby considers everything to be truthy other than `false` and `nil` - can use any expression in a conditional as long as it doesn't evaluate to `false` or `nil` 

```ruby
name = find_name

if name && name.valid?
  puts "great name!"
else 
  puts "either couldn't find name or name is invalid"
end
```

## Pseudocode

- Pseudocode is used to load the problem into our brain.
- It's used to try to dissect, understand, and solve a problem.
- Helps focus on the logical problem and not the programming language.
- Formalizing pseudocode helps make translation to programming code easier.

| keyword             | meaning                              |
| ------------------- | ------------------------------------ |
| START               | start of the program                 |
| SET                 | sets a variable we can use for later |
| GET                 | retrieve input from user             |
| PRINT               | displays output to user              |
| READ                | retrieve value from variable         |
| IF / ELSE IF / ELSE | show conditional branches in logic   |
| WHILE               | show looping logic                   |
| END                 | end of the program                   |

- Pseudocode example:

```
START

# Given a collection of integers called "numbers"

SET iterator = 1
SET saved_number = value within numbers collection at space 1

WHILE iterator <= length of numbers
  SET current_number = value within numbers collection at space "iterator"
  IF saved_number >= current_number
    go to the next iteration
  ELSE
    saved_number = current_number

  iterator = iterator + 1

PRINT saved_number

END
```

```ruby
# while loop solution
def find_greatest(numbers)
  save_number = numbers[0]
  iterator = 1
  
  while iterator <= numbers.length
    current_number = numbers[iterator]
    if saved_number >= current_number
      next
    else
      saved_number = current_number
    end
    
    iterator += 1
  end
  saved_number
end
```

```ruby
# each method solution
def find_greatest(numbers)
  saved_number = numbers[0]
  
  numbers.each do |num|
    if saved_number >= num
      next
    else
      saved_number = num
    end
  end
  
  saved_number
end
```

- [pseudocode-practice.md](./pseudocode-practice.md)

## Flowchart

- **Flowchart** helps map out the logical sequence of a possible solution in a visual way.
- Flowchart components:
  - **Oval** start/end
  - **Rectangle** processing step
  - **Parallelogram** input/output
  - **Diamond** decision (two branches per diamond)
  - **Circle** connector
- Use an imperative approach when working with flowcharts.
- **Imperative** or **procedural** is step-by-step way of solving a problem.
- **Declarative** uses abstracted or encapsulated components of a language, such as `each`.
- Using pseudocode and flowcharts to help dissect the logic of a problem, requires trying to figure out how detailed to make the chart and pseudocode and what to extract to sub-processes.
- This is exactly what a programmer should be thinking about when designing a solution.
- Start at a high level, using declarative syntax, then drill down a level (sub-processes), using imperative pseudocode.

## RuboCop

- [RuboCop](https://rubocop.org/) is a static code analyzer.
- Rules are **cops**.
- Cops are grouped into **departments**.
- The two departments we care about are style formatting and code linting (syntax and logic).
- Recommend using `v0.86.0`.

### Installation and Usage

- Gemfile
- Install: `bundle install`
- Usage: `bundle exec rubocop file.rb`
- `.rubocop.yml`

## Debugging

- Debugging is arguably the most important skill a programmer needs to learn.
- Work to develop a systematic, patient temperament.

### Online Resources

1. Search engine
2. Stack Overflow
3. Documentation

### Steps to Debugging

1. Reproduce the error.
2. Determine the boundaries of the error.
3. Trace the code.
4. Understand the problem well.
5. Implement a fix.
   - Important: Fix one problem at a time.
6. Test the fix.

### Techniques for Debugging

1. Line by line (patient, systematic)
2. Rubber duck
3. Walk away
4. Use Pry
5. Use a debugger

## Precedence

**Operator Precedence** - set of rules that dictate how Ruby determines which **operands** each operator takes 

- **() parentheses** override the default evaluation order and have the highest possible precedence 
- operations involving operators with high precedence get evaluated before operations with low precedence 
- determines which operands get passed to each operator 
- operator with a higher precedence is said to **bind** more tightly to its operands

##### Evaluation Order

```ruby
3 ? 1 / 0 : 1 + 2  # raises error ZeroDivisionError
5 && 1 / 0         # raises error ZeroDivisionError
nil || 1 / 0       # raises error ZeroDivisionError

# 1/0 is not evaluated due to short circuiting
nil ? 1 / 0 : 1 + 2  # 3
nil && 1 / 0         # nil
5 || 1 / 0           # 5
```

##### In depth

```ruby
array = [1, 2, 3]

array.map { |num| num + 1 }     # => [2, 3, 4]
p array.map { |num| num + 1 }     # outputs [2, 3, 4]

array.map do |num|
  num + 1
end                                 #   => [2, 3, 4]

p array.map do |num|
  num + 1                   #  outputs #<Enumerator: [1, 2, 3]:map>
end                           #  => #<Enumerator: [1, 2, 3]:map>
```

- The return value of `map` that gets passed to `p` as an argument which outputs `[2,3,4]` 
- blocks have the lowest precedence of all operators `{}` has higher precedence then `do..end` - has an effect on which method call the block gets passed to
  - `array.map` gets bound to `p` which first invokes `array.map` returning an Enumerator object, the Enumerator is then passed to `p` along with the block. `p` prints the Enumerator but doesn't do anything with the block 
  - the **binding of an argument to a method and the method name** (`p` and the return value of `array.map` ) is slightly tigher than the binding between the method call and a `do..end` block
  - `{}` has a higher priority so it binds more tightly to `array.map`, so the block is called and the return value gets passed to `p` 

##### Ruby's `tap` method

Object instance method `tap` - passes the calling object into a block then returns that object 

```ruby
mapped_array = array.map { |num| num + 1 }
mapped_array.tap { |value| p value } => [2, 3, 4]
```

- `[2, 3, 4]` new array gets returned and saved to `mapped_array` which then gets used to call `tap`
- `tap` takes the calling object and passes it to the **block argument**, then returns the same object 
- will normally print the object inside that block 

## Coding Tips

##### Naming Things

- choose descriptve variable and method names
- variables are named for what they actually store - capture the intent of the variable
- use `snake_case` when naming except classes are in `CamelCase` or constants in all uppercase

##### Mutating Constants

```ruby
CARDS = [1, 2, 3]
```

- do NOT add or remove values from a constsant list
- `CONSTANTS` are immutable

##### Methods

- make sure a method's task performs one thing - should be short around 10 lines or so 
- determine if method should return a value with no side effects or perform side effects with no return value 
  - `!` methods ending with this normally indicate the method has side effects 
- returning a value is implied with a method so never name a method that begins with `return` 
- should be able to extract the method from a larger problem and work with the method in isolation 

- method names should reflect mutation - `update_total`, expect the parameter passed into it will be mutated
- `print_`, `say_`, `display_` name methods with these terms that only output values to the screen (don't mutate parameters or return values)

