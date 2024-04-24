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
      console.log(newList); //["목차1","목차2","목차3","목차4"]
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
          if(str.indexOf('콜라') > -1){ 
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
      arr.filter(fn)
      arr.reverse()
      arr.map(fn)
      arr.join()
      arr.split()
      Array.isArray()
      arr.sort(fn)
      arr.reduce(fn)
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

      let result = arr.join("  ");
      console.log(result); //안녕  나는  철수야

      let result = arr.join("-");
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
#### Lodash 라이브러리 사용 : [Lodash](https://lodash.com/)
-  _.sortBy(arr); 어떤 로직이 들어있는지 신경 안써도되고, 숫자든 문자든 객체든 원하는 기준으로 정렬 해줌
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
        console.log(a, b); //8 27, 5 8, 13 5 , 13 27 두개씩 비교 a - b 해서 크기 비교 순서 정함
        return a - b;
      });
      console.log(arr); //[13, 27, 5, 8] 문자열로 인식, 1,2  인식해서 앞으로 배열
      //배열내 두개씩 순차적으로 비교, 작은수가 앞으로 간다, - 해서 양수면 더큰값 뒤로
      // Lodash -> _.sortBy(arr);
```
### arr.reduce()
- 인수로 함수를 받음
- (지금까지 누적 계산값, 현재값) => {return 계산값};
- arr.reduceRight() -> 배열 우측부터 연산을 수행함
```javascript
      //배열의 모든수 합치기
      let arr = [1, 2, 3, 4, 5];
      //for, for of, forEach
      let result = 0; //초기값은 0으로 주고
      arr.forEach((num) => {
          result += num;
      });
      console.log(result); //15

      //reduce사용
      const reduceResult = arr.reduce((prev, cur) => {
          return prev + cur;
      }, 0); //안쓰면 첫번째 요소(1)가 들어감
      console.log(reduceResult); //15
```
map()이나 filter()대신에 reduce()를 써서 반환 예시
```javascript
      //나이를 판단해 성인만 뽑아서 새로운 배열 만듬
      let userList = [
        {name: "Mike", age: 30 },
        {name: "Tom", age: 10 },
        {name: "Jane", age: 27 },
        {name: "Sue", age: 26 },
        {name: "Harry", age: 3 },
        {name: "Steve", age: 60 },
      ]
      let result = userList.reduce((prev, cur) => {
          if(cur.age > 19){
            prev.push(cur.name);
          }
          return prev;
      }, []);
      console.log(result);
      // ["Mike", "Jane", "Sue", "Steve"]
```
```javascript
      //나이 합은? 
      let userList = [
        {name: "Mike", age: 30 },
        {name: "Tom", age: 10 },
        {name: "Jane", age: 27 },
        {name: "Sue", age: 26 },
        {name: "Harry", age: 43 },
        {name: "Steve", age: 60 },
      ]
      let result = userList.reduce((prev, cur) => {
          return prev += cur.age;
      }, 0);
      console.log(result);
      //196
```
```javascript
      //이름이 3자인 사람
      let userList = [
        {name: "Mike", age: 30 },
        {name: "Tom", age: 10 },
        {name: "Jane", age: 27 },
        {name: "Sue", age: 26 },
        {name: "Harry", age: 43 },
        {name: "Steve", age: 60 },
      ]
      let result = userList.reduce((prev, cur) => {
          if(cur.name.length === 3){
            prev.push(cur.name);
          }
          return.prev;
      }, []);
      console.log(result);
      //["Tom", "Sue"]
``` 
## 구조분해 할당 : Destructuring assignment
- 구조 분해 할당 구문은 배열이나 객체의 속성을 분해해서 그 값을 변수에 담을 수 있게 하는 표현식
### 배열 Array
```javascript
    let [x, y] = [1, 2];

    console.log(x); //1
    console.log(y); //2
```
```javascript
    let users = ['Mike', 'Tom', 'Jane'];

    let [user1, user2, user3] = users;
    //let user1 = users[0];
    //let user2 = users[1];
    //let user3 = users[2];

    console.log(user1); //'Mike'
    console.log(user2); //'Tom'
    console.log(user3); //'Jane'
