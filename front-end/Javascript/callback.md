# πCallback

[μ°Έμ‘°1](https://www.youtube.com/watch?v=s1vpVCrT8f4) : λΉλκΈ° μ²λ¦¬μ μμ μ½λ°± μ΄ν΄νκΈ°

___



1. callback μ μ μ

   - "λμ€μ λ€μ λΆλ¬(call)λ¬λΌ μ λ¬νλ ν¨μλ€" μ μ½λ°± ν¨μλΌ νλ€.
   - sync μ async μ½λ°±μ΄ μ‘΄μ¬νλ€.

   <br>

2. Sync & Async

   - JSλ synchronous νλ€. => hoisting μ΄ν μ½λκ° λνλλ μμλλ‘ λκΈ°μ μΌλ‘ μ€ν

   - Hoisting : λ³μμ μΈ(var) λλ ν¨μμ μΈμ΄ μ°μ μ μΌλ‘ "μ μΌ μλ‘" μ¬λΌκ°λ κ².

   - ```javascript
     // μλμ κ²°κ³Ό : 1 => 2 => 3
     console.log('1');
     console.log('2');
     console.log('3');
     
     // μλμ κ²°κ³Ό : 1 => 3 => (1μ΄ ν) 2
     console.log('1');
     setTimeout(() => console.log('2'), 1000);
     console.log('3');
     ```

   - Sync vs Async callback μμ

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

3. callback μ£Όμμ !

   - κ°λμ±μ΄ λλ¬΄ λ¨μ΄μ§λ€. ν λμ λ‘μ§ νμμ΄ λλ¬΄ νλ¦, κ³ λ‘ λλ²κΉ λ° μ μ§λ³΄μ μ νλ€λ€.

   - callback μ§μ₯ μμ

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

   - κ³ λ‘ μ‘°κΈ λ λ³λ ¬μ μΌλ‘, ν¨μ¨μ μΌλ‘ μ½λ© νμ => Promise νΉμ Async await νμ©!