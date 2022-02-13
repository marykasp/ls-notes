# Lesson 2



## Ruby Style

**Parentheses**

- when a method is invoked `()` are optional - without them it makes it difficult to differentiate between a method call and local variable. For example, if you type `puts` it is a method invocation but without knowing that it is a method you wouldn't know. 

**puts and gets**

- use `puts` method to display something. When you want to ask the user for some input, use the `gets`method. Can call those methods with their module: `Kernel.puts()` or `Kernel.gets()` - shows that they are **module methods** in the `Kernel` module
  - **all methods come from somewhere - subclass -> parent of subclass**

## Truthiness

**Boolean** is an object whose only purpose is to convey whether its true or false - helps us build *conditional logic* and understand the **state** of an object or expression. 

Booleans are an instance of an object/class so can call instance methods on booleans

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

Expressions in conditional statements like `if/else` must evaluate to a boolean object

Using a method call as a conditional expression you will want the method to return a boolean rather than relying on the truthiness or falsiness of a return value

```ruby
num = 5

if (num < 10)
  puts "small number" # this line will be executed 
else
  puts "large number"
end

puts "it's true!" if some_method_call
```

## Logical Operators

- `&&` and operator will return `true` only if both expressions evaluate to `true`
  - Ruby's order of precedence considers `>` operators higher precedence than `&&` 
  - can chain as many expressions together, evaluated from left to right
- `||` or operator will return `true` if either one of the expressions evaluate to `true` - both expressions must return `false` to evaluate to `false` 
- **Short Circuiting** - it will stop evaluating expressions once it guarantees the return value
  - `&&` will short circuit when it encounters the first `false` expression
  - `||` will short circuit when it encounters the first `true` expression 

### Truthiness

Ruby considers everything to be truthy other than `false` and `nil` - can use any expression in a conditional as long as it doesn't evaluate to `false` or `nil` 

```ruby
name = find_name

# checks if name is not nil if it is short cicuiting will happen and ruby won't even check the second operand
if name && name.valid? 
  puts "great name!"
else
  puts "either couldn't find name or it's invalid"
end
```

## rbenv

Ruby package manager - intercepts Ruby commands using shim exectubales injected into your `PATH` variable - determmines which Ruby version to use and passes Ruby commands to that version

```bash
~/.rbenv/shims:/usr/local/bin:/usr/bin:/bin
~/.rbenv/versions # where all ruby versions are stored
```

**shims** lightweight executables that pass your command along to rbenv - reads from `RBENV_VERSION` environment variable, the first`.ruby-version` file found by searching directories, then the global `~/.rbenv/version` file

```bash
# list latest stable versions:
rbenv install -l 
# list all local versions
rbenv install -L
# install a ruby version
rbenv install 2.0.0

# list of all versions known to rbenv
rbenv versions, shows asterik next to currently active version
```

Sets a local application-specific Ruby version by writing the version name to a `.ruby-version` file in the current directory - overrides the global version 

```bash
rbenv loval 2.7.1
```

## Flowchart

Using a flowchart helps map out the logical sequence of a possible solution to a problem<img src="//d1b1wr57ag5rdp.cloudfront.net/images/flowchart_components.jpg" width="300" height="400">

##### flowchart for finding largest number in a collection<img src="//d1b1wr57ag5rdp.cloudfront.net/images/flowchart_example2-20210504.jpeg" width="450" height="750">



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

## Variable Scope

##### Blocks

`do..end` and `{}` following a method invocation (instance method that is called on an object, like `each`), **block** is the argument passed to the method

```ruby
[1, 2, 3].each do |num|
  puts num
end
```

- outerscope variables can be accessed by inner scope

  - `blocks` can access variables outside their scope

- inner scope variables cannot be accessed in outer scope 

- peer scopes do not conflict - peer blocks cannot reference variables initialized in other blocks

- **variable shadowing** - when code blocks take in a parameter, if there was an outer scoped variable with the same name, this would prevent access to outer scoped variable and making changes to that outer scoped variable

  ```ruby
  
  n = 10
  1.times do |n|
    n = 11
  end
  
  puts n          # => 10
  ```

##### Method Definitions

- method cannot access variables initialized outside of the block - scope is self contained 
- can only access variables that were initialilzed inside the method or that are defined as parameters
- can pass in outside data through the argument when the function is called - how pieces of data outside are passed into method definitions
- **blocks within method definitions**  - rules of scope for a method invocation inside a method defintion remain

##### Constants

Constant variables have different scope rules in relation to **blocks** and methods

- method defintions can access global constants
- constants can also be accessed by blocks following a method invocation 

**Method definition** define a Ruby method using `def` keyword

```ruby
def greeting
  puts 'Hello'
end
```

**Method invocation** when we call a method, whether that is an exisiting method like an *instance method* called on an instance of an object or a custom method we have defined 

- block acts as an argument to the method invocation 

```ruby
greeting # calling the defined method
[1, 2, 3].each do |num| # method invocation followed by a block 
  puts num
end
```

