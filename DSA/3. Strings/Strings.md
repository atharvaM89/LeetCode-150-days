# Strings

# Concepts

### String Methods

```java
String str="java";

1. str.length();

2. str.toLowerCase();

3. str.toUpperCase();

4. str.trim();   // Remove Spaces

5. str.SubString(i); // word will starts from i
	 str.SubString(i, j) // word only have chars form i to j
	 
6. str.replace(a,b);

7. str.StartsWith("www") // this is of Boolean type

8. str.endsWith("org")  // This is also of boolean type

9. str.CharAt(int index);

10. str.indexOf(".");
		str.indexOf(".", 4); // this will return index after 4th 
		
11. str.lastIndexOf(".");
		str.lastIndexOf(".", 4);
		
12. str.equals(String S);  // Of Boolean type

13. str.equalsIgnoreCase(String S);

14. str1.compareTo(str2);

15. Character.isLetterOrDigit(i)

16.   String words[]=s.trim().split("\\s+");
		splits on one or more spaces, so multiple spaces between words are reduced to one
```

### Examples

```java
		Index & SubString
				
									 String str1="atharvamahulkar@gmail.com";
					        int i=str1.indexOf("@");
					        String uname=str1.substring(0,i);
					        String domain=str1.substring(i+1,str1.length());
					        System.out.println("Username-"+uname);
					        System.out.println("Domain-"+domain);
					        System.out.println(domain.startsWith("gmail"));
					        
		Upper-Case & Trim
				
									String s="    Java     ";
					        System.out.println(s.length());
					        
					        System.out.println(s.toLowerCase());
					        System.out.println(s.toUpperCase());
					        System.out.println(s.trim());
					        
					        String str="Welcome";
					        System.out.println(str.substring(3,6));
					        System.out.println(str.replace('e','k'));
					        
					        String sc="www.atharva.com";
					        System.out.println(sc.startsWith("www"));
					        System.out.println(sc.endsWith("com"));
					        System.out.println(sc.charAt(5));
					        System.out.println(sc.indexOf("a",5));
					        System.out.println(str.equals(sc));
					        System.out.println(str.equalsIgnoreCase(sc));
					        
					        
		Matches & Replace
		
										 int i=010101;
								     String str=String.valueOf(i);
								     System.out.println(str.matches("[01]*"));
								     
								     String s="a@ccxvw45*&96*T87Uvjdvjhbdaksbk";
								     System.out.println(s.replaceAll("[^a-zA-B1-9]",""));
								     
								     String sc="     bfdvd    dvfdv    dfvfd";
								     System.out.println(sc.replaceAll(//s+," ");
```

### String Builder

```java
public class App {
    public static void main(String[] args) throws Exception {
        StringBuilder sb=new StringBuilder("a");
        for(char ch='a'; ch<='z'; ch++){
            sb.append(ch);
            System.out.println("");
        }
    }
}

```

# Basic

- Shortest Path in Strings

```java
public class App {
    public static float shortest(String path){
        int x=0;
        int y=0;
        for(int i=0; i<path.length(); i++){
            char dir=path.charAt(i);
            if(dir=='E'){
                x++;
            }
            else if(dir=='W'){
                x--;
            }
            else if(dir=='N'){
                y++;
            }
            else{
                y--;
            }

        }
        int X2=x*x;
        int Y2=y*y;

        return (float)Math.sqrt(X2+Y2);
    }
    public static void main(String[] args) throws Exception {
       String path="WNEENESENNN";
       System.out.println(shortest(path));
    }
}

```

## 1. Valid Palindrome(125)

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` *if it is a **palindrome**, or* `false` *otherwise*.

**Example 1:**

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

```java
class Solution { 
    public boolean isPalindrome(String s) {
        //s=s.trim();
        s=s.toLowerCase().replaceAll("[^a-z0-9]", "");
        
        int n=s.length();

        for(int i=0; i<n/2; i++){
            if(s.charAt(i)!=s.charAt(n-1-i)){
                return false;
            }
        }
        return true;
    }
}
```

More Optimized

```java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder sb=new StringBuilder();

        int n=s.length();
        for(int i=0; i<n; i++) {
            char c=s.charAt(i);
            if(Character.isLetterOrDigit(c)){
                sb.append(Character.toLowerCase(c));
            }
        }
        int l=0; int r=sb.length()-1;

        while(l<r){
            if(sb.charAt(l++)!=sb.charAt(r--)){
                return false;
            }
        }
        return true;
    }
}
```

## 2. Length of Last Word (58)

Given a string `s` consisting of words and spaces, return *the length of the **last** word in the string.*

A **word** is a maximal substring consisting of non-space characters only.

**Example 1:**

```
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int count=0;
        int len= s.length();

        for(int i=len-1; i>=0; i--){
            if(s.charAt(i) != ' '){
                count++;
            }
            else if(count!=0)
            {
                break;
            }
        }
        return count;
        
    }
}
```

## 3. Valid Parenthesis (20)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"

**Output:** true

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st=new Stack<>();
        int n=s.length();

        for(int i=0; i<n; i++){
            char c=s.charAt(i);

            if(c=='(' || c=='{' || c=='['){
                st.push(c);
            }
            else{
                if(st.isEmpty()){
                    return false;
                }
                char top=st.pop();

                if(   (c==')' && top!='(')
                    || (c=='}' && top!='{')
                    || (c==']' && top!='[')){
                        return false;
                    }
            }
        }
    return st.isEmpty();
    }
}
```

