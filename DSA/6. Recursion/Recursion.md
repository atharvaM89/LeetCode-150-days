# Rec

# Pattern 1- Basic Recursion

## a- Print Number in Decreasing Order

```java
public class App {
    public static void Dec(int n){
        if(n==1){
            System.out.print(n);
            return;
        }
        System.out.print(n+" ");
        Dec(n-1);
    }
    public static void main(String[] args) throws Exception {
       
        int n=10;
        Dec(n);

    }
}
```

## b- Print no in Increasing Order

```java
public class App {
    public static void inc(int n){
        if(n==10){
            System.out.print(n+" ");
            return;
        }
        inc(n+1);
        System.out.print(n+" ");
    }
    public static void main(String[] args) throws Exception {
        int n=1;
        inc(n);

    }
}

```

## c- Factorial of Number

```java
public class App {
    public static int fact(int n){
        if(n==0){
            return 1;
        }
    
        int fn=n*fact(n-1);
        
        
        return fn;
        

    }
    public static void main(String[] args) throws Exception {
       int n=5 ;
       System.out.println(fact(n));
    }
}

```

## d- Sum of N Natural No

```java
public class App {
    public static int fun(int n){
        if(n==1){
            return 1;

        }
        
        int fn=n+fun(n-1);
        return fn;
    }
    public static void main(String[] args) throws Exception {
        int n=5;
        System.out.println(fun(n));
    }
}

```

## e- Fibonacci Series

```java
public class App {
    public static int fib(int n){
        if(n==0 || n==1){
            return n;
        }
        int fn1=fib(n-1);
        int fn2=fib(n-2);
        int fn=fn1+fn2;
        return fn;

    }
    public static void main(String[] args) throws Exception {
        int n=4;
        System.out.println(fib(n));
    }
}

```

## f- Array is Sorted or Not

```java
public class App {
    public static boolean isSorted(int arr[], int i){
        if(i==arr.length-1){
            return true;
        }
        if(arr[i]>arr[i+1]){
            return false;
        }
        return isSorted(arr, i+1); 

    }
    public static void main(String[] args) throws Exception {
        int arr[]={5,6,7,8,9};
        System.out.println(isSorted(arr, 0));
    }
}

```

## g- First Occurrence

```java
public class App {
    public static int firstocc(int arr[], int key, int i){
        if(i==arr.length-1){
            return -1;
        }
        if(arr[i]==key){
            return i;
        }
        return firstocc(arr, key, i+1);
    }
    public static void main(String[] args) throws Exception {
        int arr[]={1,2,3,4,5,6,7,8,5};
        System.out.println(firstocc(arr, 55, 0));
    }
}

```

## h- Last Occurrence

```java
public class App {
    public static int lastOcc(int arr[], int key, int i){
        if(i== arr.length){
            return -1;
        }
        int isfound=lastOcc(arr, key, i+1);
        if(isfound==-1 && arr[i]==key){
            return i;
        }
        return isfound;
    }
    public static void main(String[] args) throws Exception {
        int arr[]={5,5,5,5,5,6};
        System.out.println(lastOcc(arr, 5, 0));
    }
}

```

## i-  Print X to Power N

```java
public class App {
    public static int power(int x, int n){
        if( n==0){
            return 1;
        }
        int fn=power(x,n-1);
        return x*fn;
    }
    public static void main(String[] args) throws Exception {
       System.out.println(power(2,5)) ;
    }
}

```

## j- Print X to Power N (Optimized)

```java
public class App {
    public static int power(int x, int n){
        if(n==0){
            return 1;
        }
        int halfpower=power(x, n/2);
        int halfpowersq=halfpower*halfpower;

        if(n%2 != 0){
            halfpowersq=x*halfpowersq;
            
        }
        return halfpowersq;
    }
    public static void main(String[] args) throws Exception {
      System.out.println(power(2,5));
    }
}

```

## 1. [**String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/) (8)**

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer.

The algorithm for `myAtoi(string s)` is as follows:

1. **Whitespace**: Ignore any leading whitespace (`" "`).
2. **Signedness**: Determine the sign by checking if the next character is `'-'` or `'+'`, assuming positivity if neither present.
3. **Conversion**: Read the integer by skipping leading zeros until a non-digit character is encountered or the end of the string is reached. If no digits were read, then the result is 0.
4. **Rounding**: If the integer is out of the 32-bit signed integer range `[-231, 231 - 1]`, then round the integer to remain in the range. Specifically, integers less than `231` should be rounded to `231`, and integers greater than `231 - 1` should be rounded to `231 - 1`.

Return the integer as the final result.

**Example 1:**

**Input:** s = "42"

**Output:** 42

**Explanation:**

```
The underlined characters are what is read in and the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
```

