# 🍃Callback

[참조1](https://www.youtube.com/watch?v=s1vpVCrT8f4) : 비동기 처리의 시작 콜백 이해하기

<hr>

<br>

1. callback 의 정의

   - "나중에 다시 불러(call)달라 전달하는 함수들" 을 콜백 함수라 한다.
   - sync 와 async 콜백이 존재한다.

   <br>

2. Sync & Async

   - JS는 synchronous 하다. => hoisting 이후 코드가 나타나는 순서대로 동기적으로 실행

   - Hoisting : 변수선언(var) 또는 함수선언이 우선적으로 "제일 위로" 올라가는 것.

   - ```javascript
     // 아래의 결과 : 1 => 2 => 3
     console.log('1');
     console.log('2');
     console.log('3');
     
     // 아래의 결과 : 1 => 3 => (1초 후) 2
     console.log('1');
     setTimeout(() => console.log('2'), 1000);
     console.log('3');
     ```

   - Sync vs Async callback 예시

     ```javascript
     // synchronous callback : 1 => 2
     printImmediately(() => console.log('1'));
     console.log('2');
     function printImmediately(print);
     
     // asynchronous callback : 2 => 1
     printWithDelay(() => console.log('1'), 1000);
     console.log('2');
     function printWithDelay(print, timeout) {
         setTimeout(print, timeout);
     };
     ```

   <br>

3. callback 주의점!

   - 가독성이 너무 떨어진다. 한 눈에 로직 파악이 너무 힘듦, 고로 디버깅 및 유지보수 시 힘들다.

   - callback 지옥 예시

     ```javascript
     userStorage.loginUser(
         id,
         pw,
         user => {
             userWithRole => {
                 alert('hello ${userWithRole.name}, you have a ${userWithRole.role} role');
             },
             error => {
                 console.log(error);
             },
         },
         error => {
             console.log(error);
         }
     ); 
     ```

   - 고로 조금 더 병렬적으로, 효율적으로 코딩 필요 => Promise 혹은 Async await 활용!