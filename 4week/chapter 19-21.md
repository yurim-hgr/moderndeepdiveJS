# 19장 프로토타입

- 자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결되어 있다. 그리고 이것은 마치 객체 지향의 상속 개념과 같이 부모 객체의 프로퍼티 또는 메소드를 상속받아 사용할 수 있게 한다. 이러한 부모 객체를 **Prototype(프로토타입) 객체** 또는 줄여서 Prototype(프로토타입)이라 한다.
- Prototype 객체는 생성자 함수에 의해 생성된 각각의 객체에 공유 프로퍼티를 제공하기 위해 사용한다.

```jsx
function Circle(raidus){
	this.radius = radius;
}

Circle.prototype.getArea = function() {
	return Math.PI * this.radius ** 2;
}

const circle1 = new Circle(1);
const circle2 = new Circle(2);

console.log(circle1.getArea === circle2.getArea);
```

## 19.3 프로토타입 객체

- 프로토타입 객체 (또는 줄여서 프로토타입) 객체지향 프로그래밍의 근간을 이루는 객체 간 상속을 구현하기 위해 사용된다.

## 19.3.1  __proto__ 접근자 프로퍼티

- 모든객체는 __proto__ 접근자 프로퍼를 통해 자신의 프로토타입, 즉[[Prototype]] 내부 슬롯에 간접적으로 접근할 수 있다.

**프로토타입이 상속을 할수있다라는걸 알려주기위한 빌드업**

**16,17,18**

### __proto__ 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유

- [[Prototype]] 내부 슬롯의 값, 즉 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유는 상호참조에 의해 프로토타입 체인이 생성되는것을 방지하기 위해서다.

## 19.4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

- 프로토타입과 생성자함수는 단독으로 존재할 수 없고 언제나 쌍으로 존재한다.

## 19.5 프로토타입의 생성시점

- 프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다.

## 19.5.1 사용자 정의 생성자 함수와 프로토타입생성시점

- 생성자 함수로서 호출할 수 있는 함수 즉 constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.
- 생성자 함수로서 호출할 수 없는 함수, 즉 non-constructor 는 프로토타입이 생성되지않는다.

## 전역객체

- 표준빌트인 객체인 Object도 전역 객체의 프로퍼티임, 전역객체가 생성되는 시점에 생성.

프로토타입은 쉽게 얘기하면 유전자라고도 볼수있다. 

### call 메서드 (287)

# 20장 Strict mode

- 자바스크립트 언어의 문법을 보다 엄격히 적용하여 기존에는 무시되던 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.
- 전역에 적용한 strict mode는 스크립트 단위로 적용된다.
따라서 strict mode는 즉시실행함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.

## ****5. strict mode가 발생시키는 에러****

### **5.1 암묵적 전역 변수**

선언하지 않은 변수를 참조하면 ReferenceError가 발생한다.

### **5.2 변수, 함수, 매개변수의 삭제**

### **5.3 매개변수 이름의 중복**

중복된 함수 파라미터 이름을 사용하면 SyntaxError가 발생한다.

### **5.4 with 문의 사용**

with 문을 사용하면 SyntaxError가 발생한다.

### **5.5 일반 함수의 this**

strict mode 에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩된다. 생성자 함수가 아닌 일반 함수 내부에서는 this를 사용할 필요가 없기 때문이다. 이때 에러는 발생하지 않는다.

### 5**.6 브라우저 호환성**

IE 9 이하는 지원하지 않는다.

# 21장 빌트인 객체

- 표준빌트인객체
- 호스트객체
- 사용자정의객체

## 21.3 원시값과 래퍼객체

- 래퍼객체: 문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시 객체
- 문자열, 숫자, 불리언, 심벌은 암묵적ㅡ로 생성되는 래퍼객체에 의해 마치 객체처럼 사용할 수 있으며, 표준 빌트인 객체인 String , Number, Boolean, Symbol 의 프로토타입 메서드 또는 프로퍼티를 참조할수있다. 
그래서 생성자함수를 new 연산자와, 함께 호출하여 문자열, 숫자, 불리언 인스턴스를 생성할 필요가 없으며 권장하지도 않는다.

## 21.4 전역객체

- 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체이며, 어떤 객체에도 속하지않은 최상위 객체

### globalThis

- 브라우저 환경과 Node.js 환경에서 전역 객체를 가리키던 다양한 식별자를 통일한 식별자

- 선언하지않은 변수에 값을 암묵적전역  전역 변수가 아니라 전역 객체의 프로퍼티다 
전역함수는 전역 객체의 프로퍼티가 된다

## 21.4.3 암묵적전역

- 선언하지않은 식별자에 값을 할당하면 전역객체의 프로퍼티가된다.
- 변수선언없이 단지 전역객체의 프로퍼티로 추가되었을뿐이다. 변수가아니고 변수호이스팅발생하지않는다.