```java
class Solution {
    public int myAtoi(String s) {
       
        s=s.trim();
         int n=s.length();

        if(n==0){
            return 0;
        }

        int i=0;
        int sign=1;
        
        long num=0;
    
        if( s.charAt(i)=='-' || s.charAt(i)=='+'){
            if(s.charAt(i)=='-'){
                sign=-1;
            }
            i++;
        }

        while(i<n && Character.isDigit(s.charAt(i)) ){
            num=num*10+(s.charAt(i)-'0');

            if(num*sign>Integer.MAX_VALUE){
                return Integer.MAX_VALUE;
            }
            if(num*sign<Integer.MIN_VALUE){
                return Integer.MIN_VALUE;
            }
            i++;
        }
        return (int) (sign*num);
    }
}
```

## 2. **Pow(x, n) (50)**

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `xn`).

**Example 1:**

```
Input: x = 2.00000, n = 10
Output: 1024.00000

```

**Example 2:**

```
Input: x = 2.10000, n = 3
Output: 9.26100
```

```java
class Solution {
    public double myPow(double x, int n) {
       
        if (n == 0) return 1.0;

        
        long N = n; 
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }

        return fastPow(x, N);
    }

    private double fastPow(double x, long n) {
       
        if (n == 0) return 1.0;

        // Divide
        double half = fastPow(x, n / 2);

        // Conquer
        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
}

```

## 3. **Count Good Numbers (1922)**

A digit string is **good** if the digits **(0-indexed)** at **even** indices are **even** and the digits at **odd** indices are **prime** (`2`, `3`, `5`, or `7`).

- For example, `"2582"` is good because the digits (`2` and `8`) at even positions are even and the digits (`5` and `2`) at odd positions are prime. However, `"3245"` is **not** good because `3` is at an even index but is not even.

Given an integer `n`, return *the **total** number of good digit strings of length* `n`. Since the answer may be large, **return it modulo** `109 + 7`.

A **digit string** is a string consisting of digits `0` through `9` that may contain leading zeros.

**Example 1:**

```
Input: n = 1
Output: 5
Explanation: The good numbers of length 1 are "0", "2", "4", "6", "8".
```

```java
class Solution {
    private static final int MOD = 1_000_000_007;

    public int countGoodNumbers(long n) {
        long evenCount = (n + 1) / 2;  
        long oddCount  = n / 2;        

        long part1 = modPow(5, evenCount);
        long part2 = modPow(4, oddCount);

        return (int)((part1 * part2) % MOD);
    }

    private long modPow(long base, long exp) {
        long result = 1;
        long x = base % MOD;

        while (exp > 0) {
            if ((exp & 1) == 1) {
                result = (result * x) % MOD;
            }
            x = (x * x) % MOD;
            exp >>= 1;
        }
        return result;
    }
}

```

## 4. Sort a Stack using Recursion

Given a stack of integers **st[]**. Sort the stack in **ascending order** (smallest element at the bottom and largest at the top).

**Examples:**

```
Input:st[] = [1, 2, 3]
Output:[3, 2, 1]
Explanation:The stack is already sorted in ascending order.

```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/911853/Web/Other/blobid2_1758086056.jpg)

```
Input:st[] = [41, 3, 32, 2, 11]
Output:[41, 32, 11, 3, 2]
Explanation:After sorting, the smallest element (2) is at the bottom and the largest element (41) is at the top.

```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/911853/Web/Other/blobid1_1758085973.jpg)

```java
import java.util.Stack;

class Solution {
    public static void sortStack(Stack<Integer> s) {
      
        if (s.isEmpty()) {
            return;
        }

      
        int top = s.pop();

        
        sortStack(s);

        
        insertSorted(s, top);
    }

    
    private static void insertSorted(Stack<Integer> s, int element) {
        
        if (s.isEmpty() || s.peek() <= element) {
            s.push(element);
            return;
        }

       
        int top = s.pop();
        insertSorted(s, element);

        
        s.push(top);
    }
}

```

## 5. Reverse a Stack using Recursion

You are given a stack **st[].** You have to reverse the stack.

**Examples:**

```
Input:st[] = [1, 2, 3, 4]
Output: [1, 2, 3, 4]
Explanation: After reversing, the elements of stack are in opposite order.

```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/709919/Web/Other/blobid2_1758084285.jpg)

```
Input: st[] = [3, 2, 1]
Output: [3, 2, 1]
Explanation: After reversing, the elements of stack are in opposite order.

```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/709919/Web/Other/blobid1_1758084056.jpg)

```java
import java.util.Stack;

class Solution {

    
    public static void reverseStack(Stack<Integer> s) {
       
        if (s.isEmpty()) {
            return;
        }

       
        int top = s.pop();

       
        reverseStack(s);

        insertAtBottom(s, top);
    }

  
    private static void insertAtBottom(Stack<Integer> s, int element) {
       
        if (s.isEmpty()) {
            s.push(element);
            return;
        }

      
        int top = s.pop();
        insertAtBottom(s, element);

       
        s.push(top);
    }
    
}
```

# Pattern 2- Subsequence

## 6. Generate all binary strings

Given an integer **n**. You need to generate all the **binary strings** of n characters representing bits.

