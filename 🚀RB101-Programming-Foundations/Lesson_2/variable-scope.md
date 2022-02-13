# Variable Scope

### Blocks

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
    

### Method Definitions

- method cannot access variables initialized outside of the block - scope is self contained
- can only access variables that were initialilzed inside the method or that are defined as parameters
- can pass in outside data through the argument when the function is called - how pieces of data outside are passed into method definitions
- **blocks within method definitions** - rules of scope for a method invocation inside a method defintion remain

### Constants

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

### Method parameter not used

```ruby
def greetings(str)  
	puts "Goodbye"
end

word = "Hello"
greetings(word)# Outputs 'Goodbye'
```

### Method parameter used

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

### Block not executed

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

### Block executed

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

- The `map` method doesn’t have direct access to the `a` variable - the block that we pass to `map` does have access to `a` - so the block can use that value to determine the transformation value for each array element
1. **method definition** sets the scope for any local variable in terms of the parameters it has, what it does with those parameters, and how it interacts with a block
2. **method invocation** uses the scope set by the method definition (when you pass a block to a defined method, if `yield` keyword is inside the defintion then that code block will be executed, that code block can have access to variables in the outer scope)
    1. if method is defined to use a block, then the scope of the block can provide more flexibility in how the method interacts with its surrounds
- **Method definition *sets* a scope for local variables in terms of parameters and interaction with blocks**
- **Method invocation *uses* the scope set by the method definition**