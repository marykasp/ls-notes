# Pass By Reference Value

## Pass by Reference vs. Pass by Value

What happens to objects that are passed into methods?

- arguments as **references** to the original object
- arguments as **values** copies of the original

### Pass by “value”

- **copy of the original object** - operations performed on the object within the method have no effect on the original object outside of the method
    - main scope variable is not accessible to the method
    - reassignment does not affect the original object
    
    ```ruby
    def change_name(name)  
    	name = 'bob'      # does this reassignment change the object outside the method?
    end
    
    name = 'jim'
    change_name(name)
    puts name           # => jim
    ```
    

### Pass by reference

- not all operations affect the object the same
- reassignment does not affect the original object, but methods like `.capitalize`! mutate the original object it is called on

<aside>
🐁 when an operation within the method mutates the caller, it will affect the original object

</aside>

- some destructive methods end with a `!`

## Medium Article on Ruby Objects

[Variable References and Mutability of Ruby Objects](https://launchschool.medium.com/variable-references-and-mutability-of-ruby-objects-4046bd5b6717)

Strings and other collection classes are similar in the way they behave (mutable unlike Booleans and Numbers in Ruby):

<aside>
💡 **Variables reference the collection, collection contains references to the actual objects in the collection**

- when working with objects that support **Indexed assignment** (arrays `#array[]`, setter method will mutate the array) the **collection element** is being reassigned to a new object not the entire collection itself
</aside>

When you pass an object as an argument to a method - the method can either mutate the object or leave it unchanged. It depends on:

- what type of object is being passed in
- how the argument is passed to the method
- what operations are acting on the object inside the method

### Mental Model for object passing in Ruby:

1. immutable objects (numbers and booleans) act like Ruby passes them around by value
2. mutable objects can always be mutated just by calling one of their mutating methods
    - pass by reference - means a reference of the object is passed around so variables inside the method are bound to the original object

<aside>
🐁 **Ruby variables are merely references to objects in memory**

</aside>

assignment to a variable merely changes the binding - the object the variable originally referenced is not mutated. A new object is now bound to the variable with a new`#object_id`

```ruby
a = 'hello'
a.object_id # returns the object id of the string literal 'hello'
```

### Setters are Mutating

- setter methods (similar to indexed assignemnt) are methods that are defined to mutate the *state of an object*
    - `something = value` look like assignments
    - indexed assignment the collection elements (elements in a list, characters in a String) are replaced or bound to a new object but not the entire collection itself
    - **setters** the state of the object is altrered - mutating or reassigning an instance variable
        - `person.name = "bill"person.age = 23`
        - these are setter calls that mutate the object bound to person

Ruby has methods that mutate its arguments - would seem that Ruby must be pass by reference in some circumstances. Arguments passed by value (or a copy) cannot be mutated - so Ruby must pass by reference when its methods can mutate its arguments

- `!` Methods mutate their called, indexed assignments, and setter methods also mutate
- assignment and assignment operators (`=, *=, -=`) are always non-mutating
- immutable objects still seem to be passed by value
- mutable objects seem to be passed by reference
- assignment can break the binding between an argument name and the object it references. Parameter now points to a different location in memory with assignment operations

### Collections (Arrays, Hashes)

**Objects can be mutated, references are immutable**. So Ruby is a pass by reference by value, meaning it passes copies of the reference.

- collections contain references to each object that comprises the collection
- reassignment of an element changes that reference of that element not the entire collection - collection still points to the same location in memory

```ruby
a = [1, 2, 3]

a.object_id # 702405415151340

a[1].object_id # 11
a[1] = 9 # reassignment of an element within a collection
# the collection is mutated, the array still has the same location memory

a[1].object_id # 19, object ID changed
a.object_id # 702405415151340, object ID of array remained unchanged
```

## Summary

- pass by reference value, passes a copy of the reference as arguments to methods
- pass by reference is accurate so long as you account for assignment - changes where the argument variable is pointing to in memory leaving the original still pointing to same location & immutability - numbers and booleans cannot be mutated
- Ruby acts like pass by value for immutable objects, pass by reference for mutable objects (appears to act like), actually passes a copy of the reference (pointer) to the object’s location in memory
    - using methods that mutate the caller will modify the original object since the pointer is still the same
    - reassignment will bind the variable to a new object in memory, leaving the old pointer alone and unmodified