# Nested Data Structures

Collections can contain other collections

```ruby
arr = [[1, 3], [2]]
# nested array, array containing 2 separate arrays
# each inner array has its own index 
```

![Untitled](Nested%20Data%20Structures%2052523bbec4ae4e5a89f8af65bf8be87c/Untitled.png)

- Each inner array can be accessed by their index
- Can retrieve the elements that make up the inner array by their index

```ruby
arr[0] #=> [1, 3]
arr[0][1] #=> 3
arr[1] #=> [2]
arr[1][0] #=> 2
```

### Updating collection elements

Use `=` assignment operator to update the elements of a collection

- collections contain references to the objects that make up the collection

```ruby
arr[1] = "hi there'
arr # => [[1, 3], "hi there"]

arr[0][1] = 5
arr #=> [[1, 5], [2]]
```

- first part of chain is element reference, second part of chain `[1] = 5` is element update

```ruby
arr = [[1], [2]]
# element refernce - first array, append an integer to the array
arr[0] << 3
arr #=> [[1,3], [2]]
```

`arr[0] << 3` is a two part chain, `arr[0]` is element reference and returns `[1]` 

the second part `[1] << 3` destructively appends `3` into the inner array

```ruby
arr = [[1], [2]]

# appends an array into another array
arr[0] << [3]
# [[1, [3]], [2]]
arr[0] #=> [1, [3]]
```

Add another array inside a nested array - three-layer nested data structure 

### Other nested structures

Hashes can be nested within an array

```ruby
[ { a: 'ant' }, {b: "bear"} ]

arr[0][:c] = 'cat'
arr # => [{ :a => "ant", :c => "cat" }, { :b => "bear" }]
```

First reference the first element (which is a hash) in the array, update the hash

### Variable reference for nested collections

Variables can reference inner collections directly 

```ruby
a = [1, 3]
b = [2]
arr = [a, b]
arr # => [[1, 3], [2]]
```

What happens when we modify a variable that is then used inside a collection

```ruby
a = [1, 3]
b = [2]
arr = [a, b]
arr # => [[1, 3], [2]]

# element reassignment - changes the overall array
a[1] = 5
arr # => [[1, 5], [2]]
a => [1, 5]
```

The value of `arr` changed because `a` still points to the *same* `Array` object that’s in `arr.`

`arr` variable references a multidimensional array - the objects that make up the collection are referenced by other variables. If any of the individual objects that make up the array are modified those changes will be reflected in the outer array. Since `a` and `b` reference the same array objects that are elements in the `arr` 2-D array then modifying those inner arrays will mutate the entire array. 

-  **If one of the array objects inside the `arr`  is modified the change will also show in the `arr` array.** 

Collection contains references to the individual objects that make up the collection 

- `a` points to the first object in the `arr` collection - so modifying `a` will affect the overall collection since `a` points to an array, updating an element in the array will modify the overall array
- if `a` pointed to an integer and the value was reassigned, `a` would now point to a new location in memory

What if we modify the first array in `arr?`

```ruby
arr[0][1] = 8
arr # => [[1, 8], [2]]
a   # => [1, 8]
```

Produces the same result as modifying `a` directly:

- both cases modifying the *object* that `a` and `arr[0]` point to
- two ways to reference the *same object*
- one modify the object through `a` the other through `arr[0], both point to the same location in memory`
    - `arr[0][1] = 8` would be the same as `a[1] = 8`
    

![Untitled](Nested%20Data%20Structures%2052523bbec4ae4e5a89f8af65bf8be87c/Untitled%201.png)

### Shallow copy

Want to make a copy of the original collection before performming some modifications 

Copy an object - `dup` and `clone` - create a *shallow copy* of the object

- **only the object that the method is called on is copied**
- the objects that make up a collection are *shared* between the original and the copy
- if you modify the objects that make up the collection with a destructive method, the original and copied collection will both be updated - since modifying the objects that are shared within the collection
- If you create a new array from transformed objects in the copied array, then a new collection is created in memory and the original is not affected

```ruby
arr1 = ["a", "b", "c"]
arr2 = arr1.dup
arr2[1].upcase! # this method destructively modifies the object within the array

# so both the original and the copy will be affected
arr2 # => ["a", "B", "c"]
arr1 # => ["a", "B", "c"]
```

```ruby
arr1 = ["abc", "def"]
arr2 = arr1.clone
arr2[0].reverse! # method destructively modifies the object in the collection

arr2 # => ["cba", "def"]
arr1 # => ["cba", "def"]
```

**the destructive methods were called on the object *within* the array rather than the array itself** 

### Example 1

```ruby
arr1 = ["a", "b", "c"]
arr2 = arr1.dup # object is copied
arr2.map! do |char|
  char.upcase # map is called which creates a new object in memory with the transformed objects
end

arr1 # => ["a", "b", "c"]
arr2 # => ["A", "B", "C"]
```

Call destructive method `Array#map!` on `arr2` method modifies the array, replacing each element of `arr2` with a new value - changing the Array and not the elements within it, `arr1` is left unchanged 

<aside>
💡 `map!` calls the block once for each element, replacing the element with the value returned by the block - the elements in the collection point to a new value in memory

</aside>

### Example 2

```ruby
arr1 = ["a", "b", "c"]
arr2 = arr1.dup
arr2.each do |char|
  char.upcase! # destructive object method
end

arr1 # => ["A", "B", "C"]
arr2 # => ["A", "B", "C"]
```

`arr2.each` calls the block on each element in the array, inside the block `upcase!` is called on each element thereby mutating it - so both the original and copied array are modified since the *objects are shared* between the collections

## Freezing Objects

<aside>
💡 Ruby objects can be frozen in order to prevent them from being modified

</aside>

`clone` preserves the frozen state of the object

```ruby
arr1 = ["a", "b", "c"].freeze
arr2 = arr1.clone
arr2 << "d"
# Runtime Error - can't modify a frozen array
```

`dup` does not preserve the frozen state of the object

```ruby
arr1 = ["a", "b", "c"].freeze
arr2 = arr1.dup
arr2 << "d"

arr2 # => ["a", "b", "c", "d"]
arr1 # => ["a", "b", "c"]
```

- only mutable objects can be frozen because immutable objects are already frozen
- `frozen?` method can be used to check if an object is frozen
- `freeze` only freezes the object it’s called on - if the object its called on contains other objects, those objects won’t be frozen - so nested arrays can still be modified

```ruby
arr = [[1], [2], [3]].freeze
arr[2] << 4
arr # [[1], [2], [3, 4]]
```

- can also apply to **strings** within the array

```ruby
arr = ["a", "b", "c"].freeze
arr[2] << "d"
arr << "e" # Runtime error
```

## Deep Copy

There is no way in Ruby to create a deep copy or freeze objects within objects