**Note:** Return the strings in  ascending order.

**Examples:**

```
Input:n = 2
Output:[00, 01, 10, 11]
Explanation:As each position can be either 0 or 1, the total possible combinations are 4.
```

```
Input:n = 3
Output:[000, 001, 010, 011, 100, 101, 110, 111]
Explanation: As each position can be either 0 or 1, the total possible combinations are 8.
```

```java
import java.util.ArrayList;

class Solution {
    
    public static ArrayList<String> binstr(int n) {
        ArrayList<String> result = new ArrayList<>();
        generate(n, new StringBuilder(), result);
        return result;
    }

    private static void generate(int n, StringBuilder curr, ArrayList<String> result) {
        
        if (curr.length() == n) {
            result.add(curr.toString());
            return;
        }

        curr.append('0');
        generate(n, curr, result);
        curr.deleteCharAt(curr.length() - 1);

        curr.append('1');
        generate(n, curr, result);
        curr.deleteCharAt(curr.length() - 1);
    }
}

```

## 7. Generate Parenthesis (22)

Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

**Example 1:**

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]

```

**Example 2:**

```
Input: n = 1
Output: ["()"]
```

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, new StringBuilder(), 0, 0, n);
        return result;
    }

    private void backtrack(List<String> result, StringBuilder curr, int open, int close, int n) {
        if (curr.length() == 2 * n) {
            result.add(curr.toString());
            return;
        }

        if (open < n) {
            curr.append('(');
            backtrack(result, curr, open + 1, close, n);
            curr.deleteCharAt(curr.length() - 1);
        }

        if (close < open) {
            curr.append(')');
            backtrack(result, curr, open, close + 1, n);
            curr.deleteCharAt(curr.length() - 1);
        }
    }
}

```

## 8. Subsets (78) / Print all Subsequences

Given an integer array `nums` of **unique** elements, return *all possible* *subsets* *(the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, 0, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int[] nums, int idx, List<Integer> curr, List<List<Integer>> result) {
     
        result.add(new ArrayList<>(curr));

        for (int i = idx; i < nums.length; i++) {
            curr.add(nums[i]);
            backtrack(nums, i + 1, curr, result);
            curr.remove(curr.size() - 1);
        }
    }
}

```

## 9. count all Subsequences with sum k

Given an array nums and an integer k.Return the **number** of **non-empty subsequences** of nums such that the sum of all elements in the subsequence is equal to k.

**Examples:**

**Input :** nums = [4, 9, 2, 5, 1] , k = 10

**Output :** 2

**Explanation :** The possible subsets with sum k are [9, 1] , [4, 5, 1].

**Input :** nums = [4, 2, 10, 5, 1, 3] , k = 5

**Output :** 3

**Explanation :** The possible subsets with sum k are [4, 1] , [2, 3] , [5].

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

class Solution {

    public long countSubsequenceWithTargetSum(int[] nums, int k) {
        int n = nums.length;
        int mid = n / 2;

        List<Long> leftSums = new ArrayList<>();
        genSums(nums, 0, mid, 0L, leftSums);

        List<Long> rightSums = new ArrayList<>();
        genSums(nums, mid, n, 0L, rightSums);

        HashMap<Long, Long> freq = new HashMap<>();
        for (Long s : rightSums)
            freq.put(s, freq.getOrDefault(s, 0L) + 1L);

        long ans = 0;
        for (Long sL : leftSums) {
            long need = (long) k - sL;
            ans += freq.getOrDefault(need, 0L);
        }

        // remove empty subsequence if k == 0
        if (k == 0)
            ans -= 1;

        return ans;
    }

    private void genSums(int[] nums, int from, int to, long cur, List<Long> out) {
        if (from == to) {
            out.add(cur);
            return;
        }
        genSums(nums, from + 1, to, cur, out);
        genSums(nums, from + 1, to, cur + nums[from], out);
    }
}

```

## 10. **Check if there exists a subsequence with sum K**

Given an array **arr** and `target sum **k**`, check whether there exists a subsequence such that the sum of all elements in the subsequence equals the given `target sum(k).`

**Example:**

```
Input: arr = [10,1,2,7,6,1,5], k = 8.
Output: Yes
Explanation: Subsequences like [2, 6], [1, 7] sum upto 8

Input: arr = [2,3,5,7,9], k = 100.
Output: No
Explanation: No subsequence can sum upto 100
```

**Your Task:**You don't need to read or print anything. Your task is to complete the boolean function **checkSubsequenceSum()** which takes N, arr and K as input parameter and returns true/false based on the whether any subsequence with sum K could be found.

