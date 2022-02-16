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