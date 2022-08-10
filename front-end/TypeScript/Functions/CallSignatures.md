# 🏠 Call Signatures

[ref1](https://www.youtube.com/watch?v=FotK-GR0kLI) : YouTube

---

1. ## Quick recap

   - ```typescript
     // very basic way to write a function
     function add(a:number, b:number): number {
         return a + b
     }
     
     // but the function can implicitly know the return type, so can write like this
     function add(a:number, b:number) {
         return a + b
     }
     ```

   - ```typescript
     // basic way to write a function using the arrow function
     // the function implicitly knows the return type
     const add = (a:number, b:number) => a + b
     ```

   <br>

2. ## using the Call Signature

   - can simplify the code by declaring the types of a function prior to implementing the function

   - the Call Signature `doesn't tell how the function is implemented`,
     but `do tell the types of arguments and the return type of the function`.

   - ```typescript
     // type of a call signature of a function
     type Add = (a:number, b:number) => number;
     
     const add:Add = (a, b) => a + b		// TS infers the type of arguments and return type 
     
     // this would cause error because it returns void type
     const add:Add = (a, b) => {a + b}
     ```
