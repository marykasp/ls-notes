# Methods

**Method** a group of code statements that perform a specific task, can call the method for the code block to be executed

```ruby
def say
  	# method body
end

say() # call/invoke a method, pass arguments in the ()
```

- **parameters** act as placeholders the the data (arguments) that are passed into the method during the method call, placeholders for data outside the method defintion 
- **method invocation** means calling a method
- **arguments** the data that is sent to the method invocation to be modified, used, or returned by the method, pass arugments to a method

## Default Parameters

- method invocation will work even if no arguments are passed in since the method definition defines a default parameter to use

  ```ruby
  def say(words='hello')
    puts words + '.'
  end
  
  say() => 'hello.'
  ```

## Method Scope

- a method defintion creates its own scope outside the regular flow of execution - local variables inside a method cannot be referenced outside of the method definiton 
- methods cannot access data outside of the method defintion unless the data is passed in as an argument

```ruby
# method invocation with a block
[1, 2, 3].each do |num|
  puts num
end

# method defintion - method only defined not invoked
def print_num(num)
  puts num
end
```

## `obj.method or method(obj)`

`some_method(obj)` format is when you send arguments to a method call - `obj` is the argument being passed to the method call

`a_caller.some_method(obj)` format is when some method modifies a caller, instance of a class has access to the instance methods of that class, the method is invoked with this format (dot notation)

## Mutating the Caller

- when the caller is altered permanently by a method called on it

- method defintions cannot modify arguments passed to them - method parameters are scoped at the method definition level (objects can be mutated)

  ```ruby
  def some_method(number)
    number = 7 # reassign argument, only available inside this method defintion
  end
  
  a = 5 # global variable
  some_method(a) # value of a is assigned to the local variable number, scoped at the method defintion level
  
  # a's value will not be affected by the method call
  puts a => 5
  
  # mutating the caller inside a method defintion
  def mutate(array)
    array.pop # pop method mutates the caller
  end
  
  b = [1, 2, 3]
  p b => [1, 2, 3]
  p mutate(b) => 3 # will print out value returned by the method, since pop returns the last element in the array to the caller and this is the last line in the mutate method, 3 will be returned
  p b => [1, 2]
  
  ```

## puts vs. return

- every method returns the evaluated result of the **last line executed** unless an explicit return comes before it

- `return` keyword lets you explicitly return a value 

  ```ruby
  def add_three(number)
    return number + 3
    number + 4 # this line will not be run
  end
  
  returned_value = add_three(4)
  ```

## Chaining Methods

- Since every method call returns something, can chain methods together

- if last line in method uses `puts` method that returns `nil` need to end method with the value you want returned or use `return` keyword

  ```ruby
  def add_three(n)
    n + 3
  end
  
  add_three(5).times { puts "this should print 8 times" }
  "Hi there".length.to_s # converts the length of that string to a string value
  ```

## Method Call as Arguments

- can pass a method call which returns a value as an argument to another method, the **returned value** is what is being passed as the argument

## Call Stack

- helps Ruby keep track of what method is executing as well as where execution should resume when it returns to the caller
- **stack frame** represents the global (top-level) portion of the program. `main` method is the initial stack frame
- when it reaches a method invocation it updates the `main` stack frame with the current program location, which it will use later to determine where execution should resume
- then a new stack frame will be created for the method called and places it on top of the stack - new frame is `pushed` onto the stack
- when a method is done executing it **pops** the top frame from the call stack 