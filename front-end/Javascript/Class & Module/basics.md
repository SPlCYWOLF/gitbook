# 🌽 basics

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.9 Class and Module

___

1. ## What is Class

   - a blueprint for creating objects.
   - 많은 경우, 객체끼리 특정 `property (보통 메서드라 함)`를 공유 할 수 있게 `Class`를 정의한다.

   <br>

2. ## Characteristics of JavaScript Class

   - `prototype` 기반의 상속 메커니즘을 기반으로 한다.
     예를들어, 두 객체가 같은 `prototype` 객체로부터 `property`를 상속받았다면,
     둘은 같은 `Class`의 `instance`이다.
   - `Java` & `C++` 와 같은 `strong type`기반의 `OOP`언어와는 매우 다르다.
     JS의 `Class`와 `prototype`기반 상속 메커니즘은 `Java` 등의 언어의 `Class`상속과는 상당히 다르다.
   - JS의 `Class`는 동적으로 확장될 수 있고, 자료형의 한 종류로 간주 가능하다.