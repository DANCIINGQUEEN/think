closure : 폐쇄, 종료, 종결시키다

```js
function getClosure(){
  var freeVar = 'independent'
  return function (){
    return freeVar
  }
}
var closure = getClosure()
console.log(closure()) // 'independent'
```
