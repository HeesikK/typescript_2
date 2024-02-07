# 📑 Type Guard

## 🔎 타입 가드란?

타입 가드는 조건문 내에서 타입의 범위를 한정시킬 수 있는 방법이다.

## 🔎 타입 가드 방법
- ### 객체의 특정 키로 검사하기</br>
  만약 아래와 같이 Lion, Ant, Sparrow 라는 리터럴 객체 타입이 있을 때 구분하는 방법은 어떤 방법이 있을까? 간단하게 객체의 `value`가 다른 공통 속성명을 찾아서 key에 접   근해 구분해주면 된다. 이 객체에서 공통된 key는 type 이므로 타입 가드는 type라는 객체의 키 값을 통해 할 수 있다.
  
  ```javascript
  type Lion    = { type: 'mammal', gender: 'F' | 'M', bite: boolean };
  type Ant     = { type: 'insect', gender: 'F' | 'M', acid: boolean };
  type Sparrow = { type: 'bird',   gender: 'F' | 'M', fly: boolean };

  function typeCheck(a: Lion | Ant | Sparrow) {
     if (a.type === 'mammal') {
        a.bite = true;
     } else if (a.type === 'insect') {
        a.acid = true;
     } else {
        a.fly = true;
     }
  }  
  ```
- ### 특정 값의 타입으로 검사하기</br>
  특정 값의 타입을 확인하고 typeof 연산자를 통해서 간단하게 타입 가드를 할 수 있다.
  ```javascript
  const func = (x: number | string) => {
  if (typeof x === 'string') {
    console.log(x.subtr(1)); 
    console.log(x.substr(1)); 
  }
  x.substr(1); 
  };
  ```
- ### 가드문 함수를 만들어서 검사하기</br>
  복잡한 타입을 가드할 경우 타입스크립트의 `is` 키워드를 통해 타입 가드문 함수를 작성할 수 있다. 이 문법은 함수의 리턴값에 is 연산자를 명시해줌으로서
  타입을 확연하게 해준다.
  ```javascript
  interface Levi {
    student: number;
  }

  interface Elvin {
    teacher: number;
  }

  function leviOrElvin(arg: Levi | Elvin): arg is Levi {
    if ((arg as Levi).student){
      return false;
  } else {
      return true;
  }
  }

  function pet(arg: Levi | Elvin) {
   if (leviOrElvin(arg)) { // Levi 일 경우
      console.log(arg.student);
   } else { // Elvin 일 경우
      console.log(arg.teacher);
   }
  }
  ```
  
