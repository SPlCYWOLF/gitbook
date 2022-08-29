# 🔫 Constructor vs Prototype

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.9 Class and Module

___

1. ## constructor recap

   - 새로 생성된 **객체를 초기화하는 용도로 사용**되는 함수이다.
   - 생성자를 호출하면 자동으로 새로운 객체가 생성, 생성자 함수 내부에서 새로 생성된 객체를 사용하기 때문에,
     생성자 함수는 **새 객체의 상태를 초기화 하는것에만 집중**하게 된다.
   - 함수가 생성자로 호출되려면 `prototype` 프로퍼티가 필요하고,
     모든 JS 함수는 생성자로 사용될 수 있다.
     고로, 모든 JS 함수에는 자동으로 `prototype` 프로퍼티가 설정된다. (`Function.blind()`와 같은 예외는 존재!)
   - 생성자의 `prototype` 프로퍼티가 새 객체의 `prototype`으로 사용된다.
     고로, 한 생성자를 통해 생성된 모든 객체는 같은 객체를 상속하고, 이는 곧 같은 `Class`의 멤버임을 뜻한다.
   - 생성자의 프로퍼티는 열거되지 않으며, 생성자 프로퍼티의 값은 해당 함수 객체이다. 

   <br>

2. ## prototype recap

   - 같은 `prototype` 객체로부터 `property`를 상속받은 객체의 집합이 `Class`이며,
     고로, **`prototype`객체는 `Class`의 핵심**이다.
   - `factory`함수의 경우,
     만약 `prototype` 객체를 정의하고, 해당 `prototype`을 상속하는 객체를 생성하기 위해 
     `inherit()`함수를 사용한다면, JS에서는 `Class`를 정의한것으로 본다.

   <br>

3. ## comparison

   - 생성자를 활용하여 클래스를 정의하는 과정에서,
     `constructor` 는 특정 객체를 초기화하는 역할을 맡고,
     `prototype`은 해당 객체의 초기 상태를 정의한다.
     다시말해, 특정 객체가 해당 객체를 상속하게 될 경우, 상속될 메서드 및 프로퍼티를 정의한다는 뜻이다.