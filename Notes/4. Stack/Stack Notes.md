# Notes

It is LIFO (Last in First Out)

- Input 1, 2,3
Output 3, 2 ,1

- We already study about stack in recursion
- That the stack it make
- That stack is known as Implict Stack (The stack which memory automatically makes it )
- The Stack we are going to Learn is Explicit Stack 
EX- Stack of Books

# A. Operations in Stack

- There are three main types of operation in stack
    1. Push ()- Inserting Element At top of the Stack
        - It is One side Operation
    2. POP ()-  Deleting Element form the Top of the stack
    3. Peek () - Accessing the top element of the stack 
    4. is Empty - It Check weather the stack is empty or not
    - All the Three operations is done in O(1) time Complexity

![image.png](../../Images/Stack%20Notes/image.png)

In all these three operation we are dealing with top i.e the element which is at the top of the stack 

# B. Implementation of Stack

- Using Array
- Using ArrayList
- Using LinkedList

### 1) Using Array List

- Array is of Fixed length, if we use array so our stack is also of fixed length
- There are so many limitations by using array
    - we can make a stack of N Size
    - every time while inserting element in array we need to check wheather the stack is full or not

```java
public class App {
    static class Stack{
        static ArrayList<Integer> list =new ArrayList<>();

        //isEmpty Operation
        public static boolean isEmpty(){
            return list.size()==0;
        }

        //Push Operation
        public static void push(int data){
            list.add(data);
        }

        //pop Operation

        public static int pop(){

            if(isEmpty()){
                return -1;
            }
            int top=list.get(list.size()-1);
            list.remove(list.size()-1);
            return top;
        }

        //peek Operation
        public static int peek(){
            if(isEmpty()){
                return -1;
            }
            return list.get(list.size()-1);   
        }
        public static void print(){
            for(int i=0; i<list.size(); i++){
                System.out.print(list.get(i)+" ");
            }
            System.out.println( );
        }
    }

```

### 2) Using Linked List

```java
public class App {

    static class Node{
         int data;
         Node next;
         Node(int data){
            this.data=data;
            this.next=null;
         }
    }

    static class Stack{
        static Node head=null;

        public static boolean isEmpty(){
            return head==null;
        }

        //push
        public static void push(int data){
            Node newNode=new Node(data);

            if(isEmpty()){
                head=newNode;
                return;
            }
            newNode.next=head;
            head=newNode;
        }

        //pop
        public static int pop(){
            if(isEmpty()){
                return -1;
            }
            int top=head.data;
            head=head.next;
            return top;
        }

        //peak
        public static int peak(){
            if(isEmpty()){
                return -1;
            }
            return head.data;
        }
        
    }

```

- here what happens when we add any Node/ data in the Linked list then what happen is that data/node  get added in the front so 
so when we need to delete data so at that time we will simply delete form the start which is our head
which is recently updated

### 3) Using Java Collection Framework

```java
import java.util.*;
public class App {
    public static void main(String[] args) throws Exception {
        Stack<Integer> s=new Stack<>();
        s.push(1);
        s.push(2);
        s.push(3);

        while(!s.isEmpty()){
            System.out.print(s.peek()+" ");
            s.pop();
        }
    }
}
```

### 4. Using 2 Queues

- Stack is LIFO and Queue if FIFO
- using Queue we need to Implement stack

![image.png](../../Images/Stack%20Notes/image%201.png)

```java

import java.util.*;

public class StackUsingQueue{
    static class Stack{
        
        static Queue<Integer> q1=new LinkedList<>();
        static Queue<Integer> q2=new LinkedList<>();

        public static boolean isEmpty(){
            return q1.isEmpty() && q2.isEmpty();
        }

        public static void push(int data){
            if(!q1.isEmpty()){
                q1.add(data);
            }
            else{
                q2.add(data);
            }
        }
        public static int pop(){
            if(isEmpty()){
                System.out.println("Stack is Empty");
                return -1;
            }
            int top=-1;

            //case 1- q1 ke aandar sarw elements hai
            if(!q1.isEmpty()){
                while(!q1.isEmpty()){
                    top=q1.remove();
                    if(q1.isEmpty()){
                        break;
                    }
                    q2.add(top);
                }
            }
            else{ // case 2- q2 ke aandar sare elem,emts hai
                while(!q2.isEmpty()){
                    top=q2.remove();
                    if(q2.isEmpty()){
                        break;
                    }
                    q1.add(top);    
                }
            }
            return top;
        }

        public static int peek(){
            if(isEmpty()){
                System.out.println("Stack is Empty");
                return -1;
            }
            int top=-1;

            //case 1- q1 ke aandar sarw elements hai
            if(!q1.isEmpty()){
                while(!q1.isEmpty()){
                    top=q1.remove();
                    q2.add(top);
                }
            }
            else{ // case 2- q2 ke aandar sare elem,emts hai
                while(!q2.isEmpty()){
                    top=q2.remove();
                    q1.add(top);    
                }
            }
            return top;
        }
    }
    public static void main(String[] args) {
        Stack s=new Stack();
        s.push(1);
        s.push(2);
        s.push(3);

        while(!s.isEmpty()){
            System.out.println(s.peek());
            s.pop();
        }
    }
}
```

