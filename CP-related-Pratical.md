# CP-related-Pratical
##Mathematics
### 2020.12.30
**1. indPoint(The mid-point formula)**
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

## 2021.01.02
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
   - status: **Failed due to some technique issues**
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

## 2021.01.03
**6. cuttingSquares(BigInteger)**
   - status: **Failed**
   - ans: `n*m - 1`
      - correct-ans:
      ```
      Dealing with large integers:
      
      Java(Understandable solution):
      
      static long solve(int n, int m) {
         return BigInteger.valueOf(n).multiply(BigInteger.valueOf(m)).longValue()-1;
      }
      
      Java(Intersting solution):

      public class Solution {

          public static void main(String[] args) {
              Scanner in = new Scanner(System.in);
              long m = in.nextLong();
              long n = in.nextLong();
              long cuts = m*n-1;
              System.out.println(cuts);
          }
      }
      
      public class Solution {

          public static void main(String[] args) {
              Scanner in = new Scanner(System.in);
              int n = in.nextInt();
              int m = in.nextInt();
              long result = (long)n*(long)m;
              System.out.println(result - 1);
          }
      }
      ```
   - explanation:
      - A single square takes zero cuts.
      - Every time a piece of paper is cut once to become 2 pieces, adding 1 to the total number of pieces.
      - A rectange of n squares takes `n - 1` cuts, adding rows or columns of m squares, the results would be `n*m - 1`.
         - Regarding the n and m, n*m is the area of the target paper, which is also the no. of papers we needed.
      - The problem is with the multiplication of the inputs, which is in `int` type.
         - The multiplication of `int` types overflows, which starts again from its minimum limit.
         - If any one of the inputs (either `n` or `m` is casted to `long`), the problem could be prevented.
   
**7. movingTiles(Velocity + RunTimeError + Math.cos())**
   - status: **Success after father's help and checking discussion**
   - ans: 
      - `Velocity = Displacement / Change-in-Time`
      - `Area = (x1 - x2) * (y1 - y2) [in time i]`
         - `Area = (l - 0) * (l - 0) [in time 0]`
         - `Area = ((l + s1*cos(45[degree])*i) - s2*cos(45[degree]*i)) * ((l + s1*cos(45[degree])*i) - s2*cos(45[degree]*i))`
         - `Area = (l + (s1 - s2)*cos(45[degree]*i))`
         - `r[i] = Math.abs((Math.sqrt(queries[i]) - l) / ((s1 - s2)*Math.cos(Math.toRadians(45))));`
      - preferred-ans: The given-codes have runtime problem that have to be solved manually.
      ```
      Java:
      import java.io.*;
      import java.math.*;
      import java.text.*;
      import java.util.*;
      import java.util.regex.*;

      public class Solution {

          /*
           * Complete the movingTiles function below.
           */
          static double[] movingTiles(int l, int s1, int s2, long[] queries) {
              /*
               * Write your code here.
               */
               double[] r = new double[queries.length];
               for(int i = 0; i < queries.length; i++) {
                  r[i] = Math.abs((Math.sqrt(queries[i]) - l) / ((s1 - s2)*Math.cos(Math.toRadians(45))));
               }
               return r;
          }

          private static final Scanner scanner = new Scanner(System.in);

          public static void main(String[] args) throws IOException {
              BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

              String[] lS1S2 = scanner.nextLine().split(" ");
              scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])*");

              int l = Integer.parseInt(lS1S2[0]);

              int s1 = Integer.parseInt(lS1S2[1]);

              int s2 = Integer.parseInt(lS1S2[2]);

              int queriesCount = scanner.nextInt();
              scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])*");

              long[] queries = new long[queriesCount];

              for (int queriesItr = 0; queriesItr < queriesCount; queriesItr++) {
                  long queriesItem = scanner.nextLong();
                  scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])*");
                  queries[queriesItr] = queriesItem;
              }
            
              double[] result = movingTiles(l, s1, s2, queries);

              for (int resultItr = 0; resultItr < result.length; resultItr++) {
                  bufferedWriter.write(String.valueOf(result[resultItr]));

                  if (resultItr != result.length - 1) {
                      bufferedWriter.write("\n");
                  }
              }

              bufferedWriter.newLine();

              bufferedWriter.close();

              scanner.close();
          }
      }
      ```
   - explanation:
      - We have to calculate `i` given the target area, but for simplicity, we just construct a area formula first.
      - `qi` is the target area that we want to calculate, and thus the information we need to find out is the top right point of the square with lower velocity and the bottom left point of the other square with higher velocity.
      - Noticeably, The overlapping area of tiles would become smaller and smaller.
         - Consider the absolute value of the difference in velocities, we get the relative velocity.
         - The velocity is restricted to an angle of 45, which then we evaluate it as cos45 or sin45.
         - The `Math.cos()` receives input of radian instead of degree, which we need a transformation using `Math.toRadian()`.
      - **The `int` data type is often unreliable with mathematical calculations, `long` or `BigInteger` is preferred more.
      - **For all arrays with for loops used, the i should be set at 0 with only "<" used as the condition.**

