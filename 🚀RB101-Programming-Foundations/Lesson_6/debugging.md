# Debugging

Majority of a programmers time is spent on analyzing and understanding a problem, experimenting or coming up with an approach, or debugging bugs in the code

### Temperament

Need to have a patient and logical temperament to debug code - programming is dealing with a constant stream of broken things and learning to deal with those ill feelings 

### Reading Error Messages

**stack trace** is critical in helping you figure out where to start debugging the code - must *carefully* read through the stack trace 

### Online Resources

1. Search Engine: study error message and walk backwards through the code to understand how the flow of the program arrived at the error condition 
   - think about data that is being used at the point of error and how missing or incorrect data could have caused the probelm 
   - use a search engine to look up the error message `NoMethodError: undefined method 'name' for nil:NilClass`

2. [Stack Overflow](https://stackoverflow.com) - answers rank highly in search engines 
3. Documentation - consult the official Ruby documenation [Ruby Docs](http://ruby-doc.org)



## Steps to Debugging

1. Reproduce the Error- isolate the root cause and reproduce the error on your machine

2. Determine the Boundaries of the Error - tweak the data that caused the error

   - modify the data or code to get an idea of the scope of the error 

3. Trace the Code - trace the code backwards and can determine which method or line the bug in the code originates from

4. Understand the Problem Well - after narrowing the source of the problem to a subprocess or a line of code it's time to break down the code within that section 

5. Implement a Fix - multiple ways to solve the problem **fix one problem at at time - its common to notice additional edge cases or problems as your are implementing a fix but resist the urge to fix multiple problems at once**

6. Test the Fix - verify that the code fixed the problem by using a similar set of tests

   ## Techniques for Debugging

   1. Line by Line - read code line by line, word by word

   2. Rubber Duck - use some object as a sounding board when faced with a hard problem. When forced to explean the problem out loud you are forcing yourself to articulate the problem detail by detail - often leads to discovering the root of the problem 

      - focus your mind on walking through the code - noticing a small detail may reveal a deeper problem

   3. Walking Away - activate a different part of your brain, even when you walk away from your computer, your brain is still working on the problem in the background 

      - first load the problem into your brain
      - good to take a step back and come back with a refreshed brain

   4. Using Pry - `Pry` is a powerful Ruby REPL that can replace IRB

      ```ruby
      require "pry" # addd this at top of file to use Pry
      
      binding.pry # insert anywhere in code
      ```

      - when Ruby gets to the `binding.pry` line, execution will stop and we'll be able to inpsect the state of the program at that point 
      - stops execution and provides a prompt where we can type in an expression and see what the return value is
      - can also change variable values - helpful way to systematically step by stp debug our program without using `puts` throughout every subprocess 

   5. Using a Debugger - `Pry` can also be used as a real debugger - gives us mechanism to step into functions and walk over code

   

