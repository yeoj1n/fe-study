## 1. let, var, const를 사용하여 생성된 변수들의 차이점은 무엇인가요?

var

- 함수 스코프
- 재할당/재선언 가능

let/consst

- 블럭 스코프
- 재선언 불가
- let은 재선언 가능, const는 재선언 불가

var의 경우 값의 선언과 초기화가 동시에 일어나지만 let/const의 경우 선언만 일어나며 선언-초기화 과정 사이에 TDZ가 발생하게된다.

```
foo; // undefined
var foo = 1;

bar;// Reference Error
var bar = 1;
```

## 2. ES6클래스와 ES5 함수 생성자의 차이점은 무엇인가요?

```
// ES5
function Person() {
   this.name = name;
}

// ES6
class Person {
    constructor(name) {
        this.name = name;
    }
}
```

생성자

```
// ES5
function Student(name, studentId) {
    Person.call(this, name);
    this.studentId = studentId;
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

// ES6
class Student extends Person {
    constructor(name, studentId) {
        super(name);
        this.studentId = studentId;
    }
}
```

## 3. 화살표 => 함수 문법에 대한 사용 예시를 들 수 있나요? 이 새로운 문법은 다른 함수와 어떻게 다른가요?

function 키워드없이 함수를 생성할 수 있다. 또한, 화살표 함수 내 this는 일반 함수와 달리 주변 스코프에 묶인다.
(일반 함수의 경우 this는 함수가 호출하는 객체에 의해 결정된다.)

## 4. 생성자의 메서드에 화살표 문법을 사용하면 어떤 이점이 있나요?

함수 생성시 this값이 결정되고 그 이후 변경되지 않는다는 점

```
const Person = function (firstName) {
  this.firstName = firstName;
  this.sayName1 = function () {
    console.log(this.firstName);
  };
  this.sayName2 = () => {
    console.log(this.firstName);
  };
};

const john = new Person('John');
const dave = new Person('Dave');

john.sayName1(); // John
john.sayName2(); // John

// 일반 함수의 'this'값은 변경할 수 있지만, 화살표 함수는 변경할 수 없습니다.
john.sayName1.call(dave); // Dave (because "this" is now the dave object)
john.sayName2.call(dave); // John

john.sayName1.apply(dave); // Dave (because 'this' is now the dave object)
john.sayName2.apply(dave); // John

john.sayName1.bind(dave)(); // Dave (because 'this' is now the dave object)
john.sayName2.bind(dave)(); // John

var sayNameFromWindow1 = john.sayName1;
sayNameFromWindow1(); // undefined (because 'this' is now the window object)

var sayNameFromWindow2 = john.sayName2;
sayNameFromWindow2(); // John
```

## 5. 고차 함수 (higher-order function)의 정의는 무엇인가요?

### 일급객체

- 값으로 사용 가능
- 변수에 할당 가능
- 함수의 리턴값으로 사용 가능
- 함수의 인자로 전달 가능

-> 즉, 함수는 일급객체이다.

### 고차함수 > 커리함수

- 다른 함수를 인자로 받거나,

결과를 함수로 반환하는 함수이다.

### 콜백함수

- 다른 함수의 인자로써 이용되는 함수

```
function printHello(){
    print('hello');
}
function sleepAndExecute(sleepTimeSecond, callback) {
    sleep(sleepTimeSecond);
    callback();
}

// 3초 후 'hello' 출력
sleepAndExecute(3, printHello);
```

- 어떤 이벤트에 의해 호출되어지는 함수

```
function onCableConnected(){
    print("케이블이 연결되었습니다");
};

//케이블이 연결될 때 마다 전달된 onCableConnected가 호출된다고 가정 setOnCableConnected(onCableConnected);

```

```
function double(num) {
 return num * 2;
}

// 고차함수
function doubleNum(func, num) {
  let doubleArr = [];
  return func(num);
}
// 함수 doubleNum은 다른 함수를 인자로 받는 고차 함수이다.
// 함수 doubleNum의 첫 번째 인자 func에 함수가 들어올 경우 func는 doubleNum의 콜백함수이다.
let output = doubleNum(double, 4);
console.log(output); // 8
```

```
function double(num) {
 return num * 2;
}

function doubleAdder(added, func) {
  const doubled = func(added);
  return function (num) {
    return num + doubled;
  };
}
// 함수 doubleAdder는 고차 함수이다.
// 함수 doubleAdder의 인자 func는 함수 doubleAdder의 콜백 함수이다.
// doubleAdder(5, double)는 함수이므로 함수 호출 기호 '()'를 사용할 수 있다.
doybleAdder(5, double)(3); // 13
```

### 6. 객체나 배열에 대한 디스트럭쳐링 예시를 들 수 있나요?

배열 디스트럭쳐링

```
const foo = ['one', 'two', 'three'];
const one = foo.one;
const ['one', 'two', 'three'] = foo;

let a = 1;
let b = 3;

[a, b] = [b, a];
console.log(a);// 3
console.log(b);// 1
```

객체 디스트럭쳐링

```
const o = {p: 42, q: true};
const { p, q } = o;

```