```java
import java.util.Arrays;

class Solution {

    public static boolean checkSubsequenceSum(int n, int[] arr, int K) {
        
        int[][] memo = new int[n + 1][K + 1];
        for (int i = 0; i <= n; i++) Arrays.fill(memo[i], -1);
        return dfs(arr, 0, K, memo);
    }

    private static boolean dfs(int[] arr, int idx, int rem, int[][] memo) {
        
        if (rem == 0) return true;
        if (idx == arr.length) return false;
        if (rem < 0) return false;
        if (memo[idx][rem] != -1) return memo[idx][rem] == 1;

        boolean take = false;
        if (arr[idx] <= rem) take = dfs(arr, idx + 1, rem - arr[idx], memo);

        boolean skip = dfs(arr, idx + 1, rem, memo);

        boolean ans = take || skip;
        memo[idx][rem] = ans ? 1 : 0;
        return ans;
    }
}

```

## 11. Combination sum I (39)

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        backtrack(candidates, 0, target, new ArrayList<>(), ans);
        return ans;
    }

    private void backtrack(int[] candidates, int idx, int target, List<Integer> curr, List<List<Integer>> ans) {

        if (target == 0) {
            ans.add(new ArrayList<>(curr));
            return;
        }

        if (idx == candidates.length || target < 0) {
            return;
        }

       
        curr.add(candidates[idx]);
        backtrack(candidates, idx, target - candidates[idx], curr, ans);
        curr.remove(curr.size() - 1);

       
        backtrack(candidates, idx + 1, target, curr, ans);
    }
}

```

## 12. Combination sum II (40)

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output:
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);  
        backtrack(candidates, target, 0, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int[] nums, int target, int start, List<Integer> curr, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList<>(curr));
            return;
        }

        for (int i = start; i < nums.length; i++) {

           
            if (i > start && nums[i] == nums[i - 1]) continue;

            int val = nums[i];
            if (val > target) break; 

            curr.add(val);
            backtrack(nums, target - val, i + 1, curr, result); 
            curr.remove(curr.size() - 1);
        }
    }
}

```

## 13. Combination Sum III (216)

Find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

- Only numbers `1` through `9` are used.
- Each number is used **at most once**.

Return *a list of all possible valid combinations*. The list must not contain the same combination twice, and the combinations may be returned in any order.

**Example 1:**

```
Input: k = 3, n = 7
Output: [[1,2,4]]
Explanation:
1 + 2 + 4 = 7
There are no other valid combinations.
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(k, n, 1, new ArrayList<>(), result);
        return result;
    }

   
    private void backtrack(int k, int target, int start, List<Integer> curr, List<List<Integer>> result) {
       
        if (curr.size() == k) {
            if (target == 0) result.add(new ArrayList<>(curr));
            return;
        }

        
        int need = k - curr.size();
        if (start > 9 || (9 - start + 1) < need) return;

        
        for (int num = start; num <= 9; num++) {
            if (num > target) break;
            curr.add(num);
            backtrack(k, target - num, num + 1, curr, result); 
            curr.remove(curr.size() - 1);
        }
    }
}

```

## 14. Subset Sum I

Given a array **`arr`** of integers, return the sums of all subsets in the list.  Return the sums in any order.

**Examples:**

```
Input:arr[] = [2, 3]
Output:[0, 2, 3, 5]
Explanation:When no elements are taken then Sum = 0. When only 2 is taken then Sum = 2. When only 3 is taken then Sum = 3. When elements 2 and 3 are taken then Sum = 2+3 = 5.
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    ArrayList<Integer> subsetSums(int[] arr) {
        ArrayList<Integer> result = new ArrayList<>();
        generate(arr, 0, 0, result);
        return result;
    }

    private void generate(int[] arr, int idx, int sum, List<Integer> result) {
        if (idx == arr.length) {
            result.add(sum);
            return;
        }
  
        generate(arr, idx + 1, sum + arr[idx], result);
        generate(arr, idx + 1, sum, result);
    }
}

```

## 15. Subset Sum II (90)

Given an integer array `nums` that may contain duplicates, return *all possible* *subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);  
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, 0, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int[] nums, int start, List<Integer> curr, List<List<Integer>> result) {
        result.add(new ArrayList<>(curr));

        for (int i = start; i < nums.length; i++) {
           
            if (i > start && nums[i] == nums[i - 1]) continue;

            curr.add(nums[i]);
            backtrack(nums, i + 1, curr, result);  
            curr.remove(curr.size() - 1);
        }
    }
}

```

## 16. Letter Combinations of Phone Number (17)

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png)

**Example 1:**

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    private static final String[] MAPPING = {
        "",     // 0
        "",     // 1
        "abc",  // 2
        "def",  // 3
        "ghi",  // 4
        "jkl",  // 5
        "mno",  // 6
        "pqrs", // 7
        "tuv",  // 8
        "wxyz"  // 9
    };

    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits == null || digits.length() == 0) return result;

        backtrack(digits, 0, new StringBuilder(), result);
        return result;
    }

    private void backtrack(String digits, int idx, StringBuilder curr, List<String> result) {
        if (idx == digits.length()) {
            result.add(curr.toString());
            return;
        }

        String letters = MAPPING[digits.charAt(idx) - '0'];

        for (char c : letters.toCharArray()) {
            curr.append(c);
            backtrack(digits, idx + 1, curr, result);
            curr.deleteCharAt(curr.length() - 1);
        }
    }
}

```

