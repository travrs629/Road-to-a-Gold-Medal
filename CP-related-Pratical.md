# CP-related-Pratical
##Mathematics
### 2020.12.30
**1. The mid-point formula**
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

**2. maximumDraws(Pigeonhole Principle)**
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
   
**3. handShakes(~Gauss formula)**
   - status: **Success after checking discussion**
   - ans: `[counts]*[values]/2(i.e. no repetition)`
   - explanation:
      - ** no need to assign another variable if the answer could be calculated in `return`.**
      - **If no mathematical theories can be think of, just use your own logic sense.**

**4. lowestTriangle(area of a triangle)**
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

**5. primeCount (distinct prime number & varialbes+arrays' limits)**
   - status: **Failed**
   - ans: 
   ```
   Distinct prime number:

   A pair of distinct prime numbers are primes p,q such that p≠q.

   Multiplying two distinct prime numbers pq together gives a composite number whose prime factorization consists only of two primes. 

   This composite number is divisible by 1,p,q,and pq.

   Variables+Arrays' limits:
   About the array length limits:
   - Java array use an integer as an index to the array.
   - The maximum integer stored by JVM is 2^32 = 2,147,483,647 elements.
   - Storing data in the file has no limits as it stored in the storage drivers but array are stored in JVM.

   ```
      - correct-ans: 
         - Either to manually assign a prime array to deal with the problem and to assign an array of primorials to avoid calculating products of the array, performing an equality test in a loop and output the index of the array.
            - The 16th primorial is larger than 2^64 so have to reduce the 16th primorial to fit into 2^64 but keep it larger than 10^18 limit specified by the question.
            - Primorial = a product of the first n primes.p
         ```
         Java:
         static void countPrimeFactors(long N){
            long primes[] = {2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53};
            // If smaller prime array is used (from 2 to 53), test case 11, 16, 17 would fail.
            // If larger prime array is used (from 2 to 59 or greater), test case 11, 16, 17 would also fail.
            // Passing all test cases is dependent on using Primes array from 2 to 53.
            int count = 0; 
            long pf = primes[0];
                  for(int j = 1; j < primes.length && pf <= N && N != 1; j++){
                      pf = pf * primes[j];
                      count++;
                      }
                  System.out.println(count);  
          } // countPrimeFactors
         ```
         - Or just to calculate maximum primes for every target value (slowest method).
         ```
         C++:
         #include <stdio.h>
         #include <stdlib.h>

         unsigned long long int gcd(unsigned long long int a, unsigned long long int b)
         {

            while (b) {
               unsigned long long int t = b;

               b = a % b;
               a = t;
            }
            return a;
         }

         unsigned int max_unique_primes(unsigned long long int n)
         {
            unsigned int count;
            unsigned long long int prod;
            unsigned long long int prim;

            if (n < 2)
               return 0;

            prod = 2;
            count = 1;
            for (prim = 3; prod * prim <= n; prim += 2) {
               if (gcd(prod, prim) == 1) {
                  prod *= prim;
                  count++;
               }
            }
            return count;
         }

         int main(void)
         {
            unsigned int q;

            if (scanf("%u", &q) != 1)
               return EXIT_FAILURE;

            while (q--) {
               unsigned long long int n;

               if (scanf("%llu", &n) != 1)
                  return EXIT_FAILURE;

               printf("%u\n", max_unique_primes(n));
            }
            return EXIT_SUCCESS;
         }
         ```
   - explanation:
      - The question is asking about what is the maximum factors, that are prime numbers could be found in the corresponding range of n.
      - For example, 3*5*7 = 105, then in the range from 1 to 105, there are at most 3 prime **factors**.
   
**5. connectingTowns(StackOverflowError)**
   - status: **Failed due to soe technique issues**
   - ans: 
      - initial-ans:
      ```
      int r = 1;
      for (int i = 0; i < n - 1; i++) {
         r *= routes[i];
      }
      r %= 1234567;
      return r;
      ```
      - recommended-ans:
      ```
      int r = 1;
      for (int i=0, i < n - 1; i++) {
         r = r*routes[n]%1234567;
      }
      return r;
      ```
   - explanation: 
      - **Remember to initialise all values before using it.**
      - Modulus arthimatic works no matter it is multiple before it or after it.
      - `StackOerflowError`: **Important - May experience multiple times when facing mathematics-related questions.**
         - A runtime error when the amount of call stack memory allocated by JVM is exceeded.
         - A common case is that the call stack exceeds due to excessive deep or infinite recursion.
      - **From now on, every count would be named as `c`.**
   
**6. cuttingSquares(BigInteger)**
   - status: **Failed**
   - ans: `n*m - 1`
   ```
   ```
   - explanation:
      - A single square takes zero cuts.
      - Every time a piece of paper is cut once to become 2 pieces, adding 1 to the total number of pieces.
      - A rectange of n squares takes `n - 1` cuts, adding rows or columns of m squares, the results would be `n*m - 1`.
         - Regarding the n and m, n*m is the area of the target paper, which is also the no. of papers we needed.
   
   
- 7. 
