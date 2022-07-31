# 🍠 Types of TypeScript part.2

[ref1](https://www.youtube.com/watch?v=kIb9cXL4SJY) : YouTube

---

1. ## Read-only property

   - allow to make a property as read-only
     thus, TS will prevent the property from mutating.

   - ```typescript
     type Player = {
         readonly name:string
         age?: number
     }
     const playerMaker = (name:string) : Player => ({name})
     const tae = playerMaker("tae")
     // this won't work since name property is read-only
     tae.name = "hun"
     ```

   - ```typescript
     const numbers: readonly number[] = [1, 2, 3, 4, 5]
     // this won't work due to the readonly property
     numbers.push(10)
     ```

   <br>

2. ## Tuple

   - array that requires a minimum length and have specific types in a specific position

   - ```typescript
     // each element in the array must match the tuple type
     const player: [string, number, boolean] = ["1", 1, true]
     
     // with readonly, it is immutable
     const player: readonly [string, number, boolean] = ["1", 1, true]
     player[0] = "2"     // this won't work
     ```

   <br>

3. ## etc types

   - ```typescript
     let a : undefined = undefined   // undefined type
     let b : null = null     // null type
     
     // any type : used only when u want to ignore TS **but not recommended
     let c : any = 10
     let d : any[] = [1, 2, 3, 4]
     ```