##### Method parameter not used

```ruby
def greetings(str)
  puts "Goodbye"
end

word = "Hello"
greetings(word)

# Outputs 'Goodbye'
```

##### Method parameter used

- method can access the string `hello` from the outer scope since it is passed in as an argument in the form of the parameter (local variable) `word` 

```ruby
def greetings(str) 
  puts str
  puts "Goodbye"
end

word = "Hello"

greetings(word)

# Outputs 'Hello'
# Outputs 'Goodbye'
```

##### Block not executed

```ruby
def greetings
  puts "Goodbye"
end

word = "Hello"

greetings do
  puts word
end

# Outputs 'Goodbye'
```

the `greetings` method is invoked with a a block but the method s not defined to use the block

##### Block executed

```ruby
def greetings
  yield
  puts "Goodbye"
end

word = "Hello"

greetings do
  puts word
end

# Outputs 'Hello'
# Outputs 'Goodbye'
```

- `yield` keyword controls the interaction with the block - so the block following the method invocation is executed once
- blocks and methods can interact with each other - level of interaction is set by the method definition and used at the method invocation 

```ruby
a = "hello"

[1, 2, 3].map { |num| a } # => ["hello", "hello", "hello"]
```

- The `map` method doesn't have direct access to the `a` variable - the block that we pass to `map` does have access to `a` - so the block can use that value to determine the transformation value for each array element 

1. **method definition** sets the scope for any local variable in terms of the parameters it has, what it does with those parameters, and how it interacts with a block
2. **method invocation** uses the scope set by the method definition (when you pass a block to a defined method, if `yield` keyword is inside the defintion then that code block will be executed, that code block can have access to variables in the outer scope)
   1. if method is defined to use a block, then the scope of the block can provide more flexibility in how the method interacts with its surrounds 

- **Method definition *sets* a scope for local variables in terms of parameters and interaction with blocks**
- **Method invocation *uses* the scope set by the method definition**

## Pass by Reference vs. Pass by Value

What happens to objects that are passed into methods? 

- arguments as **references** to the original object
- arguments as **values** copies of the original

##### Pass by "value"

- **copy of the original object** - operations performed on the object within the method have no effect on the original object outside of the method

  -  main scope variable is not accessible to the method
  - reassignment does not affect the original object

  ```ruby
  def change_name(name)
    name = 'bob'      # does this reassignment change the object outside the method?
  end
  
  name = 'jim'
  change_name(name)
  puts name           # => jim
  ```

##### Pass by reference

- not all operations affect the object the same
- reassignment does not affect the original object, but methods like `.capitalize`!  mutate the original object it is called on

##### when an operation within the method mutates the caller, it will affect the original object

- some destructive methods end with a `!` 

### Medium Article on Ruby Objects

Strings and other collection classes are similar in the way they behave (mutable unlike Booleans and Numbers in Ruby):

- **Variables reference the collection, collection contains references to the actual objects in the collection** 
  - when working with objects that support **Indexed assignment** (arrays `#array[]`, setter method will mutate the array) the **collection element** is being reassigned to a new object not the entire collection itself

When you pass an object as an argument to a method - the method can either mutate the object or leave it unchanged. It depends on:

- what type of object is being passed in 
- how the argument is passed to the method
- what operations are acting on the object inside the method

#### Mental Model for object passing in Ruby:

1. immutable objects (numbers and booleans) act like Ruby passes them around by value
2. mutable objects can always be mutated just by calling one of their mutating methods 
   - pass by reference - means a reference of the object is passed around so variables inside the method are bound to the original object 

Ruby variables are merely references to objects in memory 

assignment to a variable merely changes the binding - the object the variable originally referenced is not mutated. A new object is now bound to the variable with a new`#object_id` 

```ruby
a = 'hello'
a.object_id # returns the object id of the string literal 'hello'
```

##### Setters are Mutating

- setter methods (similar to indexed assignemnt) are methods that are defined to mutate the *state of an object* 

  - `something = value` look like assignments

  - indexed assignment the collection elements (elements in a list, characters in a String) are replaced or bound to a new object but not the entire collection itself

  - **setters** the state of the object is altrered - mutating or reassigning an instance variable

    - ```ruby
      person.name = "bill"
      person.age = 23
      ```

    - these are setter calls that mutate the object bound to person 

Ruby has methods that mutate its arguments - would seem that Ruby must be pass by reference in some circumstances. Arguments passed by value (or a copy) cannot be mutated - so Ruby must pass by reference when its methods can mutate its arguments

- `!` Methods mutate their called, indexed assignments, and setter methods also mutate 
- assignment and assignment operators (`=, *=, -=`) are always non-mutating
- immutable objects still seem to be passed by value
- mutable objects seem to be passed by reference 
- assignment can break the binding between an argument name and the object it references. Parameter now points to a different location in memory with assignment operations

#### Collections (Arrays, Hashes)

**Objects can be mutated, references are immutable**. So Ruby is a pass by reference by value,meaning it passes copies of the reference. 