## 4. Remove Outmost Parentheses (1021)

**Example 1:**

```
Input: s = "(()())(())"
Output: "()()()"
Explanation:
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
```

```java
class Solution {
    public String removeOuterParentheses(String s) {
        StringBuilder sb=new StringBuilder();
        int n=s.length();
          int count =0;

        for(int i=0; i<n; i++){
            char c=s.charAt(i);
          

            if(c=='('){
                if(count>0){
                    sb.append(c);
                }
                count++;
            }
            else{
                count--;
                if(count>0){
                    sb.append(c);
                }
            }
        }
        return sb.toString();
    }
}
```

## 5. Reverse Words in String (151)

**Example 1:**

```
Input: s = "the sky is blue"
Output: "blue is sky the"
```

```java
class Solution {
    public String reverseWords(String s) {
        int n=s.length();
        String words[]=s.trim().split("\\s+");
        StringBuilder sb=new StringBuilder();

        for(int i=words.length-1; i>=0; i--){
            sb.append(words[i]);
            if(i!=0){
                sb.append(" ");
            }
        }
        return sb.toString();

    }
}
```

## 6. String Compression (443)

```
Input: chars = ["a","a","b","b","c","c","c"]
Output: Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]
Explanation: The groups are "aa", "bb", and "ccc". This compresses to "a2b2c3".
```

```java
class Solution {
    public int compress(char[] chars) {
          int n = chars.length;
        int write = 0; 
        int i = 0;

        while (i < n) {
            char currentChar = chars[i];
            int count = 0;
            while (i < n && chars[i] == currentChar) {
                i++;
                count++;
            }
            chars[write++] = currentChar;
            if (count > 1) {
                String cntStr = Integer.toString(count);
                for (char c : cntStr.toCharArray()) {
                    chars[write++] = c;
                }
            }
        }

        return write; 
    }
}
```

## 7. Maximum Number of Vowels in a Substring of given length (1456)

**Example 1:**

```
Input: s = "abciiidef", k = 3
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.
```

```java
class Solution {
    public int maxVowels(String s, int k) {
       
        int n = s.length();
        int maxCount = 0, count = 0;

        for (int i = 0; i < n; i++) {
            char c = s.charAt(i);

            if (isVowel(c)) count++;

            if (i >= k && isVowel(s.charAt(i - k))) {
                count--;
            }

            maxCount = Math.max(maxCount, count);
        }

        return maxCount;
    }

    private boolean isVowel(char c) {
        c = Character.toLowerCase(c);
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u';
    }
    
}
```

## 8. Valid Anagram (242)

**Example 1:nt**

**Input:** s = "anagram", t = "nagaram"

