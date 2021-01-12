# Temporary-Memo-for-UVa-Contests
## 2021.01.13
**54. How to detect the whitespaces in a `string`?**
   - ans:
      - `[stringName].contains("[value]")` method
         - Searches the sequence of characters in the given `string`.
         - Returns `true` if sequence of char values are found in this `string` otherwise returns `false`.
         - Implies that the specified line must contain, somewhere within it, the specified `string`.
      - `isWhitespace` method
         - Retrusn `true` if the passed character is really a white space.
      - `[stringName].matches("[value]")` method
         - Returns `true` if, and only if, this `string` matches the given regular expression.
         - (.*) means if it is linked to another words, used either before or above the target `substring`.
         - Used inside a `""`.
         - Implies the specified line must match the specified `string`, which includes wildcards.
      - `regionMatches()` method
         - To be continued...
         
         **46. How to make an array size to be dynamic?**
   - ans: 
      - Either to allocate it first and readjust the size later,
      ```
      int[] oldItems = new int[10];
      for (int i = 0; i < 10; i++) {
          oldItems[i] = i + 10;
      }
      int[] newItems = new int[20];
      System.arraycopy(oldItems, 0, newItems, 0, 10);
      oldItems = newItems;
      ```
      - Or to use `ArrayList` to take care of the logic for growing array.
         - Generally preferred solution.

**46a. How to create and use an `ArrayList`?**
   - ans:
      - Declaring the array: `ArrayList<Integer> [arrayName] = nbew ArrayList<Integer>([sizeValue])`
      - Appending new elements: `[arrayName].add([value], [object])`
         - The `object` is used to add the element at a specific index, which the value in the original index would be index + 1.
      - Printing the array: `System.out.println([arrayName])`
      - Removing elements: `[arrayName].remove([index]/[value])`
      - Printing one of the elements: `System.out.println([arrayName].get([index]))`
      - Changing one of the elements: `[arrayName].set([index], [value])`
      - Iteration on the array(alternative):
      ```
      for (String str : al) {
         System.out.print(str + " ");
      }
      ```
      
**46b. How to convert from an `ArrayList` to an `array`?**
   - ans:
      - `Object[] [arrayName] = [arrayListName].toArray();`
         - Typecasting is required before using as `Integer` Object.
         ```
         for (Object obj : [arrayName]) {
            // Lines of codes
         }
         ```
         - A solution is to create an array into which elements of List need to be stored and pass it as an argument in `toArray()` method to store elements if it is big enough.
      - `Integer[] [arrayName] = new Integer[[arrayListName].size()]` + `[arrayName] = [arrayList].toArray([arrayName])`
         - If the new array(passed array) does not have enough space, a new array is created with same type and size of the given list.
         - If the passed array has sufficient space, the array is first filled with list elemetns, then null values are filled.
         - Generics = parameterized types, e.g. `Integer`, `String`(the exact opposite of the `primitive data type`).
      - Manually converting `ArrayList` using `get()` method,
      ```
      Integer[] [arrayName] = new Integer[[arrayListName].size()];
      for (int i = 0; i < [arrayListName].size(); i++) {
         [arrayName][i] = [arrayNameList].get(i);
      ```
      - Using streams API of collections to convert to array of primitive int type.
      ```
      int[] [arrayName] = list.stream().mapToInt(i -> i).toArray();
      ```

## 2021.01.13
**53a. What is a `StringTokenizer` class?**
   - ans: Allows an application to break a string into tokens(with regards of whitespace).
      - Do not distinguish among identifiers, numbers and quoted strings, nor do they recognize and skip comments.
      - Its uses is discouraged in new code.
         - It is recommended to use the `split` method of `String` or the `java.util.regex package` instead.
   - explanation:
      - `countTokens()`: Calculates the no of the times that this tokenizer's `nextToken` method can be called before it generates an exception.
      - `hasMoreElements()`: Returns the same value as the `hasMoreTokens` method.
      - `hasMoreToekns`: Tests if there are more tokens available from this tokenizer's `string`.
      - `nextElement()`: Returns the same value as the `nextToken` method, except its declared return value is `Object` rather than `string`.
      - `nextToken()`: Returns the next token from this string tokenizer.

**41. What is a `split()`?
   - ans: It breaks a given string around matcches of the given regular expression, replaced the usage of a `StringTokenizer` class.
   - explanation: `String[] [arrayName] = [stringName].split([regexString], [limitIntValue])`
       - `limit` parameter:
          - `limit > 0`: The pattern will be applied at most `limit - 1` times, the resulting `array`'s length will not be more than `n`, and the resulting array's last entry will contain all input beyond the last matched pattern.
          - `limit < 0`: The pattern will be applied as many times as possible, and the resulting array can be of any size.
          - `limit = 0`: The pattern will be applied as many times as possible, the resulting array can be of any size ,and trailing empty strings will be discarded.
          
**26. How to define an array?**
   - ans: `[dataType][] [variableName] = {[value], [value], ...}` or `[dataType][] [variableName] = new [dataType][[numbers]]`
   - Explanation: The first one defines an array with actual values while the second one only reserves spots for values.
  
**26a. How to pass an array to methods?**
   - ans: for example, `public static void [methodName](int[] [arrayName])`
   - explantion: just like any other variables. 