- Using Method 1

```java
class MyStack {
Queue<Integer> q1;
Queue<Integer> q2;
public MyStack() {
    q1=new LinkedList<>();
    q2=new LinkedList<>();
}

public void push(int x) {
    while(!q1.isEmpty()){
        q2.add(q1.poll());
    }

    q1.add(x);

    while(!q2.isEmpty()){
        q1.add(q2.poll());
    }
}

public int pop() {
    if(q1.isEmpty()){
        return -1;
    }
    else{
        return q1.poll();
    }
}

public int top() {
    if(q1.isEmpty()){
        return -1;
    }
    else{
        return q1.peek();
    }
}

public boolean empty() {
    return q1.isEmpty();
}

```

}

/**

- Your MyStack object will be instantiated and called as such:
- MyStack obj = new MyStack();
- obj.push(x);
- int param_2 = obj.pop();
- int param_3 = obj.top();
- boolean param_4 = obj.empty();
*/

## 5. Implement Stack Using Deque

- Push - O(1)
- Pop- O(1)
- Peek- O(1)

```java
import java.util.*;

public class StackQueueUsingDeque {
    static class Stack{
        Deque<Integer> d=new LinkedList<>();

        public void push(int data){
            d.addLast(data);
        }
        public int pop(){
            return d.removeLast();
        }
        public int peek(){
            return d.getLast();
        }
    }

    static class Queue{
        Deque<Integer> d1=new LinkedList<>();

        public void add(int data){
            d1.addLast(data);
        }
        public int remove(){
           return  d1.removeFirst();
        }
        public int peek(){
            return d1.getFirst();
        }
    }
    public static void main(String[] args) {
        Stack s=new Stack();
        s.push(1);
        s.push(1);
        System.out.println(s.pop());
        System.out.println(s.peek());

        Queue q=new Queue();
        q.add(1);
        q.add(2);
        System.out.println(q.remove());
        System.out.println(q.peek());
    
    }   
}

```

# C. Stock Span Problem

![Screenshot 2025-11-27 130544.png](../../Images/Stack%20Notes/Screenshot_2025-11-27_130544.png)

- In this Type of Problem the Stock price of the company is Given in the form of Graph/ Candle or anything 
it define the the price of stock in that day

![image.png](../../Images/Stack%20Notes/image%202.png)

- Stock is Given in the problem 
Span - we need to calculate it by our own

for ex- today some stock value is 100 
so before today how many consecutive days the` stock price is less than or equal to this price

![image.png](../../Images/Stack%20Notes/image%203.png)

- for span Consider for 70 and 80
is 70≤60- no 
is 70≤80 -yes
for that we will store previous high
- so For calculating this previous high we need O(n)
and our overall problem will take O(N^2) 
for that we use stack

![image.png](../../Images/Stack%20Notes/image%204.png)

![image.png](../../Images/Stack%20Notes/image%205.png)

![image.png](../../Images/Stack%20Notes/image%206.png)

```java
 /*int Stocks[]={100, 80, 60, 70, 60, 85, 100};
 int span[]=new int[Stocks.length];*/
 
 public static void stockSpan(int Stocks[], int span[]){

        Stack<Integer> s=new Stack<>();
        span[0]=1;
        s.push(0);

        for(int i=1; i<Stocks.length; i++){
            int curr=Stocks[i];
            while(!s.isEmpty() && curr>Stocks[s.peek()]){
                s.pop();

            }
            if(s.isEmpty()){
                span[i]=i+1;
            }
            else{
                int prevHigh=s.peek();
                span[i]=i-prevHigh;
            }
            s.push(i);
        }
    }