## 2021.01.04
**8. bestDivisor**
   - status: **Success after checking discussion**
   - ans:
      - initial-ans:
      ```
      static int bestDivisor(int[] in){
         int r = in[0];
         int rsum = 1; 
         int tm = 0;

         for (int i = 1; i <= in.length; i++) {
            for (int j = 5; j >= 1; j--) {
               tm += in[i] / Math.pow(10, j);
            }
            if(rsum < tm) {
               r = in[i];
               rsum = tm;
            } else if (rsum == tm) {
               if (r > in[i]) {
                  r = in[i];
                  rsum = tm;
               } 
            }
         }
         return r;
      }
	
      static int[] allDivisor(int n) {
         int[] r = new int[n/2];
         int k = 0;
         boolean fg = true;
         for (int i = 1; i <= n/2; i++) {
            if(n % i == 0) {
               for (int j = 0; j < r.length; j++) {
                  if(i == r[j]) {
                     fg = false;
                     break;
                  }
               }
               if (fg == true) {
                  r[k] = i;
                  r[k+1] = n / i;
                  k += 2;
               }
            }
         }
         return r;
      }
      ```
      - correct-ans:
      ```
      Java:
      import java.io.*;
      import java.math.*;
      import java.security.*;
      import java.text.*;
      import java.util.*;
      import java.util.concurrent.*;
      import java.util.regex.*;

      public class bestDivisor {

          private static final Scanner scanner = new Scanner(System.in);

          public static void main(String[] args) {
              long n = scanner.nextLong();
              scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
              scanner.close();

              long tm = 0, rsum = 0, r = 0;
              long s = 0;
              for (long i = 1; i <= n; i++) {
                  if (n%i == 0) {
                     tm = i;
                     for (int j = 5; j >= 1; j--) {
                        s += tm % Math.pow(tm, j);
                     }
                      while (tm != 0) {
                          s += tm%10; // Even if tm is really big(for example 1200), tm % 10 would always be 0.
                          tm /= 10;
                      }
                      if (s > rsum) {
                          rsum = s;
                          r = i;
                      } else if (s == rsum) {
                          if (r > i) {
                              r = i;
                          }
                      }
                  }
                  s = 0;
              }
              System.out.println(r);
          }
      }
      
      Java:
      import java.io.*;
      import java.math.*;
      import java.security.*;
      import java.text.*;
      import java.util.*;
      import java.util.concurrent.*;
      import java.util.regex.*;

      public class bestDivisor {

          private static final Scanner scanner = new Scanner(System.in);

          public static void main(String[] args) {
              long n = scanner.nextLong();
              scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
              scanner.close();

              long tm = 0, rsum = 0, r = 0;
              long s = 0;
              for (long i = 1; i <= n; i++) {
                  if (n%i == 0) {
                     tm = i;
                     for (int j = 5; j >= 1; j--) {
                        s += tm % (int)Math.pow(tm, j);
                     }
                     if (s > rsum) {
                          rsum = s;
                          r = i;
                      } else if (s == rsum) {
                          if (r > i) {
                              r = i;
                          }
                      }
                  }
                  s = 0;
              }
              System.out.println(r);
          }
      }
      The only difference above is the loop that adds up the digits, which one uses a for-loop and one uses a while loop.
      It is more suitable to use the while loop, as the for loop can not produce the correct digits as it is changed to long type instead of int type.
      ```
   - explanation:
      - **The inputs inside and outside of a method can be the same in competitive programming.**
      - **Some methods are self-designed and some are pre-designed, but both of them are methods(seems obvious but actually no).**
      - **Add space between the name of methods and constructors and the brackets.**
      - **Remember the variable to be assigned must be put to the left of the equality.**
      - **Boolean flag would be set as `fg` from now on.**
      - **`break` terminates the current loop statement and move on to the next line of codes.**
      - **All inputs for methods would be called `in` if `r` is used.**
      - **All outputs for methods would be called `ot` if `r` is used.**
      - **All smaller variables after should be set with the bigger one with the last vocab.**
      - **The temperary variable from now on would be called `tm`.**
      - **A blank class should be set so to test out small problems in competitive programming(as a beginner).**
      - **If a number cannot be divisible for another number, the output would be 0.**
      - ** Keep the codes as simple as possible.**
      - **Never use `int` to do mathematical questions, use `long` instead.**
      - **Competitive programming is about finding the most efficient way to finish the task. That's it.**
      - **Remember if any `double` type is used, the `int` calculation would become `double`, which the remainder removal is not applied to the calculation anymore.**