# Extra

### -Tilling Problem

```jsx
public class App {
    public static int tiling(int n){   //2*n floor size
        if(n==1 || n==0){
            return 1;
        }
        int vertical=tiling(n-1);
        int horizontal=tiling(n-2);

        return vertical+horizontal;
    }
    public static void main(String[] args) throws Exception {
      System.out.println( tiling(4));
    }
}

```

### -Remove Duplicate Letter From Strings

```jsx
public class App {
    public static void remove(String str, int idx, StringBuilder newString, boolean map[]){
        if(idx==str.length()){
             System.out.println( newString);
             return;
        }
        char curr=str.charAt(idx);
        if(map[curr-'a']==true){
            remove(str, idx+1, newString, map);
        }
        else{
            map[curr-'a']=true;
            remove(str, idx+1, newString.append(curr), map);
        }
    }
    public static void main(String[] args) throws Exception {
        String str="appnnacollege";
        remove(str, 0, new StringBuilder (""), new boolean[26]);
    }
}

```

### -Friend Pairing Problem

```jsx
public class App {
    public static int pair(int n){
        if(n==2|| n==1){
            return n;
        }
        int single=pair(n-1);
        int pair=pair(n-2);
        int pairingways=(n-1)*pair;

        return single+pairingways;
    }
    public static void main(String[] args) throws Exception {
       System.out.println(pair(3));
    }
}

```

### -Binary String Problme

```jsx
public class App {
    public static void binary(int n, int lp, String str){
        if(n==0){
            System.out.println(str);
            return;
        }
        binary(n-1, 0, str+"0");
        if(lp==0){
            binary(n-1, 1, str+"1");
        }
    }
    public static void main(String[] args) throws Exception {
       binary(3, 0, " ");
    }
}

```

### -Occurrences of Index

```jsx
public class App {
    public static void occurance(int arr[], int key, int n){
        if(n== arr.length){
            return;
        }
        if(arr[n]==key){
            System.out.print(n+" ");
        }
        
         occurance(arr, key, n+1);
    }
    public static void main(String[] args) throws Exception {
        int arr[]={3, 2, 4, 5, 6, 2, 7, 2, 2};
        occurance(arr,2,0);
    }
}

```

### -Convert No in String

```jsx
public class App {
    static String digit[]={"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
    public static void ts(int n){
        if(n==0){
            return;
        }
        int lastdigit=n%10;
         n=n/10;

         ts(n);
         System.out.print(digit[lastdigit]+" ");
        
    }
    public static void main(String[] args) throws Exception {
      ts(2019);
      
    }
}

```

### -Length of String

```jsx
public class App {
    public static int length(String str){
        if(str.length()==0){
            return 0;
        }
        return length(str.substring(1)) +1;
    }
    public static void main(String[] args) throws Exception {
       String str="abcd";
       System.out.println(length(str));
    }
}

```

### -Tower of Hanoi

```jsx
public class App {
    public static void toh(int n, String src, String helper, String dest){
        if(n==1){
            System.out.println("transfer disk "+n+" from "+src+" to "+dest);
            return;
        }

        toh(n-1, src, dest, helper);
        System.out.println("transfer disk "+ n+" from "+src+" to "+dest);
        toh(n-1, helper, src, dest);
    }
    public static void main(String[] args) throws Exception {
        int n=4;
        toh(n, "S","H", "D");
    }
}

```

# Pattern 3- Backtracking

### -Backtracking on Array

```jsx
public class App {
    public static void changeArr(int arr[], int i, int val){
        
        // base case
        if(i==arr.length){
            PrintArr(arr);
            return;
        }

        //recursion(kam)
        arr[i]=val;
        changeArr(arr, i+1, val+1);
        arr[i]=arr[i]-2;
    }
    public static void PrintArr(int arr[]){
        for(int i=0; i<arr.length; i++){
            System.out.print(arr[i]+" ");
        }
        System.out.println("");
    }
    public static void main(String[] args) throws Exception {
        int arr[]=new int[5];
        changeArr(arr,0,1);
        PrintArr(arr);
        

    }
}
```

### -Find Subset of Strings

```jsx
public class App {
    public static void findSubset(String str, String ans, int i){
        //base case
        if(i==str.length()){
            if(ans==""){
                System.out.println("Null");
            }
            else{
                System.out.println(ans);
            }
            
            return;
        }

        //kam

        findSubset(str, ans+str.charAt(i), i+1);
        findSubset(str, ans, i+1);
    }
    public static void main(String[] args) throws Exception {
       String str= "abc";
       String ans="";
       findSubset(str,ans,0);

    }
}

```

### -Permutation of all Strings

