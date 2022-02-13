# Methods

### `each`

The `each` method is functionally equivalent to using `loop` and represents a simpler way of accomplishing the same task 

```ruby
[1, 2, 3].each do |num|
	puts num
end

hash = {a: 1, b: 2, c: 3 }
hash.each do |key, value|
	puts "The key is #{key} and the value is #{value}"
end

def a_method(arr)
	arr.each do |num|
		puts num * 2
	end
end 
# last expression in the method is arr.each so the arr is returned from the method call
a_method([1, 2, 3]) #=> [1, 2, 3]
```

- `each` method takes a block as its argument, code in block is executed upon each iteration
- `each` sends the value of the current element to the block in the form of an argument - `num` represents the current element in the array
- **returns the original collection**

### `select`

To perform selection, `select` evaluates the **return value of the block.**

- The block returns a value on each iteration, which then gets evaluated by `select`. The return value of the block is the return value of the last expression within the block
- `select` performs selection based on the truthiness of the block’s return value. If the block’s return value is always truthy, then all the elements will be selected. When an element is selected, its placed in a **new collection**

```ruby
[1, 2, 3].select do |num|
	num.odd?
end
#=> [1, 3]

[1, 2, 3].select do |num|
	num + 1
	puts num # returns nil 
end
# since the last expression returns nil from the block, nil is a falsy value 
# no elements will be added to the new collection, returns []
```

- if the return value of the block is *truthy* then then the element during that iteration will be selected and placed into a new collection
- **returns a new collection of selected elements**

### `map`

`map` also considers the return value of the bock. The difference between `select` and `map` is that `map` uses the return value of the block to perform transformation instead of selection

*map performs transformation based on the return value of the block*

```ruby
[1, 2, 3].map do |num|
	num * 2
end #=> [2, 4, 6]

[1, 2, 3].map do |num|
	num.odd?
end #=> [true, false, true]
```

- `map` takes the value returned from the block and places it in a **new collection**
- process is repeated for each element in the collection
- if the code in the block is not a transformation instruction, it will still place the value returned into a new collection

## Enumerable

`Array` and `Hash` both have an `each` method which is specific to them and defines how the items in those collections are iterated over

The `select` and `map` methods are actually defined in a module called **Enumerable** and are made available to the `Array` and `Hash` classes 

**certain collection types have access to specific methods for a reason**

## Summary

Methods like `each`, `select`, and `map` are provided by Ruby to allow for simpler implementations of common collection manipulation tasks. Using these methods to iterate, select, and transform a collection is preferred over manually looping.

[Collection Methods](https://www.notion.so/c30eeb8eee994d2094c4afac1ca7c306)