## 2021.01.05
**9. restaurant（Greatest Common factor）**
   - status:
   - ans: `GCD = the largest postive integer that divides each of the integer.`
      - initial-ans:
      ```
      int os = l*b;
    	int rLen = 0;
    	
    	if (l == b) {
    		return 1;
    	} else {
    		for (int i = 1; i < l || i < b; i++) {
    			if (os % (int)Math.pow(i, 2) == 0) {
    				if (i > rLen) {
    					rLen = i;
    				}
    			}
    		}
    	}
    	int r = os / (int)Math.pow(rLen, 2);
    	return r;
      ```
      - correct-ans:
      ```
      int os = l*b;
    	int gcd = 0;
    	
    	if (l == b) {
    		return 1; //gcd = l or b
    	} else {
    		for (int i = 1; i < l || i < b; i++) {
    			if ((l %i == 0) && (b % i == 0)) {
    				if (i > gcd) {
    					gcd = i;
    				}
    			}
    		}
    	}
    	int r = os / (int)Math.pow(gcd, 2);
    	return r;
      ```
   - explanation:
      - Greatest factor of a number does not equal to the greatest common factor of two numbers, even if those two number multiplies and become that number.
         - Instead, the greatest number of that number must be one of the two numbers, which is definitely not the target number.
      - The method I used is problematic, after testing of changing to other variable types. But why?

