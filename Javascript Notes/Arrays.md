
> [!INFO] Array
> ```javascript
> let cars = ["Volvo", "BMW", "Ford"]
> ```

### Basic Methods
```javascript
cars.push("Honda")
// easiest way to add a new element to an array

cars.length
// Return the number of elements in an array

cars.sort()
// sorts the array
```

### Additional Methods
```javascript
let type = typeof cars
// returns the typeof array object

Array.isArray(cars)
// returns if is an array

cars.toString()
// converts an array into comma separeted string

cars.join()
// also converts an array into a comma separeted string

cars instanceof Array
// returns true if an object is created by a given constructor
```

### Add / Remove
```javascript
cars.pop()
// removes last element from an array

cars.push("Honda")
// adds a new element to the end of an array

cars.shift
// removes first array element and shifts all other elements down

cars.unshift("Honda")
// adds a new element to the beginning of an array
```

>[!error]
>Using `delete()` leaves `undefined` holes in the array.

### Merging
```javascript
let cars = ["Volvo", "BMW", "Ford"]
let colors = ["Violet", "Blue", "Red"]

let finished_car = cars.contact(colors)
// *.contact(*) merges two arrays together
```

### Copy

```javascript
let cars = ["Volvo", "BMW", "Ford"]

cars.copyWithin(2, 0)
// copy to index 2, all elements from index 0

cars.copyWithin(2, 0, 2)
// copy to index 2, the elements from index 0 to 2
```

### Flattening

```javascript
let animals = ["penguins", ["cat", ["dog"]], ["bird", "fish"]]

let animals1 = animals.flat()
let animals2 = animals.flat(2) // 2 = depth
let animals3 = animals.flat(Infinity) // will flatten until it cannot anymore
```

Output
>`animals1 = [ 'penguins', 'cat', [ 'dog' ], 'bird', 'fish' ]`
>`animals2 = [ 'penguins', 'cat', 'dog', 'bird', 'fish' ]`
>`animals3 = [ 'penguins', 'cat', 'dog', 'bird', 'fish' ]`

### Splice / Slice
```javascript
cars.splice()
// method to add new items to an array

cars.slice(#)
// method to remove elements in an array without leaving holes
```

Output
>`splice = [ 'Banana', 'Orange', 'Lemon', 'Kiwi' ]`

