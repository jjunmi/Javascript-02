# Javascript-02

## 생성자 함수
***new  -> 객체생성***
- 첫글자는 대문자로 작명
- new 연산자를 사용해서 호출
- 일관성 있게 객체 생성 가능
```javascript
  //첫글자는 대문자로 작명 User
  function User(name, age){
    this.name = name;
    this.age = age;
  }

  //new 연산자를 사용해서 호출
  //객체 3개 생성됨
  let user1 = new User('Mike', 30); //User {name: 'Mike', age: 30}
  let user2 = new User('Jane', 22); //User {name: 'Jane', age: 22}
  let user3 = new User('Tom', 17); //User {name: 'Tom', age: 17}

  //알고리즘 동작 원리(2,3 코드에 없음)
    function User(name, age){
    //this = {} //순서 2: 빈 객채를 만들고 this에 할당
    this.name = name; //순서 3: this에 프로퍼티 추가
    this.age = age; //순서 3: this에 프로퍼티 추가
    //return this; //순서 4: this 반환
    }
    new 함수명(); //순서 1 : new를 붙여서 실행
```
```javascript
  function User(name, age) {
    this.name = name;
    this.age = age;
    this.sayName = function() {
      console.log(this.name);
    } 
  }
  let user5 = new User('Han', 40);
  user5.sayName(); //'Han'
```
생성자 함수 : 상품 객체를 생성해보자
```javascript
  function Item(title, price){
    //this = {};안보이지만 실행과정

    this.title = title;
    this.price = price;
    this.showPrice = function() {
      console.log(`가격은 ${price}원 입니다.`);
    }

    //return this; 안보이지만 마지막에실행됨
  }
  const item1 = new Item('인형','3000');
  const item2 = new Item('가방','4000'); //-> new 안붙이면
  const item3 = new Item('지갑','9000');
  console.log(item1, item2, item3);

  //Item {title: "인형", price: 3000, showPrice: f}
  //Item {title: "가방", price: 4000, showPrice: f} //-> undefined 뜸
  //Item {title: "지갑", price: 9000, showPrice: f}

  item3.showPrice(); //가격은 9000원 입니다.
```

## 객체 Object - Methods & Computed  property
### Methods
- Object.assign()
- Object.keys()
- Object.values()
- Object.entries()
- Object.formEntries()

***Object.assign(): 객체복제*** 
```javascript
  const user = {
    name: 'Mike',
    age: 30,
  }
  //const cloneUser = user; X 객체가 복사 되는게 아니라 참조값만 복사됨, 즉 별명 두개로 하나의 값들 공유
  // {name:'Mike', age: 30,}
  //cloneUser.name = 'Tome'; -> user.name 도 바뀜

  // 그래서!!! 동일하게 복제 하려면 Object.assign() 메서드 써야함
  //const newUser = object.assign({}, user); -> {}빈 객체는 초기값임, 두번째 매개변수로 들어온 객체들이 초기값에 병합됨으로 복제되는것
  // {} + {name:'Mike', age: 30,}

  const newUser = Object.assign({}, user);
  newUser.name = 'Tom';
  console.log(user.name); //'Mike'
  //newUser != user (같은 객체가 아님)

  //다른 예시 : 초기값에 대해
  Object.assign({gender: 'male'}, user); //성별값만 있는 객체가 user를 병합하고 총 3개의 프로퍼티를 갖게 된다
  // {gender: 'male', name:'Mike', age: 30,}

  //다른 예시 : 같은 키값
  Object.assign({name: 'Tom'}, user); //키가 같으면 뒤에 껄로 덮어쓰게됨 
  // {name:'Mike', age: 30,}

  //다른 예시 : 두개 이상의 객체도 합칠 수 있음
  const user = {name:'Mike'}
  const info1 = {age: 20,}
  const info2 = {gender: 'male',}
  Object.assign(user, info1, info2)
```
***Object.keys(): 키 배열 반환*** 
```javascript
  const user =  {
    name : 'Mike',
    age : 30,
    gender : 'male'
  }
  //user(객체)를 Object.keys(인수)로 전달함
  const result = Object.keys(user);
  console.log(result) //키들이 배열로 반환됨 ["name", "age", "gender"]
```
***Object.values(): 값 배열 반환*** 
```javascript
  const user =  {
    name : 'Mike',
    age : 30,
    gender : 'male'
  }
  const result = Object.values(user);
  console.log(result)//value들이 배열로 반환됨 ["Mike", "30", "male"]
```
***Object.entries(): 키/값 배열 반환*** 
```javascript
  const user =  {
    name : 'Mike',
    age : 30,
    gender : 'male'
  }
  Object.entries(user); //key와value들이 쌍이로 묶어 배열로 반환됨
  // [
  //  ["name","Mike"], //0
  //  ["age",30], //1
  //  ["gender","male"] //2
  // ]
```
***Object.fromEntries(): 키/값 배열을 객체로*** 
```javascript
  const arr = 
  [
    ["name","Mike"],
    ["age",30],
    ["gender","male"]
  ];
  Object.fromEntries(arrr);
  // {
  //   name : 'Mike',
  //   age : 30,
  //   gender : 'male',
  // }
```
### Computed  property
```javascript
  //계산된 프로퍼티 Computed property
  let n = "name"
  let a = 'age';
  const user = {
    [n] : "Mike", //name : "Mike"
    [a] : 30, //age : 30
    [1 + 4] : 5,
    //변수 a에 할당된 값이 들어간다
  }
  console.log(user);
  //{5: 5, name: "Mike", age: 30}
```
```javascript
  //식 자체를 넣는것도 가능
  const user = {
    [1 + 4] : 5,
    ["안녕"+"하세요"] : "Hello"
  }
  user {5: 5, 안녕하세요 : "Hello"}
```
```javascript
  function makeObj(key, val) {
    return{
      [key] : val
    }
  }
  const obj = makeObj('나이', 33);
  console.log(obj) // {나이: 33}
  //const obj = makeObj('이름', 33);
  //console.log(obj) // {이름: 33}
```