## 2021.01.06
**10. reverseGame**
   - status: **Success after checking hints**
   - ans: `last index = (n - 2 + n % 2)/2 = original middle number of the list`
      - initial-ans:
      ```
      int r = 0;
      if ((n - 1) % 2 == 0) { // n = even number
      		if (k >= (n - 1)/2 + 1) {
            		r = ((n - 1) - k) * 2;
            	} else {
            		r = k*2 + 1;
            	}
            } else { // n = odd number
            	if (k >= (n - 1)/2) {
            		r = ((n - 1) - k) * 2;
            	} else {
            		r = k*2 + 1;
            	}
      }
      System.out.println(r);
      ```
      - correct-ans:
      ```
      Java:
      Breaking the formula inito two parts:
      int r = 0;
            
      if (k >= (n - 1) - k) {
            	r = 2*((n - 1) - k);
      } else {
            	r = 2*k + 1;
      }
      System.out.println(r);
      
      Java:
      int r = 0;
      if (n % 2 == 0) { // n = even number
      		if (k >= (n - 1)/2 + 1) {
            		r = ((n - 1) - k) * 2;
            	} else {
            		r = k*2 + 1;
            	}
            } else { // n = odd number
            	if (k >= (n - 1)/2) {
            		r = ((n - 1) - k) * 2;
            	} else {
            		r = k*2 + 1;
            	}
      }
      System.out.println(r);
      ```
      - **How to output multiple inputs:**
      ```
      private static final Scanner scanner = new Scanner(System.in);
      
      public static void main(String[] args) throws IOException {
      	BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int t = scanner.nextInt(); // t = the pairs of input that received.
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])*"); // String that have to be skipped.

        for (int tItr = 0; tItr < t; tItr++) {
	 // The assignment of the array and other variables happens according to the no. of t.
	 // The assignment, calculation and stdout happens multiple times.
            String[] lb = scanner.nextLine().split(" "); 
            scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])*");

            int l = Integer.parseInt(lb[0]);

            int b = Integer.parseInt(lb[1]);

            int result = restaurant(l, b);
	    
	    // The bufferedWriter methods could be replaced by System.out.println(result) in multiple situations.
            bufferedWriter.write(String.valueOf(result));
            bufferedWriter.newLine();
        }
	 // The closure of bufferedWriter and scanner must be located after the iteration.
        bufferedWriter.close();

        scanner.close();
      }
      ```
   - explanation:
      - **The most important thing about mathematics is about finding out the principles of data, which some of them is found decades ago with generalisation performed, some of them has to be found out by yourself.(In condition of competitive programming.)**
      - **From now on, all array would be named as `arr`.**
      - The question asked for the position of ball numbered `k` instead of the ball at position `k`.
      - **Be careful of outputing the inputs, which could be more than one. If the question did not provide enough codes, you may have to write it yourself.**
      - **From now on, the iteration of pairs of inputs is named as `titr` which stands for `iterations of t`.**
      - `n` only indicates the no. of each numbers, but the actuall max. number is `n - 1`.
      - There is two formula(two trends) in this question and we must find a way to decide whether the input number belongs to which formula.
         - Either by finding whether the number is bigger or smaller to the major part of the range from 1 to n: `k >= (n - 1) - k`
	 - Or by finding whether the no. belongs to the part larger or smaller than the middle number of the range from 1 to n, with the fidnings of whether the number range is even or odd: `n % 2 == 0`
	 - Tho actually the actual range is from 0 to n-1.
	 
**11. strangeGrid**
   - status: **Success after multiple tries**
   - ans: Just find out the relationship of each rows and columns respectively.
      - Just like how we learnt before.
   - explanation:
      - **If the data type of `parse[datatype]()` is changed, the data type before it should also be changed.**
         - e.g. `Integer.parseInt()` should be changed to `Long.parseLong()`

## 2020.01.07
**12. lights(Combination formula)**
   - status: **Success after listing out conditions**
   - ans: `nCr = n!/((n-r)!*r!)`
      - intial-ans:
      ```
      long r = 0;
      for (long i = 1; i <= n; i++) {
    		r += factorials(n) / (factorials(n - i) * factorials(i)) % 100000;
    	}
    	return r;
     }
    
     static long factorials(long n) {
    	if (n == 0) {
    		return 1;
    	}
    	return n*factorials(n-1);
      }
      ```
      - correct-ans: `Math.pow(2, n)`
      ```
      long r = 1;
      for (long i = 1; i <= n; i++) {
      	r = r*2 % 100000;
      }
      return r - (1 % 100000);
      ```
   - explanation:
      - The original answer takes too much memory and produces a `runtime error`.
         - Both the memory size and the time must have been considered to prevent `overflow`.
      - The question could be thought of an much easier way: `Math.pow(2, n)`.
      
