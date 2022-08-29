# 👊 Java-style Class

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.9 Class and Module

___

1. ## Overview

   - 자바의 네 가지 멤버 유형을 JS에서도 따라할 수 있다.
     1. `instance field`
     2. `instance methods`
     3. `class fields`
     4. `class methods`
   - but, JS에서 지원하지 않는 JAVA의 특징 :
     1. `instance methods` 안에서 `instance field`를 메서드의 지역변수처럼 사용 가능하다.
     2. `this`를 비롯한 어떤 접두사도 붙일 필요가 없다.
     3. `final`을 사용하여 상수 필드를 정의할 수 있다.
     4. `private`을 활용하여 클래스 내부에서만 사용 가능하도록 `scope`를 정의가능하다.