```
```javascript
    //arr.split()이용
    //str.split('-'); -> ["Mike", "Tom", "Jane"];
    let str = "Mike-Tom-Jane";
    let [user1, user2, user3] = str.split('-');
    console.log(user1); //'Mike'
    console.log(user2); //'Tom'
    console.log(user3); //'Jane'
```
```javascript
    //해당하는 값이 없으면 undefined
    let [a, b, c] = [1, 2]; //c undefined
    //기본값을 주면 에러방지 가능
    let [a=3, b=4, c=5] = [1, 2];
    console.log(a); //1
    console.log(b); //2
    console.log(c); //5 기본값 적용됨
```
```javascript
    //공백과 쉼표를 이용해 필요하지 않은 배열요소 무시가능
    let [user1, ,user2] = ["Mike", "Tom", "Jane", "Tony"];
    console.log(user1); //'Mike'
    console.log(user2); //'Jane'
```
배열 구조 분해 : 바꿔치기
```javascript
    //a b 값 서로 교환하려면
    let a = 1;
    let b = 2;

    let c = a; //c에 a값을 저장해둠 : 임시 변수 생성
    a = b;
    b = c;

  //구조분해로 구현
  let a = 1;
  let b = 2;
  [a, b] = [b, a]
```
### 객체 Object
```javascript
      let user = {name: 'Mike', age: 30}
      let {name, age} user;
      //let name = user.name;
      //let age = user.age;
      //let {age, name} user; 순서를 바꿔도 동일하게 동작
  
      console.log(name); //'Mike'
      console.log(age); // 30
```
```javascript
      //변수 이름 변경가능
      let user = {name: 'Mike', age: 30}
      let {name: userName, age: userAge} = user;

      console.log(userName); //'Mike'
      console.log(userAge); // 30
```
```javascript
      //변수 이름 변경가능
      let user = {name: 'Mike', age: 30}
      let {name, age, gender} = user; //gender undefined

      let {name, age, gender = 'male'} = user;
      console.log(name); //'Mike'
      console.log(age); // 30
      console.log(gender); // 'male'

      //객체에 값이 있으면 기본값 무시
      let user = {name: 'Jane', age: 18, gender: 'female'}
      let {name, age, gender} = user; //gender undefined

      let {name, age, gender = 'male'} = user;
      console.log(name); //'Jane'
      console.log(age); // 18
      console.log(gender); // 'female'
```
## 나머지 매개변수(Rest parameters), 전개 구문 (Spread syntax) = ...
### 나머지 매개변수(Rest parameters)
인수전달
```javascript
      //함수에 넘겨주는 인수의 개수는 제한없음
      function showName(name){ //(name)개수 제한 없음
        console.log(name);
      }
      showName('Mike') //'Mike'
      showName('Mike', 'Tom') //'Mike' 에러 발생하지 않고 하나만 찍힘

      showName(); //undefined 에러 발생하지 않음
```
#### 함수에 인수를 얻는 방법은 두가지가 있음
1. arguments(화살표 함수엔 없음)
2. 나머지 매개변수
##### arguments
- 함수로 넘어 온 모든 인수에 접근
- 함수 내에서 이용 가능한 지역변수
- length/index
- Array 형태의 객체
- 배열의 내장 메서드 없음(forEach, map)
```javascript
      function showName(name){
          console.log(arguments.length); //2
          console.log(arguments[0]); //'Mike'
          console.log(arguments[1]); //'Tom'
      }
      showName('Mike', 'Tom');
```
##### 나머지 매개변수
- 정해지지 않은 개수의 인수를 배열로 나타냄
- 항상 마지막에 작성
```javascript
      function showName(...names){ (...배열이름)
          console.log(names);
      }
      showName(); //[]
      showName('Mike'); //['Mike']
      showName('Mike', 'Tom'); //['Mike', 'Tom']
