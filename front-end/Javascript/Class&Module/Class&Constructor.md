# 🎺 Class and Constructor

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.9 Class and Module

___

1. ## what is a Constructor

   - 새로 생성된 객체를 초기화하는 용도로 사용되는 함수이다.
   - 생성자를 호출하면 자동으로 새로운 객체가 생성, 생성자 함수 내부에서 새로 생성된 객체를 사용하기 때문에,
     생성자 함수는 새 객체의 상태를 초기화 하는것에만 집중하게 된다.
   - 함수가 생성자로 호출되려면 `prototype` 프로퍼티가 있어야하는데,
     모든 JS 함수는 생성자로 사용될 수 있다.
     고로, 모든 JS 함수에는 자동으로 `prototype` 프로퍼티가 설정된다. (`Function.blind()`와 같은 예외는 존재!)

   <br>

2. ## characteristics

   - 생성자의 `prototype` 프로퍼티가 새 객체의 `prototype`으로 사용된다.
     고로, 한 생성자를 통해 생성된 모든 객체는 같은 객체를 상속하고, 이는 곧 같은 `Class`의 멤버임을 뜻한다.
   - 생성자의 프로퍼티는 열거되지 않으며, 생성자 프로퍼티의 값은 해당 함수 객체이다. 

   <br>

3. ## examples

   - 생성자 함수를 사용하여 `range`객체 생성하기

     ```javascript
     // 새 Range 객체를 초기화하는 생성자 함수 ↓
     // 이 함수는 어떤 객체도 내부에서 생성하고 반환하지 않는다. 그저 this 를 초기화 할 뿐..
     function Range(from, to) {
         this.from = from;
         this.to = to;
     }
     
     // 모든 Range 객체는 이 객체를 상속한다!
     // 다른 모든 객체가 이 객체를 상속하려면, property 이름이 반드시 "prototype" 이어야한다.
     Range.prototype = {
         includes: function(x) {
             return this.from <= x && x <= this.to;
         },
         foreach: function(f) {
             for (var x = Math.ceil(this.from); x <= this.to; x++) {
                 f(x);
             }
         },
         toString: function() {
             return "(" + this.from + "..." + this.to + ")";
         }
     }
     
     // range 객체를 사용하는 examples
     var r = new Range(1, 3);	// range 객체를 생성
     r.includes(2);		// true, 2가 범위에 있음
     r.foreach(console.log);	// 1 2 3
     console.log(r);		// (1...3)
     ```

   - 생성자의 프로퍼티는 열거되지 않으며, 생성자 프로퍼티의 값은 해당 함수 객체이다.

     ```javascript
     var F = function() {};	// 이것은 함수 객체이다
     var p = F.prototype;	// 이것은 F와 연관이 있는 프로토타입 객체다
     var c = p.constructor;	// 이것은 프로토타입과 관련한 함수 객체다
     c === F				   // => true   모든 함수에 대해 F.prototype.constructor === F 이다
     ```

   <br>

4. ## factory function vs constructor

   ### difference

   - 생성자는 new 키워드를 사용하여 호출되기 때문에, inherit() 등 새 객체 생성을 위해 어떤 별도의 행동도 필요없다.
   - 생성자는 그저 새 객체를 초기화하면 됨으로, 생성된 객체를 반환할 필요도 없다.
   - 생성자를 `new` 키워드 없이 호출은 불가능하다.
   - 일반 함수와 메서드는 소문자로 작명하지만, 생성자는 항상 첫글자를 대문자 처리한다 (국룰).

   - ```javascript
     // 호출 방법의 차이
     var r = range(1, 3);  // factory function
     var r = new Range(1, 3)  // constructor
     
     // prototype 객체의 이름을 짓는 방법에 차이
     range.methods = {
         ...
     }
     Range.prototype = {
         ...
     }
     ```

   ### similarity

   - 하지만!
     `factory`함수와 `constructor`로 정의된 `range`와 `Range`의 메서드들은 두 클래스 모두 같은 방식으로 정의되고 호출된다.