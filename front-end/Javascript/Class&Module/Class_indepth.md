# 🐺 Constructor In-depth

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.9 Class and Module

___

1. ## Extending Class

   - JS의 `prototype`기반 상속은 동적이다.

   - 다시말해, 객체가 생성된 이후에 `prototype`이 변경되면, 해당 변경사항을 그대로 상속받는다.

   - 고로, JS 객체에 `prototype`을 활용하여 간단히 `Class`를 확장 시킬 수 있다.

   - ```javascript
     // 이미 정의된 String.trim() 메서드를 재정의한 예시 : 
     String.prototype.trim = String.prototype.trim || function() {
         if (!this) {
             return this;					// 빈 문자열이면 변경x
         };
         return this.replace(/^\s+|\s+$/g, "");	// 정규 표현식을 활용하여 문자열의 시작과 끝의 공백을 제거한 문자열 반환
     }
     ```

   - but!! `Object.prototype`에도 메서드를 추가하여 모든 객체에서 활용 가능하지만, 권장되지 않는다.

     - `ECMAScript5`이전 버전에서는 이렇게 추가된 메서드가 열거되지 않게 할 방법이 없기 때문에,
       해당 행위는 모든 `for in` 루프에서 열거되게 됨으로 권장되지 않는다.
     - 또한, 정의된 클래스를 이렇게 확장 가능한지의 여부는 호스트 환경 (웹 브라우저 등)에 따라 다름으로 이러한 기법은 몸시 제한을 받는다.

   <br>

2. ## Class and Data type

   - 세가지 객체의 클래스를 판단하는 방법 :

     1. ### `instanceof` 연산자

        - ```javascript
          o instanceof c		 // 만약 `o`가 `c.prototype`을 상속한다면, `true`이다.
          					// `o`가 `c.protoype`을 상속한 어떤 객체를 상속한다 해도, `true`이다.
          ```

        - but! 생성자는 클래스를 구별하는 대표수단이지만, 클래스 구별의 핵심은 `prototype`이다.
          고로, 객체의 `prototype`체인에 특별한 `prototype`객체가 있는지를 검사하려 하고ㅡ 생성자 함수를 검사의 기준으로 삼고 싶지 않다면, 
          `isPrototype()`매서드를 대신 사용 가능하다.

        - ```javascript
          // range 클래스가 객체 r의 프로토타입인지를 확인
          range.methods.isPrototypeOf(r)		// range.methods는 프로토타입 객체다
          ```

        - but!! `instanceof`연산자와 `isPrototypeOf()` 메서드는, 오직 주어진 객체와 클래스의 관계만 테스트할 뿐, 어떤 객체의 클래스가 무엇인지 알 수 없다.

     2. ### `constructor` 프로퍼티

        - 생성자는 대표적인 클래스 구별 수단이기 때문에, 비교적 간단한 방법이다.

        - ```javascript
          function typeAndValue(x) {
              if (x == null) return "";	// null과 undefined에는 생성자가 없다.
              switch(x.constructor) {
                  case Number: return "Number: " + x;		// 원시 형식
                  case String: return "String: '" + x + "'";
                  case Date: return "Date: " + x;			// 내장 형식
                  case RegExp: return "Regexp: " + x;
                  case Complex: return "Complex: " + x;	// 사용자 정의 형식
              }
          }
          ```

        - but, 해당 기법도 `instanceof`와 같은 문제를 안고 있다.
          값을 공유하는 여러 실행 컨텍스트(브라우저 창 하나에 여러 프레임이 있는 경우)가 있을때, 해당 기법은 작동하지 않는다.
          이유는, 각 창이나 프레임은 서로 구분되는 실행 컨텍스트고, 각각 자신만의 전역 객체와 생성자 함수의 집합이 있다. 하지만 서로 다른 두 프레임에 생성된 두 배열은 이름은 같지만 별개의 프로토타입 객체를 상속하게된다.
          이는 곧, 하나의 프레임에 만들어진 배열은 다른 프레임에 있는 생성자의 인스턴스가 될 수 없다는 뜻이다.

     3. ### 생성자 이름

        - `instanceof`연산자와 `constructor`프로퍼티를 사용하는 방식의 문제점은, 여러 실행 컨텍스트가 존재하는 상황에서 부각된다.
        - 이에 대한 대안으로서 클래스 식별자로 생성자 함수 대신 그 이름을 사용하는 것이다.
          한 창에 있는 `Array` 생성자는 다른 창에 있는 `Array`생성자와 같지 않지만, 그 이름은 같기 때문이다.
        - but! 이는 `constructor`프로퍼티의 문제점과 같이, 객체에 `constructor`프로퍼티가 없으면 객체의 클래스를 구별할 수 없게된다.