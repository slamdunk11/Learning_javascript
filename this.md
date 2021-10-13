# this란
- 함수가 속한 scope를 결정하는 object가 그 함수의 this라고 한다.
```javascript
var idiots = {
  name: 'idiots',
  members: {
    roto: {
      memberName: 'roto',
      play: function(){
        console.log(`band ${this.name} ${this.memberName} play start`
      }
    }
  }
}
idiots.mebers.roto.play()
```
> 저기서 play함수 안의 this는 roto를 가리킨다...!!

- this 예제 
```javascript
function Cat(name, age) {
  this.name = name;
  this.age = age;
}

const tabby1 = Cat('nana', 5)
console.log(tabby1.name)
```

> 오류가 발생한다<br/>
> tabby1이 undefined 이기 때문이다.<br/>
> function Cat의 this는 window를 가리킨다.

- 오류를 해결하고 nana를 출력하고 싶으면?
```javascript
const tabby1 = new Cat('nana', 5)

//여기서 this는 tabby1를 가리킨다
// 'new'가 중요하다!
```






