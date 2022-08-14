# 🍟 ES5 methods

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.7 Arrays

---

1. ## forEach()

   - 배열의 각 요소에 대해 `callback`함수를 실행한다.

   - **`return` 값은 없다**.

   - 모든 원소가 순회되기 전에는 종료되지 않는다, 고로 `break`문을 사용할 수 없다.
     하지만, `try`블록 안에서 `forEach`를 호출한다면, `foreach.break`예외를 발생시켜 종료가 가능하다.

   - example

     ```javascript
     const data = [1, 2, 3, 4, 5]
     let sum = 0
     data.forEach(d => sum += d)
     console.log(sum)  // 15
     ```

   <br>

2. ## map()

   - `forEach`와 동일한 형태로 호출되지만, `map`에선 인자로 전달된 함수는 반드시 `return`값이 있어야한다.

   - 기존 배열은 그대로 두고, `callback`함수의 반환값을 요소로 하는 **새로운 배열을 `return`**한다.

   - example

     ```javascript
     const a = [1, 2, 3, 4, 5]
     const b = a.map(x => {
         return x + 3
     })
     console.log(b)  // [4, 5, 6, 7, 8]
     ```

   <br>

3. ## filter()

   - `forEach, map`과 동일한 형태로 호출된다.

   - 콜백 함수의 `return`값이 참인 요소들만을 모아서 **새로운 배열을 반환**한다.
     고로, 해당 매서드에 전달되는 함수는 조건자 함수(`predicate`) 여야한다.

   - example

     ```javascript
     const a = [1, 2, 3, 4, 5]
     const b = a.filter(e => {
         return e > 2
     })
     console.log(b)  // [3, 4, 5]
     ```

   <br>

4. ## every(), some()

   - 각각, 
     배열의 모든 요소가 `predicate`를 통과하면 참을 반환하고,
     배열의 요소중 하나라도 `predicate`를 통과하면 참을 반환한다.

   - 메서드의 `return`값이 결정되면 순회를 종료한다.

   - example

     ```javascript
     const a = [1, 2, 3, 4, 5]
     a.every(e => {
         return e === 3
     })  // false
     a. some(e => {
         return e === 3
     })  // true
     ```

   <br>

5. ## reduce(), reduceRight()

   - 배열의 원소들을 하나의 값으로 결합한다.

   - `callback`함수의 `return`값들을 하나의 값 `acc` 에 누적 후 반환

   - 함수형 프로그래밍에서 토용ㅇ되는 `injdect`와 `fold`연산을 수행한다.

   - 두 메서드의 차이는, 배열의 처음 부터냐 끝 부터냐의 차이다.

   - example

     ```javascript
     const a = [1, 2, 3, 4, 5]
     const sum = a.reduce((acc, n) => {
         return acc + n
     }, 0)  // 초기값 인자이다. 만약 없다면, 처음 들어오는 원소를 초기값으로 자동 할당한다.
     console.log(sum)  // 15
     
     const sumRight = a.reduceRight((acc, n) => {
         return Math.pow(n, acc)  // 거듭제곱 계산이 정렬된 배열에서 거꾸로 누적계산에 좋은 예시다
     })
     ```

   <br>

6. ## indexOf(), lastIndexOf()

   - 배열 원소중에서 특정한 값을 찾는다.

   - 값을 찾으면 해당 원소를, 아니면 `-1`을 `return`한다.

   - 두 메서드의 차이는, 베열의 처음 부터냐 끝 부터냐의 차이다.

   - example

     ```javascript
     const a = [1, 2, 3, 4, 5]
     a.indexOf(1)  // 0을 반환하고 a[0]은 1이다
     a.lastIndexOf(1)  // 3을 반환하고 a[3]은 4이다
     ```

     