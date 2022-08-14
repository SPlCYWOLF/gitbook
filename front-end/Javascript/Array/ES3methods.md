# 🚘 ES3 methods

[ref 1](https://www.oreilly.com/library/view/javascript-the-definitive/9781449393854/) : chap.7 Arrays

---

1. ## join()

   - 모든 원소를 문자열로 변환 후, 해당 문자열을 이어 붙인 **새로운 문자열을** `return`

   - `String.split()` 메서드와는 반대의 개념이다.

   - example:

     ```javascript
     const a = [1, 2, 3]
     a.join()  // 1,2,3
     a.join(" ")  // 1 2 3
     a.join("")  // 123
     
     const b = '3 4 5'
     b.split(" ")  // ['3', '4', '5']
     b.split(" ").map(n => {
         return Number(n)
     })            // [3, 4, 5]
     ```

   <br>

2. ## reverse()

   - 배열의 원소 순서를 반대로 뒤집어 `return`한다.

   - 새로운 배열이 아닌, **기존 배열을 수정**한다.

   - example

     ```javascript
     const a = [1, 2, 3]
     a.reverse()  // [3, 2, 1]
     a.reverse().join(" ")  // 3 2 1
     ```

   <br>

3. ## [sort()](https://stackoverflow.com/questions/1063007/how-to-sort-an-array-of-integers-correctly#:~:text=To%20sort%20numerically%20just%20add%20a%20new%20method%20which%20handles%20numeric%20sorts%20(sortNumber%2C%20shown%20below))

   - **기존배열** 안의 원소들을 `Alphabet` 순으로 정렬(수정)하여 `return`한다.

   - `number` 원소는 비교함수 (정렬된 배열에서 어떤게 먼저 나타나야하는지 판단) 를 활용하여 정렬한다.

   - 배열에 `undefined`원소가 존재하면, 이들은 배열의 끝부분으로 정렬된다.

   - example

     ```javascript
     const a = ['c', 'd', 'a']
     a.sort()  // ['a', 'b', 'c']
     
     const b = [5, 2, 10, 1]
     a.sort()  // [1, 10, 2, 5]
     a.sort((a, b) => a - b)  // [1, 2, 5, 10]   전달 인자로
     a.sort((a, b) => b - a)  // [10, 5, 2, 1]   비교함수 활용
     
     const c = ['a', 'c', undefined, 'b']
     c.sort()  // ['a', 'b', 'c', undefined]
     ```

   <br>

4. ## concat()

   - 배열안의 원소들을 꺼내어, 해당 원소들과 메서드의 전달인자와를 합친 **새로운 배열**을 `return`한다.

   - example

     ```javascript
     const a = [1, 2, 3]
     a.concat(4, 5)  // [1, 2, 3, 4, 5]
     a.concat([7, 7])  // [1, 2, 3, 7, 7]
     a.concat(4, [7, [5, 5]])  // [1, 2, 3, 4, 7, [5, 5]]
     ```

      

   <br>

5. ## slice()

   - 배열의 부분 배열을 잘라내어 담은 **새로운 배열**을 `return`한다.

   - 기존 배열은 유지된다

   - 두개의 인자를 받을 수 있고, 각각 배열의 처음과 끝을 명시한다.

   - 전달인자가 음수라면, 거꾸로 생각하면 된다 (마지막 원소부터 -1)

   - example

     ```javascript
     const a = [1, 2, 3, 4, 5]
     a.slice(3)  // [4, 5]
     a.slice(0, 3) // [1, 2, 3]
     a.slice(1, -1) // [2, 3, 4]
     ```

   <br>

6. ## splice()

   - 원소를 삽입 & 제거에 활용되고, 동시에 수행도 가능하다.

   - `splice, concat`와는 다르게 호출 대상 배열을 바로 수정한다.

   - 3개 이상의 인자를 받을 수 있고, 각각 삭제할 원소의 시작점, 삭제할 원소의 개수, 
     이후에는 삭제된 원소의 위치에서 삽입될 원소를 나타낸다.

   - example

     ```javascript
     const a = [1, 2, 3, 4, 5]
     a.splice(1, 3)  // [1, 5]
     a.split(0, 4, 7, [8, 8], 9)  // [7, [8, 8], 9, 5]
     ```

   <br>

7. ## push() , pop()

   - [참고](basics.md)

   <br>

8. ## shift(), unshift()

   - [참고](basics.md)

   <br>

9. ## toString(), toLocaleString()

   - 두 매서드 모두 배열의 모든 원소를 `,` 로 분리한 문자열로 변환한다.
     전달인자 없는 `join()`메서드와 동일한 결과이다. 

   - 해당 문자열은 대괄호, 배열 값의 종류를 구분하는 구분자(delimiter)를 포함하지 않는다.

   - 두 매서드간의 차이점은, 후자가 지역화된 구분자 문자열(separator string)로 반환한다.

   - example

     ```javascript
     const a = [1, 2, 3]
     a.toString()  // '1,2,3'
     const b = [1, [2, 'c']]
     b.toString()  // '1,2,c'
     ```

     