```

# D. Next Greater Element

![image.png](../../Images/Stack%20Notes/image%207.png)

- Next Greater Element means- 1st no whose value greater than X or it is in right side of X
- How it Works
Next Greater Element of 6 is 8 so added in array
Next Greater Element of 8 is nit Exist in array, so add -1 in array
Next Greater Element of 0 is 1, so add it
Next Greater Element of 1 is 3, so add it
Next Greater Element of 3 not exist, so add -1
so the final will become
[8, -1, 1, 3, -1]
{6,  8, 0, 1, 3}- values for of the Next Greater Element

### pseudo code for Brute fore approach- O(n^2)

```jsx
for(int i=0; i<arr.length; i++){
	for(int j=i+1; j<arr.length; j++){
		if(arr[i]<arr[j])- we got next greater element 
				
			}
}
```

### Using Stack Approach

![image.png](../../Images/Stack%20Notes/image%208.png)

- We will make a new Array- next Greater of size array in which we will store our final answer
- In this next Greater Array at 0 index will store the next greater element of 1st element from arr
- 
- So in this approach, instead of traversing from start we will traverse form back means when we need to find next greater we already find the right side for that element

Steps

```jsx
while(s.isEmpty() && stack[top]<=arr[i]){
	s.pop();
}
```

### Code Dry Run

![image.png](../../Images/Stack%20Notes/image%209.png)

```java
public static int[] nextgre(int arr[], Stack<Integer>s, int nextGreater[]){
        
        int n=arr.length;
        for(int i=n-1; i>=0; i--){
            while(!s.isEmpty()&& s.peek()<arr[i]){
                s.pop();
            }

            if(s.isEmpty()){
                nextGreater[i]=-1;
            }
            else{
                nextGreater[i]=s.peek();
            }

            s.push(arr[i]);
        }
        return nextGreater;
    }
```

- There Should be Multiple Problem based on same approach like
    - Next Greater Right Side
    - Next Greater Left Side - for loop ko sidha likh do
    - Next Smaller Right - While me ≤ ke jagah pe ≥ kr do
    - Next Smaller Left - For loop sidha and ≤ to ≥

# E. Conversions

- Operator - It is any Mathematical Operator
                      like /, *, -, + etc.
- Operand- It is like variable like in Expression a+b=5
    - Here a & b is a Operand and + & = is Operator
    

### Priority Order of Operator for Conversion

- ^ :- 3
- *, / :- 2
- +, - :- 1
- Remaining = -1

### Define

- What is Infix-
    - It is a regular type of Expression, we use in Programming
    - As a word says IN, means In this Type of Expression Every Operator is inside the Operand
    - like (p + q) * (m - n)

- What is Prefix-
    - It is Used in Tree data Structure
    - As a Word define pre, means all the operator will be before the expression(operand)
    - * + pq - mn

- What is Postfix-
    - It is used in Stack based Caluculator
    - As a Word says post, means in this type of Expression all the operator will be after the expression
    - pq + mn - *

## 1. Infix to Postfix Conversion

- take a Iterator i=0
- Empty Stack s
- StringBuilder s=0;

```jsx
a+b*(c^ d-e)
```

- If Operand found Directly add it to answer
- If Operator found
    - If Operator found and Stack is Empty, then simply push that operator to the stack
    - If Operator Found and top Element of the stack contain less Priority than the Found Operator, then just push found operator to the stack
    - If Operator found and top Element of the Stack contain high Priority than the Found Element then just pop that Element and add it to the answer
    - When you found closing Bracket in the String just pop every thing before the Opening Bracket and add it to the answer
    - Don’t add Opening and Closing Brackets to the answer
    - If Iteration is done then pop all the elements from the stack and add it to the final answer one by one

![image.png](../../Images/Stack%20Notes/image%2010.png)

```jsx
abcd^e-*+
```

```java
import java.util.*;

public class InfixtoPostfix {
     public static int precedence(char op) {
        switch (op) {
            case '+':
            case '-':
                return 1;
            case '*':
            case '/':
                return 2;
            case '^':
                return 3; // highest, right-associative handled separately
            default:
                return -1;
        }
    }
    public static String infix(String str){

        
        Stack<Character> s=new Stack<>();
        StringBuilder sb=new StringBuilder();
        int n=str.length();

        for(int i=0; i<n; i++){
            char ch=str.charAt(i);
            if(Character.isWhitespace(ch)){
                continue;
            }
            //if Operator will found
            if(Character.isLetterOrDigit(ch)){
                sb.append(ch);
            }

            //It Opening Bracket found
            else if(ch== '('){
                s.push(ch);
            }
            else if(ch==')'){
                while(!s.isEmpty() && s.peek()!='('){
                    sb.append(s.pop());
                }
                //poping out opening bracket
                if (!s.isEmpty() && s.peek() == '(') {
                    s.pop();
                }
            }
            //If we found any operator
            else{
                while(!s.isEmpty() && precedence(ch)<=precedence(s.peek())){
                    if (precedence(ch) == precedence(s.peek()) && ch == '^') break;

                    sb.append(s.pop());
                  
                }
                s.push(ch);
            }
           
        }

        while(!s.isEmpty()){
           char c = s.pop();
            if (c == '(' || c == ')') continue;
            sb.append(c);
        }
        return sb.toString();

    }

