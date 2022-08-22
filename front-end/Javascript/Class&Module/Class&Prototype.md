# 🕋 Class and Prototype

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.9 Class and Module

___

1. ## Relationship between Class & Prototype

   - JS의`Class`란, 같은 `prototype` 객체로부터 `property`를 상속받은 객체의 집합이다.
     고로, `prototype`객체는 `Class`의 핵심이다.
   - 만약 `prototype` 객체를 정의하고, 해당 `prototype`을 상속하는 객체를 생성하기 위해 
     `inherit()`함수를 사용한다면, JS에서는 `Class`를 정의한것으로 본다.

   <br>

2. ## examples

   - 값 범위를 표현하는 클래스를 위한 프로토타입 객체를 정의 후,
     새 인스턴스를 생성하고 초기화하는 factory 함수를 정의하는 예시

     ```javascript
     // range 객체를 반환하는 factory 함수 (클래스 프로토타입 객체를 저장하기 위한 장소!) ↓
     // 각 range 객체에 from & to 프로퍼티는 고유의 상태를 저장하고, 공유 혹은 상속되지 않는다.
     function range(from, to) {
         var r = inherit(range.methods);	// Class를 정의한 시점!
         
         r.from = from;
         r.to = to;
         
         return r;
     }
     
     // 모든 range 객체가 상속하는 매서드를 정의하는 prototype 객체 ↓
     // this를 활용해서 range객체의 from & to 프로퍼티를 참조한다! (this는 매서드의 호출 대상 객체를 가리킴)
     range.methods = {
         includes: function(x) {
             return this.from <= x && x <= this.to;
         },
         foreach: function(f) {
             for(var x = Math.ceil(this.from); x <= this.to; x++) {
                 f(x);
             }
         },
         toString: function() {
             return "(" + this.from + "..." + this.to + ")";
         }
     };
     
     // range 객체를 사용하는 examples
     var r = range(1, 3);	// range 객체를 생성
     r.includes(2);		// true, 2가 범위에 있음
     r.foreach(console.log);	// 1 2 3
     console.log(r);		// (1...3)
     ```