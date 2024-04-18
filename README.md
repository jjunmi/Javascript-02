# Javascript-02

## 생성자 함수
- 첫글자는 대문자로 작명
- new 연산자를 사용해서 호출
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
    //this = {} //순서 2
    this.name = name;
    this.age = age;
    //return this; //순서 3
    }
    new 함수명(); //순서 1
  
```