```jsx
public class App {
    public static void per(String str, String ans){

        //base case

    if(str.length()==0){
        System.out.println(ans);
        return;
    }

        //kam

        for(int i=0; i<str.length(); i++){
            char ch=str.charAt(i);

            String Nstr=str.substring(0, i)+str.substring(i+1);
            per(Nstr, ans+ch);
    }
}

    public static void main(String[] args) throws Exception {

        String str="abc";
        per(str, "");
        
    }
}

```

## 17. Palindrome Partitioning (131)

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return *all possible palindrome partitioning of* `s`.

**Example 1:**

```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]

```

**Example 2:**

```
Input: s = "a"
Output: [["a"]]
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        if (s == null) return result;
        int n = s.length();
        if (n == 0) {
            result.add(new ArrayList<>());
            return result;
        }

     
        boolean[][] isPal = new boolean[n][n];
        for (int right = 0; right < n; right++) {
            for (int left = 0; left <= right; left++) {
                if (s.charAt(left) == s.charAt(right) && (right - left <= 2 || isPal[left + 1][right - 1])) {
                    isPal[left][right] = true;
                }
            }
        }

        backtrack(s, 0, new ArrayList<>(), result, isPal);
        return result;
    }

    private void backtrack(String s, int start, List<String> curr, List<List<String>> result, boolean[][] isPal) {
        int n = s.length();
        if (start == n) {
            result.add(new ArrayList<>(curr));
            return;
        }

        for (int end = start; end < n; end++) {
            if (isPal[start][end]) {
                curr.add(s.substring(start, end + 1));
                backtrack(s, end + 1, curr, result, isPal);
                curr.remove(curr.size() - 1);
            }
        }
    }
}

```

## 18. Word Search (79)

Given an `m x n` grid of characters `board` and a string `word`, return `true` *if* `word` *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0) return false;
        if (word == null || word.length() == 0) return true;

        int m = board.length, n = board[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == word.charAt(0) && dfs(board, i, j, word, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean dfs(char[][] board, int r, int c, String word, int idx) {
        if (idx == word.length()) return true; // matched whole word
        // bounds + char check
        if (r < 0 || r >= board.length || c < 0 || c >= board[0].length) return false;
        if (board[r][c] != word.charAt(idx)) return false;

        // mark visited in place
        char saved = board[r][c];
        board[r][c] = '#';

        // explore 4 directions
        boolean found = dfs(board, r + 1, c, word, idx + 1)
                     || dfs(board, r - 1, c, word, idx + 1)
                     || dfs(board, r, c + 1, word, idx + 1)
                     || dfs(board, r, c - 1, word, idx + 1);

        // restore
        board[r][c] = saved;
        return found;
    }
}

```

## 19. N- Queen (51)

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return *all distinct solutions to the **n-queens puzzle***. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above

```

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        if (n <= 0) return result;

       
        boolean[] cols = new boolean[n];
        boolean[] diag = new boolean[2 * n - 1];
        boolean[] anti = new boolean[2 * n - 1];

       
        char[][] board = new char[n][n];
        for (int r = 0; r < n; r++) Arrays.fill(board[r], '.');

        backtrack(0, n, board, cols, diag, anti, result);
        return result;
    }

    private void backtrack(int row, int n, char[][] board,
                           boolean[] cols, boolean[] diag, boolean[] anti,
                           List<List<String>> result) {
        if (row == n) {
          
            List<String> sol = new ArrayList<>(n);
            for (int i = 0; i < n; i++) sol.add(new String(board[i]));
            result.add(sol);
            return;
        }

        for (int col = 0; col < n; col++) {
            int d = row - col + (n - 1); // main diagonal index
            int a = row + col;          // anti-diagonal index

            if (cols[col] || diag[d] || anti[a]) continue; // conflict -> skip

            // place queen
            board[row][col] = 'Q';
            cols[col] = true;
            diag[d] = true;
            anti[a] = true;

            backtrack(row + 1, n, board, cols, diag, anti, result);

            // remove queen (backtrack)
            board[row][col] = '.';
            cols[col] = false;
            diag[d] = false;
            anti[a] = false;
        }
    }
}

```

## 20. Rat in Maze

Consider a rat placed at position (0, 0) in an **n x n** square matrix **`maze[][]`**. The rat's goal is to reach the destination at position (n-1, n-1). The rat can move in four possible directions: **'U'(up)**, **'D'(down)**, **'L' (left)**, **'R' (right)**.

The matrix contains only two possible values:

- `0`: A blocked cell through which the rat cannot travel.
- `1`: A free cell that the rat can pass through.

Your task is to find **all possible paths** the rat can take to reach the destination, starting from (0, 0) and ending at (n-1, n-1), under the condition that the rat cannot **revisit** any cell along the same path. Furthermore, the rat can only move to adjacent cells that are within the bounds of the matrix and not blocked.If no path exists, return an **empty list.**

**Note:** Return the final result vector in **lexicographically smallest order**.

**Examples:**

```
Input: maze[][] = [[1, 0, 0, 0], [1, 1, 0, 1], [1, 1, 0, 0], [0, 1, 1, 1]]
Output:["DDRDRR", "DRDDRR"]
Explanation: The rat can reach the destination at (3, 3) from (0, 0) by two paths - DRDDRR and DDRDRR, when printed in sorted order we get DDRDRR DRDDRR.
```

```java
import java.util.ArrayList;