```
```javascript
      //전달된 모든수를 더해야 될때
      //...number는 배열이고 length가 있기때문에 for문 사용가능
      //배열의 매서드도 사용가능
      function add(...numbers) {
          let result = 0;
          numbers.forEach((num) => (result += num));
          console.log(result); //6 55
      }
      add(1, 2, 3); //6
      add(1, 2, 3, 4, 5, 6, 7, 8, 9, 10); //55


      //배열의 매서드 사용 : reduce()
      function add(...numbers) {
      let result = numbers.reduce((prev, cur) => prev + cur);
      console.log(result); //6 55
      }
      add(1, 2, 3); //6
      add(1, 2, 3, 4, 5, 6, 7, 8, 9, 10); //55
```
```javascript
      //user 객체를 만들어 주는 생성자 함수
      function User(name, age, ...skills) {
        this.name = name;
        this.age = age;
        this.skills = skills;
      }
      const user1 = new User('Mike', 30, 'html', 'css');
      const user2 = new User('Tom', 20, 'JS', 'React');
      const user3 = new User('Jane', 10, 'English');
      console.log(user1) //{name: 'Mike', age: 30, skills: ['html', 'css']}
      console.log(user2) //{name: 'Tom', age: 20, skills: ['JS', 'React']}
      console.log(user3) //{name: 'Jane', age: 10, skills: ['English']}
```
### 전개 구문 (Spread syntax)
#### 전개 구문 (Spread syntax) : 배열
- 배열에 넣고 중간에 빼고 병합하는 작업: arr.push(), arr.splice(), arr.concat() 은 번거로움, 전개구문 사용하면 쉽게 가능
```javascript
      let arr1 = [1, 2, 3];
      let arr2 = [4, 5, 6];

      let result = [...arr1, ...arr2];
      //중간에 쓰는것도 가능
      let result2 = [0, ...arr1, ...arr2, 7, 8, 9];

      console.log(result); //[1, 2, 3, 4, 5, 6]
      console.log(result2); //[0, 1, 2, 3, 4, 5, 6, 7, 8 , 9]
```
```javascript
    // arr1을 [4, 5, 6, 1, 2, 3]으로 만들려면?
    let arr1 = [1, 2, 3];
    let arr2 = [4, 5, 6];

    // X
    arr2.forEach((num) => {
      arr1.unshift(num) //[6, 5, 4, 1, 2, 3]
    })
    //돌기전에 역순으로 정렬 시켜줘야함
    arr2.reverse().forEach((num) => { //reverse() -> arr2 [6, 5, 4]
      arr1.unshift(num) //[4, 5, 6, 1, 2, 3]
    })
    //전개 구문사용 하면
    arr1  = [...arr2, ...arr1];

    console.log(arr1);
```
#### 전개 구문 (Spread syntax) : 객체
```javascript
      let user = {name: 'Mike'}
      let mike = {...user, age: 30}
      console.log(mike) //{name: "Mike", age: 30}
```
Object.assign()쓸 필요 없음
```javascript
      let arr = [1, 2, 3];
      let arr2 = [...arr]; //[1, 2, 3]

      let user = {name: 'Mike', age: 30};
      let user2 = {...user};

      user2.name = 'Tom';

      console.log(user.name); //"Mike"
      console.log(user2.name); //"Tom" user2가 별개로 복제 되어서 name을 바꿔도 user에 영향주지 않음
```
```javascript
      let user = {name: "Mike"};
      let info = {age: 30};
      let fe = ["JS", "React"];
      let lang = ["Korean", "English"];

      user = Object.assign({}
             user,
            info,
            {
                skills = [],
            });
      //skills에 fe, lang 넣기
      //방법 1
      fe.forEach(item => {
        user.skills.push(item);
      })
      lang.forEach(item => {
        user.skills.push(item);
      })

      //방법 2 전개구문 사용시
      user.skills = [...fe, ...lang]
      console.log(user);
