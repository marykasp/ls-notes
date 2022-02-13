# Loops

**Loops** is a repetitive execution of a piece of code for a given number of repetitions or until a certian condition is met

##	`loop`

`loop` method takes a block and will execute any code in that block until you manually intervene or insert a `break` statement inside the block - can result in an infinite loop

```ruby
loop do
  puts "This wil keep printing until you hit Crtl + c"
end
```

## Control Loop Execution

`break` keyword allows you to exit a loop at any point, so any code after will not be executed, will exit the loop

```ruby
i = 0
loop do
  i += 2
  puts i
  if i == 10
    break # once i is equal to 10 the loop will stop running
  end
end
```

`next` skips the rest of the current iteration and starts executing the next iteration

```ruby
i = 0
loop do
  i += 2
  if i == 4 
    next  # skip rest of code in this iteration, so 4 will not be printed to the screen
  end
  puts i
  if == 10
    break
  end
end
```

```ruby
x = 42
loop do
  puts x   # Prints 42 -- x is in scope inside the block
  x = 2    # We can even change the value of x
  break
end
puts x     # 2 -- the value was changed
```

`loop` blocks introduce a new scope but they still have access to any variables that were initialized from outside of the block

## `while` loops

**while loop** is given a parameter that evaluates as either true or false, once the expression becomes false the while loop stops executing

- does NOT have its own scope, the entire body of the loop is in the same scope as the code that contains the while loop

  ```ruby
  x = 0
  while x < 5
    y = x * x
    x += 1
  end
  
  puts y # 16, can have access to the variables created inside a while loop since they do not have block scope variables
  ```

## `until` loops

opposite of the while loop - phrase the problem in a different way - `until` loop is not a method so they do NOT have their own scope

```ruby
x = gets.chomp.to_i

until x < 0
  puts x
  x -= 1
end

puts "Done!"
```

## `do/while` loops

**do/while loop** works in a similar way to while loop but the code within the loop gets executed one time prior to the conditional check

- conditional check is placed at end of loop
- no built in `do/while` loop like JS, have to use `loop` and `break` 

## `for` loop

**for loops** are used to loop over a collection of elements 

- returns the collection of elements after it executes

```ruby
x = gets.chomp.to_i

for i in 1..x do  # 1..x is a range and the .. indicates the last number is includedx
  puts x - i
end
```

## Iterators

**Iterators** are methods that naturally loop over a given set of data and allow you to operate on each element in the collection

- `each` method loops through each element in the array, then it executes the code in the block with that element as the argument
- `{}` when the code can be contained to one line
- `do/end` block when performing multi-line operations

```ruby
names = ["bob", "joe", "steve", "janice"]
names.each { |name| puts name }

x = 1
names.each do |name|
  puts "#{x}. #{name}"
  x += 1
end 
```

## Recursion

**Recursion** is another way to create a loop - its the act of calling a method from within itself

```ruby
def doubler(start)
  puts start
  if start < 10
    doubler(start * 2) # calls itself within the method
  end
end 
```

![Fibonacci Diagram](https://d2aw5xe2jldque.cloudfront.net/books/ruby/images/fibonacci_diagram.jpg)