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

   <br>

3. ## multiple generic example

   - ```typescript
     type SuperPrint = <T, M>(a: T[], b: M) => T
     
     const superPrint: SuperPrint = (a, b) => a[0]
     
     const a = superPrint([1, 2, 3], "wow")
     ```

   <br>

4. ## react example

   - ```typescript
     // useState function accepts generic
     const [goal, setGoal] = useState<number>()
     ```

   <br>

5. ## real usage examples

   - implement generic with a normal function

     ```typescript
     function superPrint<T>(a: T[]) {
         return a[0]
     }
     
     const b = superPrint<number>([1, 2, 3])  // same as the one below, but 
     const a = superPrint([1, 2, 3])  // letting TS figure out the type is prefered
     ```

   - implement generic with a normal function 2

     ```typescript
     function printAllNumbers(arr: number[]) {
         console.log(arr)
     }
     // they are the same
     function printAllNumbers(arr: Array<number>) {
         console.log(arr)
     }
     ```

   - allow to re-use the type

     ```typescript
     type Player<E> = {
         name: string
         extraInfo: E
     }
     
     const tae: Player<{favFood: string}> = {
         name: "tae",
         extraInfo: {
             favFood: "miso"
         }
     }
     /////////////////////////////////////////////////////////////
     // or
     /////////////////////////////////////////////////////////////
     type Player<E> = {
         name: string
         extraInfo: E
     }
     type LynnPlayer = Player<{favFood: string}>
     
     const tae: LynnPlayer = {
         name: "tae",
         extraInfo: {
             favFood: "miso"
         }
     }
     /////////////////////////////////////////////////////////////
     // or
     /////////////////////////////////////////////////////////////
     type Player<E> = {
         name: string
         extraInfo: E
     }
     type Extra = {
         favFood: string
     }
     type LynnPlayer = Player<Extra>
     
     const tae: LynnPlayer = {
         name: "tae",
         extraInfo: {
             favFood: "miso"
         }
     }
     ```

   <br>

6. ## `any` vs `generic (type placeholder)`

   - any : TS completely abandons it's job
     generic : generate call signatures on demand

   - any cannot detect mistakes, whereas generic can
     example : 

     ```typescript
     type SuperPrint = (a: any[]) => any
     
     const superPrint: SuperPrint = (a) => a[0]
     
     const a = superPrint([1, 2, 3])
     a.toUpperCase()  // this would not work, but the TS cannot detect typeError here
     ```

     ```typescript
     // using generic, TS generates a signature call for the function,
     type SuperPrint = <T>(a: T[]) => T
     
     const superPrint: SuperPrint = (a) => a[0]
     
     // which in this case, TS detects number type arguments and expects number type return value
     const a = superPrint([1, 2, 3])
     a.toUpperCase()  // thus, TS will not allow this
     ```

     
