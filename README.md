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
## Number, Math
### toString()
- 10진수 (실생활 사용 숫자) -> 2진수 / 16진수(색사표현)
```javascript
      let num = 10;
      num.toString(); //"10" //숫자를 문자로 바꿔줌
      num.toSrting(2); // "1010" //(숫자)의 진법으로 변환함

      let num2 = 255;
      num2.toString(16); //"ff" 16진수로 변환
```
### Math
- Math.PI;
- 3.141592653589793
```plaintext
      Math.ceil()
      Math.floor()
      Math.round()
      Math.toFixed()
      isNaN()
      parseInt()
      parseFloat()
      Math.random()
      Math.max()
      Math.min()
```
### Math.ceil() : 올림
소수점 상관없이 올림
```javascript
      let num1 = 5.1;
      let num2 = 5.7;
      Math.ceil(num1); //6
      Math.ceil(num2); //6      
```
### Math.floor() : 내림
```javascript
      let num1 = 5.1;
      let num2 = 5.7;
      Math.floor(num1); //5
      Math.floor(num2); //5   
```
### Math.round() : 반올림
```javascript
      let num1 = 5.1;
      let num2 = 5.7;
      Math.floor(num1); //5
      Math.floor(num2); //6 
```
### toFixed() : 소수점 자릿수
- 통계나 지표작업시 많이 사용
- 주의 ** 문자로 반환 해줌!!! Number()를 이용해 숫자로 변환 작업 필요
#### 소수점 둘째자리 까지 표현(셋째 자리에서 반올림)
```javascript
      let userRate = 30.1234;
      //1. 100을 곱하고
      userRate * 100 //3012.34
      //2. 반올림을 해준 뒤
      Math.round(userRate) //3012
      //3. 다시 100을 나누면 됨 = 30.12
      Math.round(userRate * 100) / 100 
```
혹은
```javascript
      let userRate = 30.1234;
      userRate.toFixed(2);
      //30.12

      userRate.toFixed(0); //30 -> 소수가0이니 정수 30만 남는것
      userRate.toFixed(6); //30.123400 -> 소수갯수보다 큰숫자를 넣으면 0으로 채워줌
```
```javascript
      // Number()를 이용해 숫자로 변환 작업

      let userRate = 30.1234;
      userRate.toFixed(2); //"30.12"
      Number(userRate.toFixed(2)); //30.12
```
### isNaN() : NaN인지 아닌지 판단해줌
```javascript
      let x = Number('x'); //NaN

      //자기자신과 똑같지 않다고 판단
      x == NaN // false
      x === NaN //false
      NaN == NaN //false

      isNaN(x) //true
      isNaN(3) //false
```
### parseInt() : 문자열을 숫자로 바꿔줌, 소수점은 무시 정수만 반환
Number()와 다른점은 문자가 혼용 되어 있어도 동작함
```javascript
      let margin = '10px';
      parseInt(margin); //10
      Number(margin); //NaN

      //숫자로 시작하지 않으면 NaN 반환
      let redColor = 'f3';
      parseInt(redColor); //NaN
      //두번째 인수를 받아서 진수를 지정할 수 있음, 16진수로 바꿈
      parseInt(redColor, 16); //243
      //11을 숫자로 바꾸고 2진수에서 10진수로 바꿀 수 있음
      //parseInt('11', 2) // 3
```
### parseFloat() : 문자열을 숫자로 바꿔줌,  부동 소수점을 반환함
```javascript
      let padding = '18.5%';
      parseInt(padding); //18
      parseFloat(padding); //18.5
```
### Math.random() : 0 ~ 1 사이의 무작위 숫자 생성
```javascript
      Math.random() //0.26027823967117412
      Math.random() //0.6318592894115811
      Math.random() //0.845444567548828
      Math.random() //0.7780357401504725
```
#### 1 ~ 100까지 임의의 숫자를 뽑고 싶다면?
```javascript
      //0.6789 * 100 (총 뽑고싶은 갯수)= 67.89, 100을 5로 바꾸면 1 ~ 5까지
      //Math.floor()소수점 이하를 버린다 = 67
      // + 1 -> 0.0...이 나올 수 있기 때문에 최소값으로 1을 더해준다 = 68
      Math.floor(Math.random()*100)+1
```
### Math.max(), Math.min() : 최대값 최소값
```javascript
      Math.max(1, 4, -1, 5, 10, 9, 5.54); //10
      Math.min(1, 4, -1, 5, 10, 9, 5.54); //-1
```
### Math.abs() : 절대값
```javascript
      Math.abs(-1)  //1
```
### Math.pow() : 제곱
```javascript
      Math.pow(2, 10)  //1024
```
### Math.sqrt() : 제곱근
```javascript
      Math.sqrt(16) //4
```
## string
```plaintext
      length
      toUppercase()
      toLowercase()
      str.indexOf(text)
      str.slice(n, m)
      str.substring(n, m)
      str.substr(n, m)
      str.trim()
      str.repeat(n)
      str.includes
```
```javascript
      let html = '<div class="box_title">제목</div>';
      let desc = "It's 3 o'clock.";
      let name = 'Mike';
      let result =`My name is ${name}`; //My name is Mike.
      let add = `2 더하기 3은 ${2+3}입니다.`; //2 더하기 3은 5입니다.
      let desc = `백틱은
                  여러줄을
                  포함 할 수 있습니다.`;
      let desc = '오늘은 화창한\n날씨가 계속 되겠습니다.'; //'' "" 줄바꿈하면 에러남
```
### length : 문자열 길이
```javascript
    let desc = '안녕하세요.';
    desc.length //6

    //특정 위치에 접근, 0부터 시작
    desc[2] //하
    desc[4] = '용'; //안 바뀜, 한 글자만 바꿀 수 없음
```
### toUppercase() / toLowercase() : 대문자 소문자
```javascript
      let desc = "Hi guys. Nice to meet you.";
      desc.toUppercase(); //"HI GUYS. NICE TO MEET YOU.";
      desc.toLowercase(); //"hi guys. nice to meet you.";
```
### str.indexOf(text) : 문자를 인수로 받아 몇번째 위치하는지 알려줌
- 0부터 시작
- 문자가 여러개라도 첫번째 위치만 반환
- if문 주의(시작문자 0번째 -> if 에서 0은 false)
```javascript
      let desc = "Hi guys. Nice to meet you.";
      desc.indexOf('to'); //14
      desc.indexOf('man'); // -1 -> 찾는 문자가 없을 경우 -1 반환

      if(desc.indexOf('Hi')){ //false, 출력안됨
          console.log('Hi가 포함된 문자입니다.');
      }
      if(desc.indexOf('Hi') > -1){ //false, 출력안됨
          console.log('Hi가 포함된 문자입니다.');
      }
```
### str.slice(n, m) : 특정범위의 문자열만 뽑기
- n : 시작점
- m : 없으면 끝까지, 양수면 그 숫자 전까지(5면 4까지반환), 음수면 끝에서부터 셈
```javascript
      let desc = "abcdefg";
      desc.slice(2); //"cdefg"
      desc.slice(0, 5); //"abcde"
      desc.slice(2, -2) //"cde" 
```
### str.substring(n, m) : n 과 m 사이의 문자열 반환, 음수는 0으로 인식
- n 과 m 을 바꿔도 동작함
```javascript
      let desc = "abcdefg";
      desc.substring(2, 5); //cde
      desc.substring(5, 2); //cde
```
### str.substr(n, m) : n 시작점, m 개수
- n 부터 시작해서 m 개를 가져옴
```javascript
      let desc = "abcdefg";
      desc.substr(2, 4); //cd
      desc.substr(-4, 2); //de
```
### str.trim() : 앞 뒤 공백 제거
- 보통 사용자로부터 무언가 입력받을때 사용
```javascript
      let desc = "  coding      ";
      desc.trim(); //coding
```
### str.repeat(n) : 문자열을 n번 반복
```javascript
      let desc = "hello!";
      desc.repeat(3); //hello!hello!hello!
```
### 문자열 비교
- 아스키 코드표
- 대문자보다 소문자가 크다
- a 보다 z가 크다
```javascript
      1 < 3 //true
      "a" < "c" true

      a.codePointAt(0); //97
      String.fromCodePoint(97) //"a"
```
```javascript
      let list = [
        "01. 목차1",
        "02. 목차2",
        "03. 목차3",
        "04. 목차4",
      ];
      let newList = [];
      for(let i = 0; i < list.length; i ++) {
          newList.push(
            list[i].slice(4)
          );
      }
      console.log(newList)l //["목차1","목차2","목차3","목차4"]
```
```javascript
      //금칙어 : 콜라
      function hasCola(str) {
          if(str.indexOf('콜라')){ 
              //true
              console.log('금칙어가 있습니다.');
          }else{
              console.log('통과');
          }
      }
      hasCola('와 사이다가 짱이야!'); //-1 -> true -> console.log('금칙어가 있습니다.');
      hasCola('뭐래, 콜라가 최고'); //console.log('금칙어가 있습니다.');
      hasCola('콜라'); //통과 0 -> false

```
```javascript
      function hasCola(str) {
          if(str.indexOf('콜라')){ 
              //true
              console.log('금칙어가 있습니다.');
          }else{
              console.log('통과');
          }
      }
      hasCola('와 사이다가 짱이야!'); //통과
      hasCola('뭐래, 콜라가 최고'); //console.log('금칙어가 있습니다.');
      hasCola('콜라'); //console.log('금칙어가 있습니다.');
```
### includes 
- 문자가 있으면 true
- 문자가 없으면 false
```javascript
      function hasCola(str) {
          if(str.includes('콜라')){ 
              //true
              console.log('금칙어가 있습니다.');
          }else{
              console.log('통과');
          }
      }
      hasCola('와 사이다가 짱이야!'); //통과
      hasCola('뭐래, 콜라가 최고'); //console.log('금칙어가 있습니다.');
      hasCola('콜라'); //console.log('금칙어가 있습니다.');
```
## 배열 Array
- push() : 뒤에 삽입
- pop() : 뒤에 삭제
- unshift() : 앞에 삽입
- shift() : 앞에 삭제
```plainText
      arr.splice(n, m, x)
      arr.slice(n, m)
      arr.concat(arr2, arr3 ...)
      arr.forEach(fn)
      arr.indexOf()
      arr.lastIndexOf()
      arr.includes()
      arr.find(fn)
      arr.findIndex(fn)
```
###  arr.splice(n, m, x) : 특정 요소 지우고 추가
- n 시작
- m 개수
- x 추가
- 0 부터시작
- 삭제된 요소 반환
```javascript
      let arr = [1, 2, 3, 4, 5];
      arr.splice(1, 2); //1부터 2개 지움
      console.log(arr) //[1, 4, 5]

      arr.splice(1, 3, 100, 200);
      console.log(arr); // [1, 100, 200, 5]

      const txt = ["나는", "철수", "입니다"];
      txt.splice(1, 0, "대한민국", "소방관"); //["나는", "대한민국", "소방관", "철수", "입니다"]

      let num = [1, 2, 3, 4, 5];
      let result = num.splice(1, 2);
      console.log(num); //[1, 4, 5]
      console.log(result); //[2,3]
      
```
### arr.slice(n, m) : n부터 m까지 반환
```javascript
     let arr = [1, 2, 3, 4, 5];
      arr.slice(1, 4); //[2, 3, 4]
      arr.slice(); //[1, 2, 3, 4, 5] 빈 값이면 배열 복사됨
```
### arr.concat(arr2, arr3) : 합쳐서 새배열 반환
- 인자에 주어진 배열이나 값들을 기존 배열과 합쳐서 새 배열 반환
```javascript
      let arr = [1, 2];
      arr.concat([3, 4]); //[1, 2, 3, 4]
      arr.concat([3, 4],[5, 6]); //[1, 2, 3, 4, 5, 6]
      arr.concat([3, 4], 5, 6); //[1, 2, 3, 4, 5, 6]
```
### arr.forEach(fn) : 배열 반복
- 해당요소, index, 해당배열 자체
```javascript
      let users = ['Mike', 'Tom', 'Jane'];
      users.forEach((item, index, arr) => {
        // ...
      })

      let arr = ['Mike', 'Tom', 'Jane'];
      users.forEach((name, index) => {
        console.log(`${index + 1}. ${name}`);
      })
```
### arr.indexOf / arr.lastIndexOf
- 발견하면 해당 요소의 인텍스 반환
- 없으면 -1 반환
```javascript
      let arr = [1, 2, 3, 4, 5, 1, 2, 3];
      arr.indexOf(3); //2
      arr.indexOf(3, 3); //3시작해서 3 찾아 : index 는 7(뒤에3)
      arr.lastIndexOf(3); //7 : 끝에서 첫번째 만나는 3의 index
```
### arr.includes(): 포함 하는지 확인 
```javascript
      let arr = [1, 2, 3];
      arr.includes(2); //true
      arr.includes(8); //false
```
### arr.find(fn) / arr.findIndex(fn)
- 첫번째 true 값만 반환하고 끝!!!, 만약 없으면 undfinded를 반환
- arr.findIndex(fn): 해당 index 반환 없으면 -1
```javascript
      let arr = [1, 2, 3, 4, 5];
      const result = arr.find((item) => {
        return item % 2 === 0;
      })
      console.log(result) //짝수 찾아서 반환, true 일때 멈추고 2
```
```javascript
      let userList = [
        {name: "Mike", age: 30},
        {name: "Jane", age: 27},
        {name: "Tom", age: 10},
      ];
      const result = userList.find((user) => {
          if(user.age < 19) {
              return true;
          }
          return false;
      });
      console.log(result) //{name: "Tom", age: 10}

      const result2 = userList.findIndex((user) => {
          if(user.age < 19) {
              return true;
          }
          return false;
      });
      console.log(result2) //{2}
```
### arr.filter(fn) : 해당 요소 모두 반환
```javascript
      let arr = [1, 2, 3, 4, 5];
      const result = arr.filter((item) => {
        return item % 2 === 0;
      })
      console.log(result) //[2, 4, 5]
```
### arr.reverse() : 역순으로 재정렬
- 최근 가입된 user, 게시판 작성 최신순
```javascript
      let arr = [1, 2, 3, 4, 5];
      arr.reverse(); //[5, 4, 3, 2, 1]
```
### arr.map(fn) : 함수를 받아 특정 기능을 시행하고, 새로운 배열을 반환 
```javascript
      let userList = [
        {name: "Mike", age: 30},
        {name: "Jane", age: 27},
        {name: "Tom", age: 10},
      ];
    let newUserList = userList.map((user, index) => {
        return Object.assign({}, user, {
            id: index + 1,
            isAdult: user.age > 19,
        });
    });
    console.log(newUserList);
    //{name: "Mike", age: 30, id: 1, isAdult: true}
    //{name: "Jane", age: 27, id: 2, isAdult: true}
    //{name: "Tom", age: 10, id: 3, isAdult: false}
``` 
### join : 배열을 합쳐서 문자열로 만듬
```javascript
      let arr = ["안녕", "나는", "철수야"];
      let result = arr.join();
      console.log(result); //안녕, 나는, 철수야

      let result = arr.join(  );
      console.log(result); //안녕  나는  철수야

      let result = arr.join(-);
      console.log(result); //안녕-나는-철수야
```
### split: 문자열을 배열로 만들어줌
```javascript
      let user = "Mike,Jane,Tom,Tony"
      let result = user.split(","); //"," 어떤걸 기준으로 배열을 나눌지
      console.log(result); //["Mike", "Jane", "Tom", "Tony"]

      let str = "Hello, My name is Mike.";
      const result = str.split("");
      console.log(result); //["H", "e", "l", "l", "o", ",", " ", "M", "y", " ", "n", "a", "m", "e"," ", "i", "s", " ", "M", "i", "k", "e", "."]
```
### Array.isArray() : 배열인지 확인
```javascript
      let user = {
        name: "Mike",
        age: 30,
      };
      let userList = ["Mike", "Tom", "Jane"];
      consoel.log(typeof user); //object
      consoel.log(typeof userList); //object
      consoel.log(Array.isArray(user)); //false
      consoel.log(Array.isArray(userList)); //true
```
### arr.sort() : 배열 재정렬, 배열 자체가 변경되니 주의
```javascript
      let arr = [1, 5, 4, 2, 3]
      arr.sort();
      console.log(arr); // [1, 2, 3 ,4, 5]

      let arr = ['a', 'c', 'd', 'e', 'b']
      arr.sort();
      console.log(arr); // ['a', 'b', 'c', 'd', 'e']

      let arr = [27, 8, 5, 13]
      arr.sort();
      console.log(arr); //[13, 27, 5, 8] 문자열로 인식, 1,2  인식해서 앞으로 배열

      let arr = [27, 8, 5, 13]
      arr.sort((a, b) => {
        return a - b;
      });
      console.log(arr); //[13, 27, 5, 8] 문자열로 인식, 1,2  인식해서 앞으로 배열
```
### 
```javascript
      
```
### 
```javascript
      
``` 
