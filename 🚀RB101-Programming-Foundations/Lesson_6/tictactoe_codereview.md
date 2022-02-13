Hi Mary,

I'll be reviewing your code today.  **Sarah N Bunker(TA)**

# **Question**

I understand your question as, "What can you use to determine when to stop extracting and wrapping logic into helper methods?" One way is using what we learned earlier. Back in lesson 2 we learned about pseudo-code, where we describe what we want the code to do and then we can write the actual code to do that. We also learned about flowcharts where we capture main things the program needs to do in a logic flow. When I am writing my main loop I want it to read almost like pseudo-code where my method names are describing the main logic blocks if it were in a flow chart. Another good tool to help is rubocop which has a metric for complexity of a function. If this starts showing an offense on any function then you should consider refactoring that function or loop.

# **User Experience/Gameplay**

- I like the option to get help instead of forcing the rules on every user
- I also like the info on how the board is numbered.
- I like that the person who goes first can be random instead of forcing them to pick, but I think I would only do this for the first time and then alternate until someone is the ultimate winner.
- I don't like how an invalid choice at the beginning shows the entire intro message.
- Screen clears worked well.
- I like how the error for an invalid choice shows the correct options I can choose from.

# **Rubocop**

- No offenses detected. Great Job.

# **Source Code**

- Some messages in the yaml file and some at the top of the code.
- Main game loop is very clean and the succinct.
- `#computer_offense` and `#computer_defense` have repeating code. Is there a way you could extract this into another method?
- The other methods are clearly named.

# **Overall Thoughts**

Interacting with this game was easy because the prompts were clear such as an error message for an invalid input showing the correct options. I also like that the help option shows how the board is numbered. Some areas for improvement are fixing what is repeated when the user inputs something other then `help` or `Enter` at the beginning, and I would also consider changing how who play first is chosen throughout the game.

Connected to your question above, on the main game loop I think you did a great job extracting the logic to other methods. And I think those other methods have clear names that describe the purpose of the methods. Some messages are in a yaml file and some are at the top of the main program file. I would like you to consider the tradeoffs of each location because both have pros and cons. I like the choice to keep things such as the markers, winning number, and max score as constants at the top so they are easier to change later. I encourage you to look at the code in `#computer_offense` and `#computer_defense`for ways to refactor and extract common code to another method. Great job coding this game.

I hope this is helpful. Have fun working on the ideas for improvement. Please let me know if you have any questions!