*** ***
## 심볼 Symbol
### 1. 객체 property key는 문자형으로 가능
- 유일한 식별자, 유일성이 보장된다
- Symbol : 이름이 같더라도 다른존재임
```javascript
      const obj = {
        1: '1입니다',
        flase: '거짓'
      }
      object.keys(obj); //["1", "false"] 문자형으로 반환
    
      //접근시 문자1이나 문자false로 접근 가능
      obj['1'] //"1 입니다."
      obj['false'] //"거짓"
  // 
```
### 2. 하나더 가능 한게 바로 symbol형
Symbol은 유일한 식별자를 만들때 사용
```javascript
      const a = Symbol(); //new를 붙이지 않음!
      const b = Symbol();
      console.log(a) //Symbol();
      console.log(b) //Symbol();

      a == b; //false
      a === b; //false

      //Symbol : 유일성 보장, 설명 붙일 수 있음
      const id = Symbol('id');
```
```javascript
      //심볼을 객체의 key로 사용 예시 (computed property :key)
      const id = Symbol('id');
      const user = {
        name : 'Mike',
        age : 30,
        [id] : 'myid'
      }
      console.log(user); //{name: "Mike", age": 30, Symbol(id): "myid"}
      console.log(user[id]); //"myid"
      user[id] //"myid"

      //Object Method ,for in은 key가 symbol 형인 property는 건너뜀
      object.keys(user); //["name", "age"]
      object.values(user); // ["Mike", 30]
      Object.entries(user); //[Array(2),Array(2)]
      for(let a in user){}

      //원본 데이터는 Object Method ,for in으로순회하면서 사용하고 있을 수 있기 때문에(내가 추가한 프로퍼티가 어디서 나올지 예측할 수 없음)
      //그러므로 원본은 건드리지 않고 속성을 추가할 수 있다
      const user = {
        name : 'Mike',
        age : '30'
      }
      const id = Symbol('id');
      user[id] = 'myid';
```
## Symbol.for() : 전역 심볼
- 하나의 심볼만 보장받을 수 있음
- 없으면 만들고, 있으면 가져오기 때문
- Symbol 함수는 매번 다른 Symbol 값을 생성하지만,
- Symbol.for 메소드는 하나를 생성한 뒤 키를 통해 같은 Symbol을 공유
```javascript
      const id1 = Symbol.for('id');
      const id2 = Symbol.for('id');

      id1 === id1; // true

      //생성한 이름(Symbol.for('id') -> 'id')을 알고 싶다면 Symbol.keyFor를 사용해 변수를 넣어주면 됨
      Symbol.keyFor(id1) // "id"

      //!!! 전역심볼이 아닌 Symbol()은 keyFor사용불가, description사용 !!!
      const id = Symbol('id 입니다.');
      id.description; // "id 입니다."
```
숨겨진 Symbol key 보는법
```javascript
      const id = Symbol('id');
      const user =  {
        name : 'Mike',
        age : 30,
        [id] : 'myid'
      }
      Object.getOwnPropertySymbols(user); // Symbol(id) 심볼만 보여줌
      Reflect.ownKeys(user); //["name", "age", "Symbol(id)"]심볼 포함한 모든키를 보여줌
```
실전 예시
```javascript
      //다른 개발자가 만들어 놓은 객체
      const user = {
        name : "Mike",
        age : 30
      }

      //내가 작업
      //user.showName = function() {};
      // -> 결과 : His showName is function(){}.
      const showName = Symbol("show name");
      user[showName] = function() {
        console.log(this.name);
      }
      user[showName]();
      //Mike

      //사용자가 접속하면 보이는 메세지
      for(let key in user){
        console.log(`His ${key} is ${user[key]}.`);
      }
      //His name is Mike.
      //His age is 30.
```












