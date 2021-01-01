# CP-related-Pratical
##Mathematics
### 2020.12.30
1. The mid-point formula
- status: **Success after checking discussion**
- ans: `mid-point = (first-coordinate + second coordinate) / 2`
   - `one-of-the-coordinate = 2*mid-point - the-other-of-the-coordinate`
   - initial-ans:
   ```
   int rx = Math.abs(qx - px) + qx;
   int ry = Math.abs(qy - py) + qy;
   int[] r = {rx, ry};
    	
   return r;
   ```
   - correct-ans:
   ```
   int rx = 2*qx - px;
   int ry = 2*qy - py;
   int[] r = {rx, ry};
    	
   return r;
   ```
- explanation:
   - The question requires us to find another point named r such that q would be the mid-point.
   - My initial ans is somhow close to the mid-point formula, but however I choose to use `Math,.abs()` method.
   - Absoultely no need to consider the positive or negative.
   - **It is more a problem that I am not using mathematical methods to think of the question first.**
   - **From now on, all scanners are named as `ky`.

2. maximumDraws(Pigeonhole Principle)
- status: **Sucuss**
- ans: `n = km + 1`
```
Pigeonhole Principle: n = km + 1 or k = (n - 1)/m
If n items are put into m containers, with n>m, then at least one container must contain more than one item.
For example, people in London = n, no. of hairs = m.

for natural numbers k and m, if n=km+1 objects are distributed among m sets, then the pigeonhole principle asserts that at least one of the sets will contain at least k+1 objects.
For example, no. of pairs of socks = n, pulls out a sock = m

Similar to n = object and m = evaluator (something that evaluates(or "contains") the n).
```
- explanation: **From now on, all return variables are named as `r`.**
   
3. handShakes(~Gauss formula)
- status: **Success after checking discussion**
- ans: `[counts]*[values]/2(i.e. no repetition)`
- explanation:
   - ** no need to assign another variable if the answer could be calculated in `return`.**
   - **If no mathematical theories can be think of, just use your own logic sense.**

4. lowestTriangle(area of a triangle)
- status: **Success after numerous tries**
- ans: The problem is that whenever `int` types perform division, it would throw away the remainder.
   1. Either to turn the `int` type into `float`(or `double`) (even just for the dividend).
   2. Or to add `1` or `0` after the division.
   3. Or to force the `int` division to be `rounded-up`.
   - initial ans: 
   ```
   int h = (int)Math.ceil(2*a/b)
   return ;
   ```
   - correct-ans:
   ```
   C++:
   int main() {
   uint32_t a, b;
   cin >> b >> a;
   cout << 2 * a / b + bool((2 * a) % b);   
   return 0;
   }
   C++/Java:
   int lowestTriangle(int base, int area){
   // Complete this function
   return (area * 2 + (base - 1)) / base; // To make it become ceil value
   }
   Java(recommended for me):
   height = (int)Math.ceil((2.0*area)/base);
   ```

- explanation:
   - The area `a` is just the minimum number, but bigger area could be used.
   - **Constructors and methods cannot be used in a `return`.**
   - **All booleans are named as `rw` from now on.**
