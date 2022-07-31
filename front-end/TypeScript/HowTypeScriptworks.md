# 😘 How TypeScript works

[ref1](https://www.youtube.com/watch?v=gprIrVbBx-M) : YouTube

---

<br>

1. ## Definition of TypeScript

   - A JavaScript with syntax for types
   - A strongly typed programming language that builds on JavaScript 

   <br>

2. ## Why use TypeScript

   - protects developer from code errors
     - If the TS compiler detects any error, it won't get compiled into JS,
       thus preventing code errors 

   <br>

3. ## Examples

   - ```typescript
     function divide(a, b) {
         return a / b
     }
     // this function won't work due to the compilor check
     // which detects that it lacks one argument, and the 
     // argument type isn't adequate for this function
     divide("hello")
     ```

