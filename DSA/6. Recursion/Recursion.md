# Rec

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
        if(n==1){
            System.out.print(n+" ");
            return;
        }
        inc(n-1);
        System.out.print(n+" ");
    }
    public static void main(String[] args) throws Exception {
        int n=10;
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