    public static void main(String[] args) {
        String str=" a+b *(c ^ d-e)";
        System.out.println(infix(str));

    }
}
//O(n)
```

## 2. Infix to Prefix

- Reverse the Original String
- Convert the reversed String to Postfix
- Reverse the Answer
    - But there is Slightly Change in the condition when revere the original string just make the Opening bracket to Closing bracket and closing bracket to opening bracket

![image.png](../../Images/Stack%20Notes/image%2011.png)

```jsx
(A+B)*C-D+F

F+D-C*)B+A(

F+D-C*(B+A)
```

```java
import java.util.*;

public class InfixtoPrefix {
     public static int precedence(char op) {
        switch (op) {
            case '+':
            case '-':
                return 1;
            case '*':
            case '/':
                return 2;
            case '^':
                return 3; // highest, right-associative handled separately
            default:
                return -1;
        }
    }
    public static String Reverse(String str){
        Stack<Character> st=new Stack<>();
        StringBuilder sr=new StringBuilder();

        for(int i=0; i<str.length(); i++){
            char ch=str.charAt(i);

            if(ch=='('){
                st.push(')');
            }
            else if(ch==')'){
                st.push('(');
            }
            else{
                 st.push(ch);
            }
        }

        while(!st.isEmpty()){
            sr.append(st.pop());
        }
        return sr.toString();

    }
    public static String infix(String str){

        String rev=Reverse(str);
        Stack<Character> s=new Stack<>();
        StringBuilder sb=new StringBuilder();
        int n=rev.length();

        for(int i=0; i<n; i++){
            char ch=rev.charAt(i);
            if(Character.isWhitespace(ch)){
                continue;
            }
            //if Operator will found
            if(Character.isLetterOrDigit(ch)){
                sb.append(ch);
            }

            //It Opening Bracket found
            else if(ch== '('){
                s.push(ch);
            }
            else if(ch==')'){
                while(!s.isEmpty() && s.peek()!='('){
                    sb.append(s.pop());
                }
                //poping out opening bracket
                if (!s.isEmpty() && s.peek() == '(') {
                    s.pop();
                }
            }
            //If we found any operator
            else{
               while (!s.isEmpty() && (precedence(s.peek()) > precedence(ch))) {

                    sb.append(s.pop());
                  
                }
                s.push(ch);
            }
           
        }

        while(!s.isEmpty()){
           char c = s.pop();
           if (c == '(' || c == ')') continue;
            sb.append(c);
        }
        String postfix=sb.toString();
        String prefix=Reverse(postfix);
        return prefix;

    }

    public static void main(String[] args) {
        String str=" a+b *(c ^ d-e)";
        String str1="(A+B)*C-D+F";
        System.out.println(infix(str1));

    }
}

```

## 3. Postfix to Infix

- When you found Operand simply push it to stack
- When you found Operator
    - pop 2 operand and insert that operator inside that operand and Wrap them up inside the brackets
    - When there is not 2 operator then select one bracket and one operand and add operator inside them and wrap them up inside the brackets
    top 2 + Operator + top 1
    - When there is no 2 operand then just select both the brackets insert the operand between them and wrap both the brackets with the operator inside the brackets
- At the end there is only one element in the stack and that element is our answer
- TC= O(n )+ O(n)

![image.png](../../Images/Stack%20Notes/image%2012.png)

```jsx
	AB - DE + F */
	
	((A-B) / ((D + E)*F))
```

```java
import java.util.*; 
public class PostfixToInfix {

    public static String postfixInfix(String str){
        Stack<String> s=new Stack<>();
        for(int i=0; i<str.length(); i++){
            char ch=str.charAt(i);
            
            if(Character.isWhitespace(ch)){
                continue;
            }

            //If it is operand
            if(Character.isLetterOrDigit(ch)){
                s.push(str.valueOf(ch));
            }//It is an operator
            else{
                String t1=s.pop();
                String t2=s.pop(); 
                String ope='('+t2+str.valueOf(ch)+t1+')';
                s.push(ope);
            }
        }
        return s.peek();
    }
    public static void main(String[] args) {
        String str="AB+DE+F*/";
        System.out.println(postfixInfix(str));
    }
}

```

## 4. Prefix to Infix

- It is Different not like Reversing
- In this we will traverse from the backward form the string
- If Operand Found push it into the stack
- If Operator found]
    - Pop the 2 top element place the operator inside that operand and then wrap it up around two brackets
    but the difference is  top2 + operator + top 1
- TC= O(n1)+O(n2)

![image.png](../../Images/Stack%20Notes/image%2013.png)

```jsx
* + PQ - MN

((P + Q) * (M - N))
```

```java
    import java.util.*; 
public class PrefixToInfix {

    public static String prefixInfix(String str){
        Stack<String> s=new Stack<>();
        for(int i=str.length()-1; i>=0; i--){
            char ch=str.charAt(i);
            
            if(Character.isWhitespace(ch)){
                continue;
            }

            //If it is operand
            if(Character.isLetterOrDigit(ch)){
                s.push(str.valueOf(ch));
            }//It is an operator
            else{
                String t1=s.pop();
                String t2=s.pop(); 
                String ope='('+t1+str.valueOf(ch)+t2+')';
                s.push(ope);
            }
        }
        return s.peek();
    }
    public static void main(String[] args) {
        String str="*+pq-mn";
        System.out.println(prefixInfix(str));
    }
}
```

## 5. Postfix to Prefix

- In this Expression we will traverse normally
- whenever any operand appear directly push it to stack
- when a operator appear pop 2 top element from stack and add operator in front of the the 2 top and add the combine whole string in the stack\
- Operator+ t2+ t1

![image.png](../../Images/Stack%20Notes/image%2014.png)

```jsx
AB - DE + F * /

/ - AB * + DEF
```

```java
import java.util.*; 
public class PostfixToPrefix {

    public static String postfixPrefix(String str){
        Stack<String> s=new Stack<>();
        for(int i=0; i<str.length(); i++){
            char ch=str.charAt(i);
            
            if(Character.isWhitespace(ch)){
                continue;
            }

            //If it is operand
            if(Character.isLetterOrDigit(ch)){
                s.push(str.valueOf(ch));
            }//It is an operator
            else{
                String t1=s.pop();
                String t2=s.pop(); 
                String ope=str.valueOf(ch)+t2+t1;
                s.push(ope);
            }
        }
        return s.peek();
    }
    public static void main(String[] args) {
        String str="AB+DE+F*/";
        System.out.println(postfixPrefix(str));
    }
}
```

## 6. Prefix to Postfix

- This is kind of Similar to Postfix to Prefix
- The Difference is Here we need to Traverse from backward and instead of 
operator +t2+t1
- We need to do 
t1 + t2+ operator

![image.png](../../Images/Stack%20Notes/image%2015.png)

```jsx
/-AB*+DEF

AB - DE + F * /
```

```java
import java.util.*; 
public class PrefixToPostfix {

    public static String prefixPostfix(String str){
        Stack<String> s=new Stack<>();
        for(int i=str.length()-1; i>=0; i--){
            char ch=str.charAt(i);
            
            if(Character.isWhitespace(ch)){
                continue;
            }

            //If it is operand
            if(Character.isLetterOrDigit(ch)){
                s.push(str.valueOf(ch));
            }//It is an operator
            else{
                String t1=s.pop();
                String t2=s.pop(); 
                String ope= t1+ t2+ str.valueOf(ch);
                s.push(ope);
            }
        }
        return s.peek();
    }
    public static void main(String[] args) {
        String str="/-AB*+DEF";
        System.out.println(prefixPostfix(str));
    }
}

```

# F. LRU Cache

- It is Type of Page Replacement algorithm
- Paging is a memory management technique used by the OS
- The main Memory is divided into Fixed sized blocks called frames
- Process are divided into pages, which are loaded into frames as needed
- When a process reference a page which is not in memory that time page fault occur
- so, os will bring that page into memory, possibly by replacing another page

- so when page memory is full and new page is to be loaded, os must choose a victim page to remove and it select it based on how recently it used

- In the LRU cache we will store the values in key value pair
- Here, we use DLL, for traversal of nodes
- We use HashMap to store the Elements in key value pair

- The element which is least recently used we add it to end of the Doubly linked list
- The Element which is inserted is placed at the start of the DLL
- When we want to insert data we insert to head
- when we want to delete data we will delete form tail
