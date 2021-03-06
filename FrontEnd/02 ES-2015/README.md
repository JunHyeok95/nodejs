## 07

> ES5 (2009)

```
1. 배열에 forEach, map, filter, reduce, some, every와 같은 메소드 지원
2. Object에 대한 getter / setter 지원
3. 자바스크립트 strict 모드 지원
4. JSON 지원 ( 과거에는 XML )
```

> ES6 (2015)

```

1. 변수선언 : let, const

2. 블록 유효범위 : var와 다르다. 함수의 정의 역시 블록 유효범위를 가짐

3. 템플릿 리터럴 : 문자열을 연접을 + , concat() 대신 백틱(`)으로 감싼 템플릿 활용

4. 디폴트 연산자

  function ex(name){              function ex2(name = "기본값"){
    if(!name){                      console.log(name) // name == "기본값"
      name = "기본값";      =>      }
    }                             ex2(); // 기본값
    console.log(name);
  }
  ex(); // 기본값

5. 화살표 함수

  const add = function(a,b){              const add2 = (a,b) => {
    return a+b;                   =>        return a+b;
  }                                       }
  add(1,2); // 3                          add2(2,3); // 5

6. this 예약어와 화살표 함수

  const text = { // ERR
    name : "기본",
    hello : function(){
      setTimeout(function(){
        console.log(`hello ${this.name}`);
      }, 1000);
    }
  };

  const text_bind = { // OK
    name : "바인드",
    hello_bind : function(){
      setTimeout(function(){
        console.log(`hello ${this.name}`);
      }.bind(this), 1000);
    }
  };


  function NumberEx() {
    var that = this
    that.num = 0;
    setInterval(function add() {
    // setInterval 안에서의 this 는 NumberEx의 this가 아니므로 다른 변수에 this 를 지정
    that.num++;
      console.log(that.num);
    }, 1000);
  }

  function NumberEx() {
    this.num = 0
    setInterval(() => {
      this.num++ // this is from NumberEx
    }, 1000);
  }

```

```
참고 : https://woowabros.github.io/experience/2017/12/01/es6-experience.html
```

## 08

> ES6 (2015)

```
7. 클래스 정의

  var Person = function(id, name){          class Person{
    this.id = id;                             constructor(id, name){
    this.name = name;                           this.id = id;
  }                                             this.name = name;
  Person.prototype.printName(){         =>    }
    console.log(this.name);                   printName(){
  }                                             console.log(this.name);
                                              }
                                            }

  var person = new Person(1, "name");
  preson.printName();

8. 클래스 상속

  class Participant extends Person{
    constructor(id, name, channel){
      super(id, name);
      this.channel=channel;
    }
  }

9. 프라미스(Promise) : 비동기 처리를 간결하고 일관적으로 다룰 수 있게 해주는 객체

  // old
  function lazy_execute(callback, delay){
    setTimeout(() => callback(), delay);
  }

  // Hell
  lazy_execute(() => {
    console.log("call 1");
    lazy_execute(() => {
      console.log("call 2");
      lazy_execute(() => {
        console.log("call 3 ...");
      }, 1000);
    }, 1000);
  }, 1000);

  // Promise then
  lazy_execute(() => console.log("call 1"), 1000)
    .then(() => lazy_execute(() => console.log("call 2"), 1000))
    .then(() => lazy_execute(() => console.log("call 3"), 1000));

  // new
  function lazy_exceute(callback, delay){
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        callback();
        resolve();
      }, delay);
    });
  };

  >>> 실행 대기 중 : dending,
      처리 성공 : fulfilled,
      처리 실패 : rejected
  >>> resolve() 호출 : fulfilled 상태 됨
  >>> reject() 호출 : rejected 상태 됨

  * then() 메서드는 2개의 인자를 받음 // 다른 방법으로는 1개 + catch 활용
  ex_func(value)
    .then(
      (value) => console.log("fulfilled", value),
      (value) => console.log("rejected", value),
    )

  // 예시
  function my_func(message, delay){
    const length_max = 10;

    return new Promise((resoleve, reject) => {
      setTimeout(() => {
        if(message.length > length_max){
          reject("메시지가 길다");
        }
        console.log("message");
        resolve("완료");
      }, delay);
    });
  };

  my_func("11글자를 넘으면 실패", 1000)
    .then((value) => console.log("fulfilled", value))
    .catch((value) => console.log("rejected", value));

```
