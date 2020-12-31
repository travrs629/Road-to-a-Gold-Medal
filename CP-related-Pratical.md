# CP-related-Pratical
## 2020.12.30
**1. How to assign an array size for primitive type?**
   - ans: (for exmaple int)
      - `int[] [arrayName] = new int[[arrraySize]]`
      - `int[] [arrayName] = {...[values]}`
      - `int[] [arrayName] = new int[]{...[values]}`
      - **Remember all array starts from zero.**
      
**2. How to assign an array value afterward?**
   - ans: `[arrayName][[no. of row]][[no. of column]] = [value]`

**3. What does it means by `throw [exception]`?**
   - ans: **Indication that this method might throw one of the listed type exception.**
   - explanation: and thus similar to just ignore it.
   
**4. what is `bufferedwriter` class?**
   - ans: It writes text to character-output stream, buffering characters.
   - exxplanation:
      - Constructor: `BufferedWriter(Writer out, int [size])` Creates a buffered character-output stream.
         - If no size is given, it uses a default output stream.