**13. divisors**
   - status: **Failed**
   - ans:
      - intial-ans:
      ```
      int r = 0;
      for (long i = 1; i <= n; i++) {
      	 if (n % i == 0) {
    	    if (i % 2 == 0) {
    	       r += 1;
    	    }
    	 }
      }
      return r;
      ```
      - correct-ans:
      ```
      Python:
      def divisors(n):
    	count = 0
    	for i in range(1,int(math.sqrt(n))+1):
        if n%i==0 and i%2==0:
            # i is even
            count+=1
        if n%(n//i)==0 and (n//i)%2==0:
            # n//i is even and n's factor
            count+=1
        if i==n//i and i%2==0 and n%i==0:
            # if i is sqrt reduce by 1
            count-=1
    	return count
      Java:
      static int divisors(int n) {
    	int r = 0;
        if (n % 2 == 0) {
        	for(long i = 2;i <= Math.sqrt(n); i++){ // That's why it is math.sqrt(), but why not n/2??
        		// If i^2 is already larger than n, than the no. is already a target in n/i test.
            	// the factor must be equal or bigger than 2 to be calculated.
            	
                if((n % i == 0) && (i % 2 == 0)) { // Whether i is a valid divisor.
                	r++;
                }
                if((n % (n/i) == 0) && ((n/i) != i) && ((n/i) % 2 == 0)) { // Whether n/i is a valid divisor.
                    r++;
                }
            }
            if(n % 2 == 0) { // Whether n/1 is a valid divisor.
                	r++;
            }
        }	 
        return r;
    	}
      ```
   - explanation:
      - The original answer takes too much time and produces a `time limit exceeded`.
      - **All odd number `n` has 0 target output.**
      - The above `java` codes explains everything.
         - **Noticeably, if divisor is required to be found, there is no need of checking every no. from 1 to `n` in the `for` loop.**
	 
**14. gameWithCells**
   - status: **Failed**
   - ans:
      - initial-ans:
      ```
      long nm = n*m;
    	long r = 0;
    	if (nm % 2 == 0 ) { // nm = even
    		r = nm / 2 - (long)Math.floor(nm / 4);
    	} else { // nm = odd
    		r = (nm + 1) / 2;
    	}
    	return r;
      ```
      - correct-ans:
      ```
      Java:
      int r = ((n+1)/2) * ((m+1)/2);
      return r;
      Java:
      long r = (n+n%2) * (m+m%2)/4;
      return r;
      ```
   - explanation:
      - If `n` is even, it will round down. If it is odd, then simply acts as thought it were a slightly larger graph with an even number of rows.
      
**15. haloweenParty**
   - status: **Success after checking discussion**
   - ans:
   ```
   static long halloweenParty(int k) {
        /*
         * Write your code here.
         */
    	long r = (k - k/2) * (k/2);
    	return r;
    }
   ```
   - explanation:
      - THe no. of cuts must be equally distributed to rows and clumns for `1*1` pieces.
      - The pieces of chocolate is actually fixed as the no. of cuts are specified with `1*1` pieces.
      - **It is always a great way to change the input type to `long` when the output type is `long`**
         - As usually the memory space is not enough(without specified).
      - **It seems like usually `long` is already enough to solve the problem.**
      
**16. fillingJars**
   - stauts: **Success**
   - ans: `output = ((lastJar - (firstJar - 1)) * noOfCandies) / totalNoOfJars`
   - explanation: 
      - **Just always change the data size to `long` please, that's just being disgusting.**
      - **However, remember the value of array size must be either `int`, `short` , `byte` or `char` primitive data type.**

