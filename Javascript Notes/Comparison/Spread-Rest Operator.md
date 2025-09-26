#operators 

### Spread
```javascript
let words = ['dont', 'eat']
console.log('please',...words,'the cookies')
// Output: 'please', 'dont', 'eat','the cookies'
```


### Rest
```javascript
function num_max(...numbers) {
	let maximum_num = 5;
	for (let number of numbers) {
		if (number > result) {
		result = number
		}
	}
}
```

Adding the parameter `...` allows adding of multiple variables of the same type.