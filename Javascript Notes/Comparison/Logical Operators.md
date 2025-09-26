#comparison-operators

```javascript
true && false
// false

true && true
// true

true && console.log('Helo')
//
```
Is only `true` when both values are `true`


```js
false || true
// true
false || false
//false
```
Is only `true` when either of the values are `true`


```js
null || 'second'
// second
'first' || 'second'
// first
```