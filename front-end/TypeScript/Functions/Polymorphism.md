# 🐰 Polymorphism

[ref1](https://www.youtube.com/watch?v=u5Kky7DZhq4) : YouTube

---

1. ## what is Polymorphism?

   - denotation : multi-structured, multi-sided
   - using placeholder when writing call signature, for better readability and less-codes.
     TS will replace and make every call signature different depending on the argument's type.
   - very commonly used in external libraries
   
   <br>
   
2. ## examples

   - Bad example

     ```typescript
     // it's pain in the neck to write every call signatures
     type SuperPrint = {
         (arr: number[]): void
         (arr: boolean[]): void
         (arr: string[]): void
         (arr: (number|boolean|string)[]): void
     }
     
     const superPrint: SuperPrint = (arr) => {
         arr.forEach(i => console.log(i))
     }
     
     superPrint([1, 2, 3, 4])  // works
     superPrint([true, false, true])  // works
     superPrint(["a", "b", "c"])  // works
     superPrint([1, 2, true, "a"])  // works
     ```

   - good example : 

     ```typescript
     // use generic (it's like a placeholder for the types, thus act like a dynamic type)
     // TS will replace and make every call signature different depending on the argument's type
     type SuperPrint = {
         <TypePlaceholder>(arr: TypePlaceholder[]): void
     }
     
     const superPrint: SuperPrint = (arr) => {
         arr.forEach(i => console.log(i))
     }
     
     superPrint([1, 2, 3, 4])
     superPrint([true, false, true])
     superPrint(["a", "b", "c"])
     superPrint([1, true, "a"])
     ```

   - good example 2 :

     ```typescript
     // the function is going to receive an array of TypePlaceholder,
     // and it will return one of those TypePlaceholder
     type SuperPrint = {
         <TypePlaceholder>(arr: TypePlaceholder[]): TylePlaceholder
     }
     
     const superPrint: SuperPrint = (arr) => {
         return arr[0]
     }
     
     superPrint([1, 2, 3, 4])
     superPrint([true, false, true])
     superPrint(["a", "b", "c"])
     superPrint([1, true, "a"])
     ```

     
