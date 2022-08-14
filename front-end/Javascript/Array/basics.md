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

   - 마음만 먹으면 `Array`도 `Object`처럼, 그리고 이의 반대로도 활용이 가능하지만, 
     각기 다른 방향으로 최적화되어있기 떄문에, 상황에 따라 알맞는걸 선택해 활용하는걸 추천한다.

   <br>

4. ## Create

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

5. ## Interact

   - 읽기

     ```javascript
     // 배열의 `[]` 연산자는 객체 `property`접근 시 활용되는 `[]`와 동일하게 동작한다.
     
     const a = [1, 2, 3]
     a[1]  // 2번째 원소의 값을 읽는다
     ```

   - 원소 추가하기 (`push`메서드 활용)

     ```javascript
     const a = []
     a.push(1, 2, 3)
     console.log(a)  // [1, 2, 3]
     ```

   - 원소 삭제하기 (`delete` 연산자 활용 (비추천))

     ```javascript
     const a = [1, 2, 3]
     delete a[1]
     console.log(a)  // [1,  , 3]   2가 undefined로 채워졌다.
     a.length  // 고로 length도 3 그대로이다
     ```

     `pop, shift` 메서드 활용

     ```javascript
     const a = [1, 2, 3]
     a.pop()  // returns 3
     console.log(a)  // [1, 2]
     a.shift()
     console.log(a)  // [2]
     ```

   <br>

6. ## Sparse Array

   - 배열에 속한 원소의 위치가 연속적이지 않은 배열이다.

   - 배열의 `length`는 원소의 개수를 의미하지만,
     `Sparse Array`의 경우는 `length`가 원소의 개수보다 항상 크다.

     ```javascript
     const a = new Array(5);  //원소는 없지만 length는 5 이다.
     a[100] = 0  // 하나의 원소를 할당했지만, length가 1001 이 된다
     ```

      