```
위에꺼 전개구문으로 정리 하자면
```javascript
      let user = {name: "Mike"};
      let info = {age: 30};
      let fe = ["JS", "React"];
      let lang = ["Korean", "English"];

    user = {
      ...user,
      ...info,
      skills: [...fe, ...lang],
    };

    console.log(user);
```
## 클로저 (Closure)
- 함수와 렉시컬 환경의 조합, 함수가 생성될 당시의 외부 변수를 기억
### 어휘적 환경 (Lexical Environment)
- Lexical환경
1. 코드가 실행되면 script 내 변수 들이 Lexical환경에 올라감(호이스팅) -> one: 초기화x(사용불가), addOne: function 초기화o(사용가능)
2. one: undefined (사용해도 에러는 안남 값으로 undefined 반환), addOne: function
3. one: 1, addOn: function
4. 함수 실행 num: 5
5. 내부 Lexical 환경(내부가 외부 전역 참조) -> num: 5, 전역 Lexical 환경 -> one:1, addOne: function
```javascript
      let one; //2
      one = 1; //3
      function addOne(num) {
        console.log(one + num);
      }
      addOne(5); //4
```
1. 전역 Lexical 환경 -> makeAdder:function, add3: 초기화x
2. const add3 = makeAdder(3);실행시 함수가 실행되고 makeAdder Lexical환경이 만들어짐 -> x:3 전달받은 x의 값이 들어감
3. 전역 Lexical 환경 -> makeAdder:function, add3: function
4. console.log(add3(2)); 실행시 return function(y) {} 익명함수 Lexical환경이 만들어짐 -> y:2
5. 익명함수에 x 값이 없으니 상위함수인 makeAdder의 x에 접근함 (makeAdder Lexical환경으로 찾으러감) = 클로저 Closure
```javascript
      function makeAdder(x) {
          return function(y) {
              return x + y;
          }
      }
      const add3 = makeAdder(3);
      console.log(add3(2)); //5

      const add10 = makeAdder(10);
      console.log(add10(5)); //15
      console.log(add3(1)); //4
```
```javascript
      function makeCounter() {
          let num = 0; //은닉화
          return function() {
            return num ++;
          };
      }

      let counter = makeCounter();

      console.log(counter()); //0
      console.log(counter()); //1
      console.log(counter()); //2
```
## setTimeout / setInterval
- setTimeout (함수, 시간, 인수) : 일정 시간이 지난 후 함수를 실행
- setInterval : 일정 시간 간격으로 함수를 반복
- clearTimeout(tId); : 예정된 작업을 없앰, setTimeout은 아이디를 반환하는데, tId를 사용해 스케줄 취소
### setTimeout
```javascript
      //작성법 1 : 함수 전달
      function fn() {
        console.log(3)
      }
      setTimeout(fn, 3000); //3초후에 console.log(3)찍어줌

      //작성법 2 : 함수 전달 안 하고 바로 작성
      setTimeout(function() {
        console.log(3)
      }, 3000);
```
### setTimeout 인수 / ClearTimeout
```javascript
      const tId = function showName(name) {
                    console.log(name);
                  }
      setTimeout(showName, 3000, 'Mike'); //인수 'Mike'가 name 으로 들어감

      clearTimeout(tId); //3초전에 실행되기 떄문에 log 안찍힘, 아무일도 일어나지 않음
```
### setInterval
```javascript
      function showName(name) {
        console.log(name);
      }
      const tId = setInterval(showName, 3000, 'Mike'); //3초마다 'mike'가 찍힘, 'mike' 'mike' 'mike'...

      clearTimeout(tId); //중단시 사용
```
- 주의사항: 시간을 0으로 줘도 바로 실행되지 않음, 실행중인 스크립트가 종료된후 스케줄인 함수 실행
- 브라우저엔 시본적으로 4ms~ 대기 시간이 있음
```javascript
      setTimeout(function() {
        console.log(2) //2번째로 찍힘
      }, 0);
      console.log(1); //1번째로 찍힘
