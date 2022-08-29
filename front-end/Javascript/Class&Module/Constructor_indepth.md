# 👾 Constructor In-depth

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.9 Class and Module

___

1. ## Constructor !== Class

   - 두개의 객체가 같은 프로토타입 객체를 상속 == 두 객체는 하나의 클래스의 인스턴스.
   - 서로 다른 두 생성자 함수라도 같은 `prototype` 객체를 가리키는 `prototype`프로퍼티를 가질 수 있다.
     고로, 두 생성자는 같은 `Class`의 인스턴스를 만드는데 사용될 수 있다.
   - 고로, 새로 생성된 객체의 상태를 초기화하는 생성자 함수는 `Class` 구별의 핵심x

   <br>

2. ## Constructor === Class

   - 생성자는 `Class`를 대표하는 역할을 맡는다.

   - 대부분의 생성자 함수 이름은 `Class`이름과 같다.
     ex. : `Range()` 생성자는 `Range`객체를 만든다.

   - 생성자는 객체가 어떤 `Class`에 속한 것인지 `instanceof`연산자로 검사 가능하다.

     ```javascript
     instanceof Range	// r이 Range.prototype을 상속했다면 true
     // r이 Range 생성자에 의해 초기화되었는지 검사 x
     // r이 Range.prototype을 상속하는지 검사 o
     ```

   - But!
     `instanceof`는 생성자를 사용해서 클래스를 구별하도록 강제한다..!

   <br>

3. ## Constructor Property

   - 모든 JS 함수는 생성자로 사용될 수 있고, 함수가 생성자로 호출되려면 `prototype` 프로퍼티가 있어야 한다.
     고로, 모든 JS 함수에는 자동으로 `prototype` 프로퍼티가 설정된다 (일부 제외가 존재한다).

   - 생성자의 프로퍼티는 열거되지 않으며, 생성자 프로퍼티의 값은 해당 함수 객체이다.

     ```javascript
     var F = function() {};	// 이것은 함수 객체이다
     var p = F.prototype;	// 이것은 F와 연관이 있는 프로토타입 객체다
     var c = p.constructor;	// 이것은 프로토타입과 관련한 함수 객체다
     c === F				   // => true   모든 함수에 대해 F.prototype.constructor === F 이다
     ```

   - 위 말인 즉슨,
     미리 정의된 `prototype` 객체가 있다 `+` 해당 `prototype` 객체가 `constructor` 프로퍼티를 가지고 있다 
     `===` 일반적으로 객체는 자기 자신의 생성자를 가리키는 `constructor` 프로퍼티를 상속하고 있다.
     고로,
     생성자는 `Class`를 구별하는데 사용될 수 있고, `constructor` 프로퍼티를 통해 객체의 `Class`를 얻을 수 있다.

     ```javascript
     var o = new F();	// Class F의 객체 o를 생성
     o.constructor === F	// constructor 프로퍼티는 Class를 가리키기 때문에 true를 반환
     ```

   <br>

4. ## Constructor Summary

   - 생성자는 새로 생성된 `객체를 초기화`하는 용도로 사용되는 `함수`이다.
   - 생성자는 `new` 키워드를 사용하여 호출된다.
   - 생성자는 프로퍼티를 부여하기 위한 메서드이고, 객체를 생성할때 자동으로 호출된다.
   - 생성자의 `prototype` 프로퍼티는 새 객체의 `prototype`으로 사용되고,
     고로 한 생성자를 통해 생성된 모든 객체는 같은 객체를 상속하며, 같은 `Class`에 속함을 나타낸다.