class Solution {

    ArrayList<String> ratInMaze(int[][] maze) {
        int n = maze.length;
        ArrayList<String> result = new ArrayList<>();

        if (n == 0) return result;
        if (maze[0][0] == 0 || maze[n-1][n-1] == 0) return result;

        boolean[][] visited = new boolean[n][n];
        StringBuilder path = new StringBuilder();

        dfs(maze, n, 0, 0, visited, path, result);
        return result;
    }

    private void dfs(int[][] maze, int n, int r, int c,
                     boolean[][] visited, StringBuilder path,
                     ArrayList<String> result) {

        if (r == n - 1 && c == n - 1) {
            result.add(path.toString());
            return;
        }

        visited[r][c] = true;

        // D
        if (isSafe(maze, n, r + 1, c, visited)) {
            path.append('D');
            dfs(maze, n, r + 1, c, visited, path, result);
            path.deleteCharAt(path.length() - 1);
        }

        // L
        if (isSafe(maze, n, r, c - 1, visited)) {
            path.append('L');
            dfs(maze, n, r, c - 1, visited, path, result);
            path.deleteCharAt(path.length() - 1);
        }

        // R
        if (isSafe(maze, n, r, c + 1, visited)) {
            path.append('R');
            dfs(maze, n, r, c + 1, visited, path, result);
            path.deleteCharAt(path.length() - 1);
        }

        // U
        if (isSafe(maze, n, r - 1, c, visited)) {
            path.append('U');
            dfs(maze, n, r - 1, c, visited, path, result);
            path.deleteCharAt(path.length() - 1);
        }

        visited[r][c] = false;
    }

    private boolean isSafe(int[][] maze, int n, int r, int c, boolean[][] visited) {
        return r >= 0 && r < n && c >= 0 && c < n && maze[r][c] == 1 && !visited[r][c];
    }
}

```

## 21. Unique Paths (62)

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return *the number of possible unique paths that the robot can take to reach the bottom-right corner*.

The test cases are generated so that the answer will be less than or equal to `2 * 109`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
Input: m = 3, n = 7
Output: 28

```

```java
class Solution {
    public int uniquePaths(int m, int n) {
        return dfs(0, 0, m, n);
    }

    private int dfs(int r, int c, int m, int n) {
        // reached destination
        if (r == m - 1 && c == n - 1) {
            return 1;
        }

        int paths = 0;

        // move down
        if (r + 1 < m) {
            paths += dfs(r + 1, c, m, n);
        }

        // move right
        if (c + 1 < n) {
            paths += dfs(r, c + 1, m, n);
        }

        return paths;
    }
}

```

## 22. Word Break (139)

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

```java
import java.util.HashSet;
import java.util.List;
import java.util.Set;

class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);
        int n = s.length();
    
        int[] memo = new int[n];
        return canBreak(s, 0, dict, memo);
    }

  
    private boolean canBreak(String s, int start, Set<String> dict, int[] memo) {
        int n = s.length();
        if (start == n) return true;
        if (memo[start] != 0) return memo[start] == 1;

        for (int end = start + 1; end <= n; end++) {
            String prefix = s.substring(start, end);
            if (dict.contains(prefix)) {
                if (canBreak(s, end, dict, memo)) {
                    memo[start] = 1;
                    return true;
                }
            }
        }

        memo[start] = -1;
        return false;
    }
}

```

## 23. M- Coloring Problem

You are given an undirected graph consisting of **V** vertices and **E** edges represented by a list **edges[][]**, along with an integer **`m`**. Your task is to determine whether it is possible to **color the graph** using at most **`m`** different colors such that no two adjacent vertices share the **same color**. Return `true` if the graph can be colored with at most **`m`** colors, otherwise return `false`.

**Note:** The graph is indexed with 0-based indexing.

**Examples:**

```
Input:V = 4, edges[][] = [[0, 1], [1, 3], [2, 3], [3, 0], [0, 2]], m = 3
Output:true
Explanation:It is possible to color the given graph using 3 colors, for example, one of the possible ways vertices can be colored as follows:

Vertex 0: Color 1
Vertex 1: Color 2
Vertex 2: Color 2
Vertex 3: Color 3
```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893404/Web/Other/blobid3_1746162701.jpg)

