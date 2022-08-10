# 🌼 Types of TypeScript part.3

[ref1](https://www.youtube.com/watch?v=alzyYRaLq54) : YouTube

---

1. ## Unknown type

   - use it when we don't know the type of the variable in advance

   - TS force one to check for the type afterwards

   - ```typescript
     let a:unknown;
     
     // this won't work
     let b = a + 1
     
     // this works
     if(typeof a === 'number') {
         let b = a + 1
     }
     // this works
     if(typeof a === 'string') {
         let b = a.toUpperCase();
     }
     ```

   <br>

2. ## Void type

   - functions that don't return anything

   - usually TS implicitly understands void type

   - ```typescript
     // implicit
     function hello() {
         console.log('x')
     }
     
     const a = hello()
     // this won't work because it returns something
     a.toUpperCase()
     ```

   <br>

3. ## Never

   - Not commonly used type

   - when a function never returns, or function throws exception.

   - ```typescript
     // doesn't work because it returns "X"
     function hello():never{
         return "X"
     }
     
     // works because it throws exception and not return anything
     function hello():never{
         throw new Error("X")
     }
     
     // incase the type of argument could be two
     function hello(name:string|number){
         name + 1 // can't do this because name could be string, but check below
         
         if(typeof name === "string"){
             name  // type of name is "string"
         } else if (typeof name === "number"){
             name  // type of name is "number", so 
             name + 1 // this works
         } else {
             name  // type of name is "never", meaning this code will and should never run.
         }
     }
     ```
