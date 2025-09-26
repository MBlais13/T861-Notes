#functions 


Instead of using the `function` keyword, you can use an arrow `=>`.
The arrow comes after the list of parameters and is followed by the functions body.


```javascript
const power = (base, exponent) => {
	let result = 1;
	for (let count = 0; count < exponent; count++) {
		result *= base;
	}
	return result;
}
```

### Simplified Arrow Functions

* When there is only one parameter name you can remove the brackets around the parameter list.

* If the body is a single expression then you can remove the curly braces and that expressions will be returned.

```js
const square1 = (x) => { return x * x; };
const square = x => x * x
// both function identically the same
```

### Other function stuff
* you can call a function with too many or too few arguments
* unneeded arguments are ignored
* missing arguments are set to undefined
* you can test for missing arguments