```
### setTimeout 인수 / ClearTimeout
```javascript
      let num = 0;
      function showTime() {
          console.log(`안녕하세요. 접속하신지 ${num++}초가 지났습니다.`);
          //5초 동안만 보여줌 0,1,2,3,4,5
          if(num > 5) {
            clearInterval(tId);
          }
      }
      const tId = setInterval(showTime, 1000);//일초에 한번씩 메세지가실행 
```
## call, apply, bind
- 함수 호출 방식과 관계없이 this를 지정할 수 있음
### call()
- 모든 함수에서 사용가능 this를 특정값으로 지정가능
- call(this가 사용할 값, 함수가 사용할 매개변수 )
- 매개변수를 직접 받아서 객체에 들어감
```javascript
      const mike = {
        name: 'Mike',
      };
      const tom = {
        name: 'Tom',
      };
      function showThisName() {
        console.log(this.name); //window
      }

      showThisName(); //window.name; ""
      showThisName().call(mike); //Mike
      showThisName().call(tom); //Tom

      function update(birthYear, occupation){
        this.birthYear = birthYearl;
        this.occupation = occupation;
      };

      update().call(mike, 1999, 'singer');
      console.log(mike); // {name: 'Mike', birthYear: 1999, occupation: "singer"}
      update().call(tom, 2002, 'teacher');
      console.log(tom); // {name: 'Tom', birthYear: 2002, occupation: "teacher"}
```
### apply()
- apply(this가 사용할 값, &#91;매개변수, 매개변수&#93;)
- 함수 매개변수를 처리하는 방법을 제외하면 call 과 같음
- 매개변수를 배열로 받음
- 배열요소를 함수 매개변수로 사용할때 유용
```javascript
      function update(birthYear, occupation){
        this.birthYear = birthYearl;
        this.occupation = occupation;
      };

      update().apply(mike, [1999, 'singer']);
      console.log(mike); // {name: 'Mike', birthYear: 1999, occupation: "singer"}
      update().apply(tom, [2002, 'teacher']);
      console.log(tom); // {name: 'Tom', birthYear: 2002, occupation: "teacher"}
```
```javascript
    const minNum = Math.min(3, 10, 1, 6, 4);
    const maxNum = Math.max(3, 10, 1, 6, 4);

    console.log(minNum); //1
    console.log(maxNum); //0

    //Math에 배열 넣으면 NaN으로 나옴
    const minNum = Math.min([3, 10, 1, 6, 4]);
    console.log(minNum); //NaN

```
```javascript
    //배열이 있다고 하면 풀어서 넣어줘야함
    const nums = [3, 10, 1, 6, 4];

    const minNum = Math.min(nums);
    const maxNum = Math.max(nums);

    console.log(minNum); //NaN
    console.log(maxNum); //NaN

    //spread 연산자 활용
    const nums = [3, 10, 1, 6, 4];

    const minNum = Math.min(...nums);
    const maxNum = Math.max(...nums);

    console.log(minNum); //1
    console.log(maxNum); //10

    //call(), apply() 사용
    const nums = [3, 10, 1, 6, 4];

    const minNum = Math.min.apply(null, nums);
    const maxNum = Math.max.apply(null, nums);
    const minNum = Math.min.call(null, ...nums);
    const maxNum = Math.max.call(null, ...nums);

    console.log(minNum); //1
    console.log(maxNum); //10
```
### bind()
```javascript
      const mike = {
        name : "Mike",
      };

      function update(birthYear, occupation){
        this.birthYear = birthYearl;
        this.occupation = occupation;
      };

      const updateMike = update.bind(mike);

      updateMike(1980, "police");
      console.log(mike) //{name: "Mike", birthYear: 1980, occupation: 'police'}
```
```javascript
      const user = {
        name: "Mike",
        showName: function() {
          console.log(`hello, ${this.name}`);
        },
      };

      user.showName(); //hello, Mike

      let fn = user.showName;
      fn(); //hello,
      fn.call(user); //hello, Mike
      fn.apply(user); //hello, Mike

      let boundFn = fn.bind(user);
      boundFn(); //hello, Mike
```
## 상속, prototype




