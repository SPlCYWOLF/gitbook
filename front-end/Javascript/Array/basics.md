# 🌽 basics

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.7 Arrays

___

1. ## What is Array

   - 정렬된 값의 집합이다.
   - 객체의 특별한 형태 : `index`는 정수 `property`값 과도 같다 .

   <br>

2. ## Characteristics

   - 32bit 인덱스를 사용함으로, `0 ~ (2^32 - 2)` 만큼의 인덱스를 사용한다.
     해당 범위를 벗어날 경우, `array`의 `length property`가 갱신되지 않는다.
   - 원소들의 타입이 고정되어 있지 않고, `array`의 타입은 `object` 이다.
   - 배열 리터럴에서 빠진 부분은 `undefined`가 된다.
   - 객체 `property`를 통하는것 보다 `index`를 통한 원소 접근에 최적화 되어있다.
   - 배열을 다루는 여러 `methods` 가 정의되어 있는 `Array.prototype`의 `property`들을 상속 받고,
     이들은 `generic`형태임으로 유사배열객체에서도 활용이 가능하다.

   <br>

3. ## Array vs Object

   - |                                                              | Array |  Object  |
     | :----------------------------------------------------------: | :---: | :------: |
     | `property` 이름으로 `2^32`이하의 양수를 사용할 때, 자동으로 `length property`값이 갱신된다. |   O   |    X     |
     | 존재하지 않는`property` 이름을 읽어오려 하면 에러 없이 `undefined` 값이 반환된다. |   O   |    O     |
     |       음수, 정수 아닌 수들인`property`를 가질 수 있다.       |   O   |    O     |
     |    객체의 `prototype`으로부터 원소들을 상속 받을 수 있다.    |   O   | O (추천) |
     | `getter`, `setter` 메서드를 통해 정의된 원소도 가질 수 있다. |   O   |    O     |
     |                        객체타입 이다.                        |   O   |    O     |

   - 마음만 먹으면 `Array`도 `Object`처럼 활용이 가능하지만, 다른 방향으로 최적화되어있기 떄문에,
     상황에 따라 알맞는걸 선택해 활용하는걸 추천한다.

   <br>

4. ## How to create an Array

   - `literal` 활용 (추천)

     ```javascript
     const a = []	// empty array
     const b = [1, 2, 3]  // comma to distinguish element
     const c = [1+temp, 2+temp]  // also works
     const d = [1, , 3]  // d[1] would be `undefined`
     const e = [1, , ]  // e.length would return 2, not 3, due to the literal rule
     ```

   - `Array()` 생성자 활용

     ```javascript
     const a = new Array();  // equal to []
     const b = new Array(10);  // sets the default `length` property of the Array to 10
     const c = new Array(5, 4, 3)  // equal to [5, 4, 3]
     ```

   <br>

5. ## How to interact with an Array

   - `[]` 연산자를 활용

     ```javascript
     const a = [1, 2, 3]
     a[1]  // 2번째 원소의 값을 읽는다
     ```

   - 배열의 `[]` 연산자는 객체 `property`접근 시 활용되는 `[]`와 동일하게 동작한다.

   - 