**Output:** true

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length()!=t.length()){
            return false;
        }

        char sarr[]=s.toCharArray();
        char tarr[]=t.toCharArray();

        Arrays.sort(sarr);
        Arrays.sort(tarr);

       return Arrays.equals(sarr, tarr);
    }
}
```

## 9. Find all Anagrams in a String (438)

```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
         List<Integer> result = new ArrayList<>();
        if (s.length() < p.length()) return result;

        int[] pCount = new int[26]; 
        int[] sCount = new int[26]; 

        for (char c : p.toCharArray()) {
            pCount[c - 'a']++;
        }

        int k = p.length();
        for (int i = 0; i < s.length(); i++) {
            
            sCount[s.charAt(i) - 'a']++;

            if (i >= k) {
                sCount[s.charAt(i - k) - 'a']--;
            }

            if (Arrays.equals(sCount, pCount)) {
                result.add(i - k + 1);
            }
        }

        return result;
    }
}
```

## 10. Largest Odd Number in String (1903)

**Example 1:**

```
Input: num = "52"
Output: "5"
Explanation: The only non-empty substrings are "5", "2", and "52". "5" is the only odd number.
```

```java
class Solution {
    public String largestOddNumber(String num) {
        int n=num.length();
       
        
        for(int i=n-1; i>=0; i--){
            int c=num.charAt(i)- '0';   //-'0' is for converting ASCII char to Actual Integer
            
            if( c%2==1){
               return num.substring(0, i+1);
            }
            
        }
        
        return "";
    }
}
```

## 11. Isomorphic Strings (205)

**Example 1:**

**Input:** s = "egg", t = "add"

**Output:** true

**Explanation:**

The strings `s` and `t` can be made identical by:

- Mapping `'e'` to `'a'`.
- Mapping `'g'` to `'d'`.

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        int n=s.length();

        if(s.length()!=t.length()){
            return false;
        }

        HashMap<Character, Character> ss=new HashMap<>();
        HashMap<Character, Character> st=new HashMap<>();

        for(int i=0; i<n; i++){
            char c1=s.charAt(i);
            char c2=t.charAt(i);

            if(ss.containsKey(c1)){
                if(ss.get(c1)!=c2){
                    return false;
                }
            }
            else{
                ss.put(c1, c2);
            }

            if(st.containsKey(c2)){
                if(st.get(c2)!=c1){
                    return false;
                }
            }
            else{
                st.put(c2, c1);
            }
        }
        return true;
    }

}
```

## 12. Longest Common Prefix (14)

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {

        if(strs==null || strs.length==0){
            return "";
        }

        String prefix=strs[0];

        for(int i=1; i<strs.length; i++){
            String current=strs[i];
            int j=0;

            while(j<prefix.length() && j< current.length() && prefix.charAt(j)==current.charAt(j)){
                j++;
            }
            prefix=prefix.substring(0,j);

            if(prefix.isEmpty()){
                return "";
            }
        }
        return prefix;
    }
}
```

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {

        if(strs==null || strs.length==0){
            return "";
        }

        String prefix=strs[0];

        for(int i=1; i<strs.length; i++){
          while(!strs[i].startsWith(prefix)){
            prefix=prefix.substring(0, prefix.length()-1);
          }

            if(prefix.isEmpty()){
                return "";
            }
        }
        return prefix;
    }
}
```

## 13. Rotate Strings (796)

Given two strings `s` and `goal`, return `true` *if and only if* `s` *can become* `goal` *after some number of **shifts** on* `s`.

A **shift** on `s` consists of moving the leftmost character of `s` to the rightmost position.

- For example, if `s = "abcde"`, then it will be `"bcdea"` after one shift.

**Example 1:**

```
Input: s = "abcde", goal = "cdeab"
Output: true
```

Method 1 - for Logic

```java
class Solution {
    public boolean rotateString(String s, String goal) {
       /* if one string is roated of another string then after addimg the same string we will get the 
       remiang part of of that string */

       if(s.length()!=goal.length()){
        return false;
       }

       int n=s.length();
       for(int i=0; i<n; i++){
        String rotated=s.substring(i)+s.substring(0, i);

        if(rotated.equals(goal)){
            return true;
        }
       }
       return false;
    }
}
```

Method 2- ShortCut

```java
class Solution {
    public boolean rotateString(String s, String goal) {
       
    if(s.length()!=goal.length()){
        return false;
    }
    /* if one string is roated of another string then after addimg the same string we will get the 
       remiang part of of that string */
       String sub=s+s;
        return sub.contains(goal);
    }
}
```

## 14. Maximum Nesting Depth of the Parenthesis (1614)

Given a **valid parentheses string** `s`, return the **nesting depth** of **`s`. The nesting depth is the **maximum** number of nested parentheses.

**Example 1:**

**Input:** s = "(1+(2*3)+((8)/4))+1"

**Output:** 3

**Explanation:**

Digit 8 is inside of 3 nested parentheses in the string.

```java
class Solution {
    public int maxDepth(String s) {
        int st=0;
        int count=0;
        for(int i=0; i<s.length(); i++){
            char c=s.charAt(i);
           if(c=='('){
            st++;
            count=Math.max(st, count);
           }
           else if(c==')'){
            st--;
           }
            
        }
        return count;
        
    }
}
```

## 15. Sort Characters By Frequency (451)

Given a string `s`, sort it in **decreasing order** based on the **frequency** of the characters. The **frequency** of a character is the number of times it appears in the string.

Return *the sorted string*. If there are multiple answers, return *any of them*.

**Example 1:**

