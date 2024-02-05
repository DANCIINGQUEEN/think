# Binding
- 변수, 함수, 또는  this키워드가 특정 값이나 객체에 연결되는 과정
- this 바인딩은 함수의 호출 방식에 따라 그 값이 결정됨


## this 바인딩의 다양한 형태\

1. Default Binding 기본 바인딩
   함수가 스탠드얼론(Standalone)[함수가 객체의 메서드로 호출되지 않고, 독립적으로 호출될 때] 으로 호출될 때 this는 전역 객체에 바인딩됨
```js
function show(){
   console.log(this)    //전역 객체 또는 undefined
}
show()
```

2. Implicit Binding  암시적 바인딩
  객체의 메소드로서 함수가 호출될 때, this는 그 함수가 속한 객체에 바인딩됨
```js
const obj = {
  value : 42,
  show : function() {
      console.log(this.value)     //42
      }
}
obj.show()
```

3. Explicit Binding 명시적 바인딩
   call, apply, bind메소드를 사용하여 함수를 호출할 때 this를 명시적으로 바인딩 할 수 있음
```js
functinon show() {
  console.log(this.value)
}
const obj = { value : 42 }
show.call(obj)    //42
show.apply(obj)   //42

const boundShow = show.bind(obj)
boundShow()    //42
```

4. New Binding
   생성자 함수를  new 키워드와 함께 호출하면, this는 새로 생성된 객체에 바인딩됨
```js
function Item(value) {
    this.value = value
}
const item = new Item(42)
console.log(item.value)  //42
```

5. Arrow Function Binding 화살표 함수 바인딩
   화살표 함수에서는  this가 전통적인 방식으로 바인딩되지 않음. 대신, 자신이 선언된 렉시컬 스코프의 this값을 상속받음
```js
const obj = {
    value : 42,
    show : function() {
      setTimeout(()=>{
        console.log(this.value)  //42, this는 렉시컬 스코프의  this를 상속받음
      }, 1000)
    }
}
obj.show()
```
