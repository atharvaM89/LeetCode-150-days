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

## 8. Find all Anagrams in a String (438)

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