```
Input: s = "tree"
Output: "eert"
Explanation: 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

```java
class Solution {
    public String frequencySort(String s) {
        HashMap<Character, Integer> hm=new HashMap<>();

        for(char ch:s.toCharArray()){
            hm.put(ch, hm.getOrDefault(ch, 0)+1);
        }
        
        ArrayList<Character> list=new ArrayList<>(hm.keySet());
        //put only unique chars in list
        //list={t,r,e}

        Collections.sort(list, (a,b)->hm.get(b)-hm.get(a));
        //Sort it based on thier freq

        StringBuilder sb=new StringBuilder();
        for(char i:list){
            //return no of time the string which has its freq
            for(int j=0; j<hm.get(i); j++){
                 sb.append(i);
            }
           
        }
        return sb.toString();
    }
}
```

## 16. Roman to Integer (13)

**Example 1:**

```
Input: s = "III"
Output: 3
Explanation: III = 3.
```

```java
class Solution {
    public int romanToInt(String s) {
        int res=0;
        HashMap<Character, Integer>hm=new HashMap<>();
        hm.put('I', 1);
        hm.put('V', 5);
        hm.put('X', 10);
        hm.put('L', 50);
        hm.put('C', 100);
        hm.put('D', 500);
        hm.put('M', 1000);

        for(int i=0; i<s.length()-1; i++){
            if(hm.get(s.charAt(i))<hm.get(s.charAt(i+1))){
                res-=hm.get(s.charAt(i));
            }
            else{
                res+=hm.get(s.charAt(i));
            }
        }
        return res+hm.get(s.charAt(s.length()-1));
    }
}
```

## 17. Integer to Roman(12)

Given an integer, convert it to a Roman numeral.

**Example 1:**

**Input:** num = 3749

**Output:** "MMMDCCXLIX"

**Explanation:**

```
3000 = MMM as 1000 (M) + 1000 (M) + 1000 (M)
 700 = DCC as 500 (D) + 100 (C) + 100 (C)
  40 = XL as 10 (X) less of 50 (L)
   9 = IX as 1 (I) less of 10 (X)
Note: 49 is not 1 (I) less of 50 (L) because the conversion is based on decimal places
```

```java
class Solution {
    public String intToRoman(int num) {
         int[] values =    {1000, 900, 500, 400, 100, 90,  50, 40,  10, 9,  5, 4, 1};
        String[] symbols ={"M",  "CM","D", "CD","C","XC","L","XL","X","IX","V","IV","I"};

        StringBuilder sb = new StringBuilder();

        // Go through each value
        for (int i = 0; i < values.length; i++) {
            while (num >= values[i]) {
                num -= values[i];
                sb.append(symbols[i]);
            }
        }

        return sb.toString();
    }
}
```

## 18. String to Integer (atoi) (8)

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

## 19. Longest Palindromic SubString (5) - Without DP

Given a string `s`, return *the longest* *palindromic* *substring* in `s`.

**Example 1:**

```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

```java
class Solution {
    public static Boolean Palindrome(String S){
        int n=S.length();
        int l=0, r=n-1;

        while(l<r){
            if(S.charAt(l++)!=S.charAt(r--)){
                return false;
            }
        }
        return true;
    }
    public String longestPalindrome(String s) {
        int n=s.length();
        if(n==0){
            return "";
        }
        int maxlen=1;
        String longest=s.substring(0,1);
        
        for(int i=0; i<n; i++){
            for(int j=i+1; j<=n; j++){
           String sub=s.substring(i,j);
           if(Palindrome(sub) && sub.length()>maxlen){
            maxlen=sub.length();
            longest=sub;
           }
        }
        }
        return longest;
    }
}
```

## 20. **Sum of Beauty of All Substrings (1781)**

The **beauty** of a string is the difference in frequencies between the most frequent and least frequent characters.

- For example, the beauty of `"abaacc"` is `3 - 1 = 2`.

Given a string `s`, return *the sum of **beauty** of all of its substrings.*

**Example 1:**

```
Input: s = "aabcb"
Output: 5
Explanation:The substrings with non-zero beauty are ["aab","aabc","aabcb","abcb","bcb"], each with beauty equal to 1.
```

```java
class Solution {
    public int beautySum(String s) {
        int totalSum=0;
        int n=s.length();

        for(int i=0; i<n; i++){
            //making a freq array for Character
            int freq[]=new int[26];

            for(int j=i; j<n; j++){
                char c=s.charAt(j);

                freq[c-'a']++;

                int max=0;
                int min=Integer.MAX_VALUE;

                for(int k=0; k<26; k++){
                    if(freq[k]>0){
                        max=Math.max(max, freq[k]);
                        min=Math.min(min, freq[k]);
                    }
                }
                totalSum=totalSum+(max-min);
            }

        }
        return totalSum;
    }
}
```