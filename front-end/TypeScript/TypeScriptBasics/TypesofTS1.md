# 🏈 Types of TypeScript part.1

[ref1](https://www.youtube.com/watch?v=v5VAIHZpr8o) : YouTube

---

<br>

1. ## Types in TypeScript

   - | Basic types                                                  | Optional types                                               | Alias type | Return type |
     | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- | ----------- |
     | - number   `let a : number = 1`<br />- boolean   `let b : boolean = true`<br />- string   let c : string = "wow"<br />- array   let d : string[] = ["hoho"] | `const player : `{<br/>    `name: string,`<br/>    `age?: number`<br/>}` = {`<br/>    `name: "taehun"`<br/>`}` | see below  | see below   |

   <br>

2. ## Improve type readability (Alias type)

   - ```typescript
     // from this
     const playerTae : {
         name: string,
         age?: number
     } = {
         name: "taehun"
     }
     const playerLynn : {
         name: string,
         age?: number
     } = {
         name: "lynn"
     }
     
     // to this (type Alias)
     type Player = {
         name: string,
         age?: number
     }
     const playerTae : Player = { 
         name: "taehun"
     }
     const playerLynn : Player = {
         name: "lynn"
     }
     
     // maybe to this ;)
     type Age = number;
     type Name = string;
     type Player = {
         name: Name,
         age?: Age
     }
     const playerTae : Player = {
         name: "taehun"
     }
     const playerLynn : Player = {
         name: "lynn"
     }

   <br>

3. ## Improve type readability (Return type)

   - ```typescript
     type Player = {
         name: string,
         age?: number
     }
     // this function accepts string type argument and returns Player type
     function playerMaker(name:string) : Player {
         return name
     }
     
     // I can also do this because the function accepts Player type!
     const taehun = playerMaker("tae")
     taehun.age = 22
     
     // as for the arrow function..
     const playerMaker = (name:string) : Player => ({name})
     ```

   

