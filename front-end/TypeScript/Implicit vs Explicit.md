# 🍣 Implicit type vs Explicit type

[ref1](https://www.youtube.com/watch?v=KGKpLTLl5sY) : YouTube

---

<br>

1. ## What's the difference?

   - Let the TS infer the type   **vs**   Directly tell TS what the type should be

   <br>

2. ## Ideal usage

   - Let TS infer the type whenever possible.
     This improves the readability as well as your time.
   - Thus, use Explicit type only when TS cannot infer the type 

   <br>

3. ## Examples

   - ```typescript
     // TS can implicitly infer the type
     let a = "hello"
     let b = false
     const player = {
         name: "wow"
     }
     
     // TS can't infer the type, thus use Explicit type
     let c : number[] = []
     c.push[1]
     ```

