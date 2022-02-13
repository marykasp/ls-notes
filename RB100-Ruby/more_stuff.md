# More Stuff

## Regex

**regex** stands for **regular expression** - sequence of characters that form pattern matching rules and then is applied to a string to look for matches

- `/match/` and use `=~` operator to see if have a match 

  ```ruby
  "powerball" =~ /b/ # returns the index of where match is located => 5
  ```

  

- `match` method to perfom regex comparisons - uses `MatchData` objects that describes the match

  - called on regex itself

  ```ruby
  /b/.match("powerball") # MatchData "b"
  ```

## Standard Classes

- find libraries that help you solve a problem - like Ruby's `Math` module, `Time` class
- no need to reinvent the wheel when there is a rich resource to accomplish a task already built 
  - `Math.sqrt` is a class method not an instance method

## Variables as Pointers

- point to an **address space** in memory - variables don't actually contain the value, contains a pointer to a specific location in memory that contains the value
  - **some methods mutate the address space while others make the variable point to a different address space**
  - use variables to pass an argument to a method, we are assigning the value of the original variable to a variable inside the method
  - the operations that are performed inside the method determine if the original argument will change - `map` method does not mutate the caller, so will have no affect on the value of the variable passed in 

![Variables as Pointers 1](https://d2aw5xe2jldque.cloudfront.net/books/ruby/images/variables_pointers1.jpg)

## Blocks and Procs

- blocks can be passed into a method just like normal variables 

  ```ruby
  # passing_block.rb
  
  def take_block(number, &block)
    block.call(number)
  end
  
  number = 42
  # first takes a number as one paramter then does a block.call
  take_block(number) do |num|
    puts "Block being called in the method! #{num}"
  end
  ```

  

- **procs** are blocks wrapped in a proc object and stored in a variable

  ```ruby
  # can also take arguments
  talk = Proc.new do |name|
    puts "I am talking #{name}"
  end
  
  talk.call
  ```

  - procs can be passed into method

    ```ruby
    # method that takes a proc as its argument - passed in when call method
    def take_proc(proc)
      [1, 2, 3, 4, 5].each do |number| # iterate through an array inside the method, and call the proc on each element
        proc.call number
      end
    end
    
    proc = Proc.new do |number| # proc takes an argument
      puts "#{number}. Proc is being called!"
    end
      
    take_proc(proc)
    ```

    

## Exception Handling

- specific process that deals with errors in a managable and predictable way 

- `Exception` that uses `begin, rescue, end` to signify exception handling 

  ```ruby
  # exception_example.rb
  
  begin
    # perform some dangerous operation
  rescue
    # do this if operation fails
    # for example, log the error
  end
  ```

  - when an error is raised the `rescue` block will be executed then the program will continue as it normally would would not just stop

## Excpetions and Stack Traces

- an exception is raised means the code has encountered some sort of error condition \

  ```ruby
  greeting.rb:2:in `+': no implicit conversion of Integer into String (TypeError) from greeting.rb:2:in `greet'
  from greeting.rb:6:in `<main>'
  ```

  

- `def` statements - when Ruby encounters one it merely reads the function defintion in memory and saves it away to be executed later - body of the method isn't executed until the method is called 

  ```ruby
  def top
    bottom
  end
  
  def bottom
    puts "Reached the bottom"
  end
  
  top
  ```

  