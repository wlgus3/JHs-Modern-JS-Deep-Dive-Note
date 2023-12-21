# 22 this

## 22.1 this 키워드

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 **자기 참조 변수**이다.

자바스크립트의 함수는 호출시 [arguments](18.md#18.2.1-arguments) 객체와 this를 암묵적으로 전달받는다.&#x20;

자바스크립트의 this는 java 등의 this 키워드와 다르게 작동한다. java에서 this는 인스턴스 자신을 가리키는 참조변수이다.&#x20;

JS의 this는 해당 함수 **호출 방식에 따라 this에 바인딩되는 객체가 달라진다.**

{% hint style="info" %}
\-바인딩 : 식별자와 값을 연결하는 과정. 변수 선언은 변수 이름(식별자)과 확보된 메모리 공간의 주소를 바인딩하는 것.&#x20;
{% endhint %}

```javascript
// 객체 리터럴
const circle = {
  radius: 5,
  getDiameter() {
    // this는 메서드를 호출한 객체를 가리킨다.
    return 2 * this.radius;
  }
};

console.log(circle.getDiameter()); // 10
```

객체 리터럴의 메서드 내부에서는 this가 메서드를 호출한 객체, 즉 circle을 가리킨다.

```javascript
// 생성자 함수
function Circle(radius) {
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  this.radius = radius;
}

Circle.prototype.getDiameter = function () {
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  return 2 * this.radius;
};

// 인스턴스 생성
const circle = new Circle(5);
console.log(circle.getDiameter()); // 10
```

&#x20;생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다. 이처럼 this는 상황에 따라 가리키는 대상이 다르다.&#x20;



this는 어디에서도 참조 가능하다. 전역에서도 함수 내부에서도 참조할 수 있다.&#x20;

```javascript
// this는 어디서든지 참조 가능하다.
// 전역에서 this는 전역 객체 window를 가리킨다.
console.log(this); // window

function square(number) {
  // 일반 함수 내부에서 this는 전역 객체 window를 가리킨다.
  console.log(this); // window
  return number * number;
}
square(2);

const person = {
  name: 'Lee',
  getName() {
    // 메서드 내부에서 this는 메서드를 호출한 객체를 가리킨다.
    console.log(this); // {name: "Lee", getName: ƒ}
    return this.name;
  }
};
console.log(person.getName()); // Lee

function Person(name) {
  this.name = name;
  // 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
  console.log(this); // Person {name: "Lee"}
}

const me = new Person('Lee');
```

하지만 this의 본 목적은 원래 객체의 프로퍼티나 메서드를 참조하기 위함이므로 객체의 메서드 내부, 생성자 함수 내부에서만 의미가 있다. 따라서 strict mode가 적용된 일반 함수 내부의 this에는 undefined가 바인딩된다. 일반 함수 내부에서 this를 사용할 필요가 없기 때문이다.&#x20;





## 22.2 함수 호출 방식과 this 바인딩