```java
class Solution {

    boolean graphColoring(int V, int[][] edges, int m) {
      
        boolean[][] graph = new boolean[V][V];
        for (int[] e : edges) {
            int u = e[0];
            int v = e[1];
            graph[u][v] = true;
            graph[v][u] = true;
        }

        int[] color = new int[V];
        return backtrack(0, V, m, graph, color);
    }

    private boolean backtrack(int node, int V, int m, boolean[][] graph, int[] color) {
        if (node == V) return true;

        for (int c = 1; c <= m; c++) {
            if (isSafe(node, c, graph, color, V)) {
                color[node] = c;
                if (backtrack(node + 1, V, m, graph, color)) return true;
                color[node] = 0; 
            }
        }
        return false;
    }

    private boolean isSafe(int node, int c, boolean[][] graph, int[] color, int V) {
        for (int i = 0; i < V; i++) {
            if (graph[node][i] && color[i] == c) {
                return false;
            }
        }
        return true;
    }
}

```

## 24. Sudoku Solver (37)

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

The `'.'` character indicates empty cells.

**Example 1:**

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```
Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
Explanation: The input board is shown above and the only valid solution is shown below:

```

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public void solveSudoku(char[][] board) {
        
        int[] rows = new int[9];
        int[] cols = new int[9];
        int[] boxes = new int[9];
        List<int[]> empties = new ArrayList<>();

      
        for (int r = 0; r < 9; r++) {
            for (int c = 0; c < 9; c++) {
                char ch = board[r][c];
                if (ch == '.' || ch == '0') {
                    empties.add(new int[]{r, c});
                } else {
                    int d = ch - '1'; // 0..8
                    int bit = 1 << d;
                    rows[r] |= bit;
                    cols[c] |= bit;
                    boxes[(r / 3) * 3 + (c / 3)] |= bit;
                }
            }
        }

        backtrack(board, 0, empties, rows, cols, boxes);
    }

    private boolean backtrack(char[][] board, int idx, List<int[]> empties,
                              int[] rows, int[] cols, int[] boxes) {
        if (idx == empties.size()) return true; // solved

        int r = empties.get(idx)[0];
        int c = empties.get(idx)[1];
        int b = (r / 3) * 3 + (c / 3);

       
        int used = rows[r] | cols[c] | boxes[b];
       
        int avail = (~used) & 0x1FF; // keep only 9 bits

        while (avail != 0) {
            int pick = avail & -avail;        
            int d = Integer.numberOfTrailingZeros(pick); 
            char ch = (char) ('1' + d);

            // place
            board[r][c] = ch;
            rows[r] |= pick;
            cols[c] |= pick;
            boxes[b] |= pick;

            // recurse
            if (backtrack(board, idx + 1, empties, rows, cols, boxes)) return true;

            // undo
            board[r][c] = '.';
            rows[r] &= ~pick;
            cols[c] &= ~pick;
            boxes[b] &= ~pick;

            // remove tried bit
            avail &= avail - 1;
        }

        
        return false;
    }
}

```

## 25. Expression Add Operator (282)

Given a string `num` that contains only digits and an integer `target`, return ***all possibilities** to insert the binary operators* `'+'`*,* `'-'`*, and/or* `'*'` *between the digits of* `num` *so that the resultant expression evaluates to the* `target` *value*.

Note that operands in the returned expressions **should not** contain leading zeros.

**Note** that a number can contain multiple digits.

**Example 1:**

```
Input: num = "123", target = 6
Output: ["1*2*3","1+2+3"]
Explanation: Both "1*2*3" and "1+2+3" evaluate to 6.

```

**Example 2:**

```
Input: num = "232", target = 8
Output: ["2*3+2","2+3*2"]
Explanation: Both "2*3+2" and "2+3*2" evaluate to 8.

```

**Example 3:**

```
Input: num = "3456237490", target = 9191
Output: []
Explanation: There are no expressions that can be created from "3456237490" to evaluate to 9191.
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> result = new ArrayList<>();
        if (num == null || num.length() == 0) return result;
        backtrack(num, 0, 0L, 0L, new StringBuilder(), target, result);
        return result;
    }

   
    private void backtrack(String num, int pos, long value, long last,
                           StringBuilder expr, long target, List<String> result) {
        int n = num.length();
        if (pos == n) {
            if (value == target) result.add(expr.toString());
            return;
        }

        int lenBefore = expr.length();
        long currNum = 0L;

        
        for (int i = pos; i < n; i++) {

            if (i > pos && num.charAt(pos) == '0') break;

            currNum = currNum * 10 + (num.charAt(i) - '0');
            String currStr = num.substring(pos, i + 1);

            if (pos == 0) {
                
                expr.append(currStr);
                backtrack(num, i + 1, currNum, currNum, expr, target, result);
                expr.setLength(lenBefore);
            } else {
                // PLUS
                expr.append('+').append(currStr);
                backtrack(num, i + 1, value + currNum, currNum, expr, target, result);
                expr.setLength(lenBefore);

                // MINUS
                expr.append('-').append(currStr);
                backtrack(num, i + 1, value - currNum, -currNum, expr, target, result);
                expr.setLength(lenBefore);

                // MULTIPLY
                expr.append('*').append(currStr);
               
                backtrack(num, i + 1, value - last + last * currNum, last * currNum, expr, target, result);
                expr.setLength(lenBefore);
            }
        }
    }
}

```