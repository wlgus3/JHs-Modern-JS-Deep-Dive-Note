# 15 let, const 키워드와 블록 레벨 스코프

## &#x20;15.1 var 키워드로 선언한 변수의 문제점&#x20;

ES5 까지 변수를 선언하는 유일한 방법은 var 키워드를 사용하는 것이었으며, var의 여러 특징 때문에 여러 문제가 발생했다. 다음은 var 키워드의 문제점들이다.&#x20;

### 15.1.1 변수 중복 선언 허용

var 키워드는 중복 선언을 허용하기 때문에 변수가 이미 선언되어 있는 것을 모르고 중복으로 선언하면서 값까지 할당하면 의도치 않게 변수 값이 변경되는 부작용이 발생

### 15.1.2 함수 레벨 스코프

var 키워드는 \[함수 레벨 스코프]를 따르기 때문에 오로지 함수의 코드 블록만을 지역 스코프로 인정한다. 따라서 의도치 않게 지역변수가 중복 선언되는 경우가 발생.

### 15.1.3 변수 호이스팅

var 키워드는 변수 호이스팅을 지원한다. 따라서 변수 **할당문** **이전**에 변수를 참조해도 undefined를 뱉어낼 뿐 에러를 발생시키지는 않는다. 이는 프로그램 흐름에 맞지 않고 가독성을 떨어트리는 부작용이 있다.



## 15.2 let 키워드

앞서 살펴본 var 키워드의 단점을 보완하기 위해서 ES6에서 let 키워드와 const 키워드를 도입한다. 다음은 let 키워드의 특징이다.&#x20;

### 15.2.1 변수 중복 선언 금지

let 키워드는 이름이 같은 변수를 중복 선언하면 Syntex Error가 발생한다.&#x20;

### 15.2.2 블록 레벨 스코프

var 키워드는 함수 레벨 스코프를 따른다. 하지만 let 키워드는 모든 코드 블록 (함수 , if , for , while, try/catch 등)을 지역 스코프로 인정하는 \[블록 레벨 스코프]를 따른다.&#x20;

### 15.2.3 변수 호이스팅

let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작한다.&#x20;

```javascript
console.log(foo); // ReferenceError: foo is not defined
let foo;
```

let 키워드는 변수 선언문 이전에 참조하면 참조 에러 (ReferenceError)를 발생한다. (원래 호이스팅시 =undefined)

<mark style="color:purple;">var 키워드는 런타임 이전에 JS엔진에 의해  '변수 선언'과 '변수 초기화' 단계가 한 번에 진행</mark>된다.&#x20;

이에 반해&#x20;

<mark style="color:purple;">let 키워드는 '선언 단계'와 '변수 초기화' 단계가 분리되어 진행</mark>된다. 런타임 이전에 JS엔진에 의해 '선언 단계'는 먼저 이루어지지만, '초기화 단계'는 변수 선언문에 이르러서야 '초기화 단계 ' -> '할당 단계' 순서로 진행된다.&#x20;

따라서 스코프 시작부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 **\[일시적 사각지대]Temporal DeadZone;TDZ** 라고 부른다.

### 15.2.4 전역 객체와 let

var 키워드로 선언한 전역변수와 전역 함수, 그리고 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역 객체 window의 프로퍼티가 된다.&#x20;

```javascript
// 이 예제는 브라우저 환경에서 실행해야 한다.

// 전역 변수
var x = 1;
// 암묵적 전역
y = 2;
// 전역 함수
function foo() {}

// var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티다.
console.log(window.x); // 1
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(x); // 1

// 암묵적 전역은 전역 객체 window의 프로퍼티다.
console.log(window.y); // 2
console.log(y); // 2

// 함수 선언문으로 정의한 전역 함수는 전역 객체 window의 프로퍼티다.
console.log(window.foo); // ƒ foo() {}
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(foo); // ƒ foo() {}
```

하지만 let 키워드로 선언한 전역변수는 전역객체의 프로퍼티가 아니다. 따라서 window.foo와 같이 접근할 수 없다.



## 15.3 const 키워드

const 키워드는 상수constant를 선언하기 위해서 사용한다. 하지만 반드시 상수만을 위해서 사용하지는 않는다. const의 특징은 let과 거의 유사하며 차이점 위주로 정리한다.

### 15.3.1 선언과 초기화&#x20;

const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화 해야한다.

```javascript
const foo = 1;
//그렇지 않으면 아래와 같은 에러발생
const foo; // SyntaxError: Missing initializer in const declaration
```

const 키워드는 let과 동일하게 **\[블록 레벨 스코프]**를 가지며, **호이스팅이 발생하지 않는 것처럼 동작**한다.&#x20;

### 15.3.2 재할당 금지&#x20;

var , let과는 다르게 const는 재할당이 금지된다.

### 15.3.3 상수&#x20;

const 키워드로 선언한 변수에 **원시 값**을 할당한 경우 **변수 값을 변경할 수 없다.**&#x20;

변수의 상대개념인 **'상수'**는 **재할당이 금지된 변수**를 말한다.&#x20;

{% hint style="danger" %}
const 키워드로 선언된 변수에 **원시 값을 할당한 경우 원시값은 변경할 수 없는 값 immutable value**이고 const 키워드에 의해 재할당이 금지되므로 **할당된 값을 변경할 수 있는 방법은 없다.**
{% endhint %}

일반적으로 상수 이름은 대분자로 선언해서 상수임을 명확히 나타내고 스네이크 케이스로 표현한다.

```javascript
// 세율을 의미하는 0.1은 변경할 수 없는 상수로서 사용될 값이다.
// 변수 이름을 대문자로 선언해 상수임을 명확히 나타낸다.
const TAX_RATE = 0.1;

// 세전 가격
let preTaxPrice = 100;

// 세후 가격
let afterTaxPrice = preTaxPrice + (preTaxPrice * TAX_RATE);

console.log(afterTaxPrice); // 110
```

### 15.3.4 const 키워드와 객체

const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다.

{% hint style="danger" %}
const 키워드는 재할당을 금지할 뿐 불변을 의미하지는 않는다. 따라서 객체를 변경하는 것은 가능하다.
{% endhint %}



## 15.4 var  vs.  let  vs.  const

{% hint style="success" %}
**변수 선언에는 기본적으로 const를 사용**하고 **let은 재할당이 반드시 필요한 경우**에 **제한적으로 사용**하는 것이 좋다. const는 의도치 않은 재할당을 방지하기에 더 안전하다.
{% endhint %}

* ES6를 사용한다면 **var은 사용하지 않는다.**
* 변수를 선언하는 시점에는 재할당이 필요한지 잘 모르는경우가 많다. 따라서 **일단 const를 사용하고 반드시 재할당이 필요하다는 것이 확인될 때 const를 let으로 바꾸어도 늦지 않다.**&#x20;