## 2020.01.08
**17. floatingRock(linear equation + Euclidean Algorithm)**
   - status: **Failed(Need revision)**
   - ans: `Euclidean Algorithm: [dividend] = [divisor]*[quotient] + [remainder]`
      - `[divisor] / [remainder] until [remainder] = 0`
      - `then gcd([dividend],[divisor]) = [last divisor]`
      - initial-ans:
      ```
      static long solve(long x1, long y1, long x2, long y2) {
    	long s = (y2 - y1) / (x2 - x1);
    	long r= 0;
    	if (x2 > x1) {
    		for (long i = x1 + 1; i > x1 && i < x2; i++) {
    			if(y2 > y1) {
    				for (long j = y1 + 1; j > y1 && j < y2; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
            		}
    			} else if (y2 == y1) {
    				for (long j = y1 + 1; j >= y1 && j <= y2; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
    				}
    			} else {
    				for (long j = y2 + 1; j >= y2 && j <= y1; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
    				}
    			}
    		}
    	} else if (x2 == x1) {
    		for (long i = x1 + 1; i >= x1 && i <= x2; i++) {
    			if(y2 > y1) {
    				for (long j = y1 + 1; j > y1 && j < y2; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
            		}
    			} else if (y2 == y1) {
    				for (long j = y1 + 1; j >= y1 && j <= y2; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
    				}
    			} else {
    				for (long j = y2 + 1; j >= y2 && j <= y1; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
    				}
    			}
    		}
    	} else {
    		for (long i = x2 + 1; i > x2 && i < x1; i++) {
    			if(y2 > y1) {
    				for (long j = y1 + 1; j > y1 && j < y2; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
            		}
    			} else if (y2 == y1) {
    				for (long j = y1 + 1; j >= y1 && j <= y2; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
    				}
    			} else {
    				for (long j = y2 + 1; j >= y2 && j <= y1; j++) {
            			long c = (j - y1) / (i - x1);
            			if (c == s) {
            				r++;
            			}
    				}
    			}
    		}
    	}
    	return r;
      }
      ```
      - correct-ans:
      ```
      Let the fraction a / b in its reduced form be the slope of the line joining P(x1, y1) and Q(x2, y2), which is equal to (y1 - y2) / (x1 - x2).
      
      To get all the points with integral coordinates, lying on the line PQ and between P and Q, we need to keep moving b units in the x-direction and a unit in the y-direction, starting from P until we reach Q.
      
      So the number of such points (excluding P and Q) is given by n, where
      
      n = abs((y1 - y2)/a) - 1
      
      or equivalently,
      
      n = abs((x1 - x2)/b) - 1
      
      However, since
      
      a = (y1 - y2)/g
      
      and 
      
      b = (x1 - x2)/g
      
      where 
      
      g = gcd(y1 - y2, x1 - x2)
      
      we have
      
      n = abs(g) - 1
      
      To express a fraction x/y in its reduced form, we divide x and y by gcd(x, y). For example, to get the reduced form of 2/4, we have to divide the numerator(dividend) and denominator(divisor) by 2 = gcd(2, 4).
      ```
      ```
      static long solve(long x1, long y1, long x2, long y2) {
    	long g = gcdByEuclidsAlgorithm(y2 - y1, x2 - x1);
    	long r = (long)Math.abs(g) - 1;
    	return r;
    	
    }
    
    static long gcdByEuclidsAlgorithm(long n1, long n2) {
    	if (n2 == 0) {
    		return n1;
    	}
    	return gcdByEuclidsAlgorithm(n2, n1 % n2);
      }
      ```
   - explanation:
      - forms for the equation of a line:
         - slope-intercept: `y = m(slope)x+ b(y-intercept)`
	 - two-point form: `(y - y1) / (x - x1) = (y2 - y1) / (x2 - x1)`
	 - point-slope: `y - y1 = m(x - x1)`
	 - standard form: `a(must be positive)x + by = c`
	 - intercept form: `x/a + y/b = 1`
	 - vertical: `x = a(x-intercept)`
	 - horizontal: `y = b`
      - **Remember if the condition is set at its lower limit, the initialisation of `i` must be bigger than that.**
      - **In many math problems, it is useful to find an invariant, which is the slope in this question.**
      - The slope in reduced form would give the smallest rise and run from one point to the next. So in total `abs(gcd(rise, run)) - 1` times(minus one because of the outer point).
         - `(y1 - y2)/(x1 - x2) = ((y1 - y2)/gcd)/((x1 - x2)/gcd) [reduced]`
      - **Usually in mathematic questions, divide-and-conquer method is often not the best solution.**
      - In `BigInteger` class, `[firstValue].gcd([secondValue])` could be used to find the gcd.

**18. celebrityJeopardy**
   - status:
   - ans:
   - explanation:
      - The major problem is about separating the symbol and value, as well as finding out the no. of spaces.
         - The symbol must be the first character in the `string`.

## 2021.05.10
**19. Roman Numerals**
   - status: 
   - ans: 
   - explanation:
      - The actual problem is about the 4 and 9 which cannot be represents by using three consecutive roman numbers.
      - 
