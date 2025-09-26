#bindings
#variables
#scopes


Parameters act like regular variables. The value is set by the caller of the function such as:
```js
function callmebabe(yournumber) {
	if(younumber == 911) {
		console.log('call the police')
	}
}
callmebabe(911)
```



```js
let color = 5 * 5;
// use if you know the value will change within the block (local scope)

var color = 5 * 5;
// use if you want variable in global scope

const color = 5 * 5;
// cannot be reassigned
```
