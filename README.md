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

## 객체 Object - Methiods & Computed  property
### Methids
- Object.assign()
- Object.keys()
- Object.values()
- Object.entries()
- Object.formEntries()

####***Object.assign(): 객체복제*** 
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

  const newUser = Object.assignA({}, user);
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
####***Object.keys(): 키 배열 반환*** 

### Computed  property
```javascript
  //계산된 프로퍼티 Computed property
  let a = 'age';
  const user = {
    name : 'Mike',
    [a] : 30 //age : 30
    //변수 a에 할당된 값이 들어간다
  }
```
```javascript
  //식 자체를 넣는것도 가능
  const user = {
    [1 + 4] : 5,
    ["안녕"+"하세요"] : "Hello"
  }

  user {5: 5, 안녕하세요 : "Hello"}
```













