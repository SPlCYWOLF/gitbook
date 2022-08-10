# 💣 Overloading

[ref1](https://www.youtube.com/watch?v=RBK1id3iKHg) : YouTube

---

1. ## what is overloading

   - overloading is used when a function has a multiple and different call signatures

   - very often used in external libraries, thus important to understand it

   - quick recap of the call signature

     ```typescript
     // ordinary call signature
     type Add = (a: number, b: number) => nubmer;
     
     // long way of writing call signature
     type Add = {
         (a: number, b: number) : number
     }
     
     const add: Add = (a, b) => a + b
     ```

   - dumb example of overloading

     ```typescript
     type Add = {
         (a: number, b: number) : number	// TS detects how b could be both number or string
         (a: number, b: string) : number
     }
     
     // TS would complain due to the type of b, thus check the below function
     const add: Add = (a, b) => a + b
     
     // by doing this, TS won't complain
     const add: Add = (a, b) => {
         if (typeof b === "string") {
             return a
         } else {
             return a + b
         }
     }
     ```

     <br>

2. ## real-life example of overloading

  - example situation :  where you want to change page in Next.js

  - this is how packages from external libraries are designed

    ```typescript
    // we can send a string or object, to change the page 
    Router.push({
        path: "/home",
        state: 1
    })
    
    .push("/home")
    ```

    ```typescript
    // the overloading for the two ways to change the page
    
    type Config = {
        path: string,
        state: object
    }
    
    type Push = {
        (path: string):void
        (config: Config):void
    }
    
    const push: Push = (config) => {
        if(typeof config === "string") {
            console.log(config)  // cannot return, due to its void type
        } else {
            console.log(config.path, config.state) // if the type of argument is object, can choose 
        }
    }
    ```

    <br>

3. ## Elaboration

  - what happens when there's many different argument numbers?

    ```typescript
    type Add = {
        (a: number, b: number): number
        (a: number, b: number, c: number): number	// means that c is optional
    }
    
    // this won't because we have an extra parameter c, which is optional
    const add: Add = (a, b, c) => {
        return a + b
    }
    
    // thus, we must explicitly mention that parameter c is optional
    const add: Add = (a, b, c?:number) => {
        if(c) {
            return a + b + c
        }
        
        return a + b
    }
    ```

    
