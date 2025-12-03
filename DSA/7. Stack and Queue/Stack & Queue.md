# Stack & Queue

# Stack

### - Implementation of Stack using Array List

- Array is of Fixed length, if we use array so our stack is also of fixed length
- There are so many limitations by using array
    - we can make a stack of N Size
    - every time while inserting element in array we need to check wheather the stack is full or not

```java
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

```

### -Implementation Using Linked List

- here what happens when we add any Node/ data in the Linked list then what happen is that data/node  get added in the front so 
so when we need to delete data so at that time we will simply delete form the start which is our head
which is recently updated

```java
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
        }0
```

### -Implement Stack Using Deque

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

### -Push Element at Bottom of Stack

- When ever we push element in the stack we push at top 
but in this we need to push element at the bottom

![image.png](image.png)

- Step 1- using recursion we need to make stack empty and end push our element and insert the element which is already present in the stack in the same order

![image.png](image%201.png)

![image.png](image%202.png)

```java
public class pushBottom {
    public static void pushAtBottom(Stack<Integer> s, int n){
        if(s.isEmpty()){
            s.push(n);
            return;
        }
        int top=s.pop();
        pushAtBottom(s, n);
        s.push(top);
    }
```

### -Reverse a String Using Stack

![image.png](image%203.png)

```java
    public static String reverseString(String str){
         Stack<Character> s=new Stack<>();

         int idx=0;

         while(idx<str.length()){
            s.push(str.charAt(idx));
            idx++;
         }

         StringBuilder sb=new StringBuilder();

         while(!s.isEmpty()){
            char curr=s.pop();
            sb.append(curr);
         }
         return sb.toString();
    }
```

### -Reverse a Stack

- What we do is Create new Stack and pop element one by one and add push that element in new stack in that way we can reverse our stack
- In this approach we use extra memory
so we use Recursion So using recursion what we do is 
pop element one by one until the Stack get empty when it get empty we start putting element in the reverse order, so we can able to reverse our stack

![image.png](image%204.png)

![image.png](image%205.png)

- When the stack get empty we start pushing element at the bottom of the stack

![image.png](image%206.png)

```java

    public static void pushAtBottom(Stack<Integer> s, int n){
        if(s.isEmpty()){
            s.push(n);
            return;
        }
        int top=s.pop();
        pushAtBottom(s, n);
        s.push(top);

    }

    public static void reverseStack(Stack<Integer> s){
        if(s.isEmpty()){
            return;
        }
        int top=s.pop();
        reverseStack(s);
        pushAtBottom(s, top);
    }
    public static void print(Stack<Integer> s) {
        while(!s.isEmpty()){
            int top=s.pop();
            System.out.print(top+" ");
        }
    }
```

### #Conversions

### -Infix to Postfix

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
//O(n)/
```

### -Infix to Prefix

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

### -Postfix to Infix

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

### -Prefix to Infix

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

### -Postfix to Prefix

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

### -Prefix to Postfix

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

# Queue

### -Implementation of Queue Using Array

- Array is of Fixed Size, so we can only add N elements in the Array
- The Time Complexity of Remove Operation using Array is O(n), which is not idea
- so we try to avoid making queue using Array

```java
public class QueueUsingArray {
    static class Queue{
        static int arr[];
        static int size;
        static int rear;

        Queue(int n){
            arr=new int[n];
            size=n;
            rear=-1;
        }

        public static boolean isEmpty(){
            return rear==-1;
        }

        public static void add(int data){   O(1)
            if(rear==size-1){
                System.out.println("Queueu is Full");
                return;
            }
            rear++;
            arr[rear]=data;
        }

        public static int remove(){     O(n)
            if(isEmpty()){ 
                System.out.println("Queue is Empty");
                return -1;
            }
            int front=arr[0];
            for(int i=0; i<rear; i++){
                arr[i]=arr[i+1];
            }
            rear--;
            return front;
        }

        public static int peek(){   O(1)
            if(isEmpty()){
                return -1;
            }
            return arr[0];
        }

        public static void print(){
            for(int i=0; i<size;i++){
                System.out.println(arr[i]+" ");
            }
        }
    }
    public static void main(String[] args) {
        Queue q=new Queue(5);
        q.add(10);
        q.add(20);
        q.print();
    }
}

```

### -Implementation of Circular Queue Using Array

- The Concept of Circular Queue Implemented because
the TC of Remove Operation is O(n) and we want to Decrease to O(1)
- In this type of Queue while Deleting we just Simply Move our Front Pointer to next instead of moving complete array to front

![image.png](image%207.png)

- If want to Add to some Elements in the Queue at that time we check the array is full or not 
by checking the rear position
- but here should be a condition where the rear is at the last position and there is Extra Space at Front, at that time we use

```jsx
rear=(rear+1)% size;
```

![image.png](image%208.png)

![image.png](image%209.png)

- In this case, if 8 will remove then front should be at last, so front will be

```jsx
front =( front +1)% size;
```

```java
public class CircularQueueUsingArray {
    static class Queue{
       static int arr[];
       static int size;
       static int rear;
       static int front;

       Queue(int n){
        arr=new int[n];
        size=n;
        rear=-1;
        front=-1; 
       }

       public static boolean isEmpty(){
        return rear==-1 && front ==-1;
       }

       public static boolean isFull(){
         return (rear+1)%size== front;
       }

       public static void add(int data){
        if(isFull()){
            System.out.println("Queue is Full");
            return;
        }

        //adding 1st element
        if(front==-1){
            front=0;
        }
        rear=(rear+1)%size;
        arr[rear]=data;
       }

       public static int remove(){
        if(isEmpty()){
            System.out.println("Queue is Empty");
            return -1;
        }   
        
        
        int result=arr[front];
        

        if(rear==front){
            rear=front=-1;
        }
        else{
            front=(front+1)%size;
        }
        return result;
       }

       public static int peek(){
        if(isEmpty()){
            System.out.println("Queue is Empty");
        }
        return arr[front];
       }

        public static void print(){
            for(int i=0; i<size;i++){
                System.out.println(arr[i]+" ");
            }
        }
    }
    public static void main(String[] args) {
         Queue q=new Queue(3);
	       q.add(1);
        q.add(2);
        q.add(3);
        System.out.println(q.remove());
        q.add(4);
        System.out.println(q.remove());
        q.add(5);
        q.print();

    }
}

```

### -Implementation of Queue using Linked List

- Implementing Queue using Linked List is Very Easy
- When we need to insert new data , we need to make [tail.next](http://tail.next) =newnode 
and make new node=tail
- when we need to delete element from front just simply move head=head.next
and when no other node pointing to that node 
then that node will be automatically deleted by java’s garbage collector

![image.png](image%2010.png)

```java
public class QueueUsingLinkedList{
    static class Node{
        int data;
        Node next;

        Node(int data){
            this.data=data;
            this.next=null;
        }
    }

    static class Queue{
        static Node head=null;
        static Node tail=null;

        public static boolean isEmpty(){
            return head==null && tail==null;
        } 

        public static void add(int data){
            Node newNode=new Node(data);
            if(isEmpty()){
                head=tail=newNode; 
            }
            tail.next=newNode;
            tail=newNode;
        }
        public static int remove(){
            if(isEmpty()){
                System.out.println("Queue is Empty");
                return -1;
            }
            int first=head.data;

            if(tail==head){
                head=tail=null;
            }
            else{
            head=head.next;

            }
            return first;
        }

        public static int peek(){
            if(isEmpty()){
                System.out.println("Queue is Empty");
                return -1;
            }
            return head.data;
        }
    }
    public static void main(String[] args) {
        
        Queue q=new Queue();
        q.add(1);
        q.add(2);
        q.add(3);

        while(!q.isEmpty()){
            System.out.println(q.peek());
            q.remove();
        }
    }
}

```

### -Implementation of Deque

- It is an Double Ended Queue, In which insertion and deletion is happen form both the end

![image.png](image%2011.png)

### Operation in Queue

- addFirst() - add Element in the start of the Queue
- addLast()- add Element at the end of the Queue
- removeFirst()- Remove Element from the Start of the Queue
- removeLast()- Removing Element from the last of the Queue
- getFirst()- It is Similar to Peek, just getting Element form the start of the Queue’
- getLast()- It is Peeking element form end of the Queue

```java
import java.util.*;
public class Dequeimplementation{
    public static void main(String[] args) {
      Deque<Integer> d=new LinkedList<>();

        d.addFirst(1);
        d.addFirst(2);
        System.out.println(d);
        d.addLast(3);
        d.addLast(4);
        System.out.println(d.getFirst());
        System.out.println(d.getLast());
        d.removeFirst();
        d.removeLast();

        System.out.println(d);
    }
}
```

![image.png](image%2012.png)

### -Implementation of Queue Using Deque

- add- O(1)
- REMOVE- O(1)
- peek- O(1)

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

### -Queue Reversal

```java
import java.util.*;

public class QueueReversal {
    public static void reversal(Queue<Integer> q){
        Stack<Integer> s=new Stack<>();

        while(!q.isEmpty()){
            s.push(q.remove());
        }
        while(!s.isEmpty()){
            q.add(s.pop());
        }
    }
    public static void main(String[] args) {
        Queue<Integer> q=new LinkedList<>();
        for(int i=1; i<=5; i++){
            q.add(i);
        }
        reversal(q);
        while(!q.isEmpty()){
            System.out.print(q.remove()+" ");
        }
    }
}

```

# Questions

## 1. Implementation of Stack Using Queue(225)

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (`push`, `top`, `pop`, and `empty`).

Implement the `MyStack` class:

- `void push(int x)` Pushes element x to the top of the stack.
- `int pop()` Removes the element on the top of the stack and returns it.
- `int top()` Returns the element on the top of the stack.
- `boolean empty()` Returns `true` if the stack is empty, `false` otherwise.

**Notes:**

- You must use **only** standard operations of a queue, which means that only `push to back`, `peek/pop from front`, `size` and `is empty` operations are valid.
- Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.

**Example 1:**

```
Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False

```

### -Method 1

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
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

### -Method 2

```java
class MyStack {

    Queue<Integer> q1;
    Queue<Integer> q2;

    public MyStack() {
        q1=new LinkedList<>();
        q2=new LinkedList<>();
    }
    
    public void push(int x) {
        if(!q1.isEmpty()){
            q1.add(x);
        }
        else{
            q2.add(x);
        }
    }
    
    public int pop() {
        if(empty()){
            return -1;
        }

        int top=-1;

        //case 1- q1 contains all element
        if(!q1.isEmpty()){
            while(!q1.isEmpty()){
                top=q1.poll();

                if(q1.isEmpty()){
                    break;
                }

                q2.add(top);
            }
        }
        //case 2- q2 contains all element
        else{
            while(!q2.isEmpty()){
                top=q2.poll();

                if(q2.isEmpty()){
                    break;
                }
                q1.add(top);
            }
        }
        return top;
    }
    
    public int top() {
        if(empty()){
            return -1;
        }

        int top=-1;

        if(!q1.isEmpty()){
            while(!q1.isEmpty()){
                top=q1.poll();
                q2.add(top);
            }
        }
        else{
            while(!q2.isEmpty()){
                top=q2.poll();
                q1.add(top);
            }
        }
        return top;
    }
    
    public boolean empty() {
        return q1.isEmpty() && q2.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

## 2. Implementation of Queue Using Stack(232)

### -Method 1

```java
class MyQueue {
    Stack<Integer> s1;
    Stack<Integer> s2;
    public MyQueue() {
        s1=new Stack<>();
        s2=new Stack<>();
    }
    
    public void push(int x) {
        while(!s1.isEmpty()){
            s2.push(s1.pop());
        }
        s1.push(x);
        while(!s2.isEmpty()){
            s1.push(s2.pop());
        }

    }
    
    public int pop() {
        if(s1.isEmpty()){
            return -1;
        }
        else{
            return s1.pop();
        }
    }
    
    public int peek() {
        if(s1.isEmpty()){
            return -1;
        }
        else{
            return s1.peek();
        }
    }
    
    public boolean empty() {
        return s1.isEmpty();
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

### -Method 2

```java
class MyQueue {
    Stack<Integer> s1;
    Stack<Integer> s2;
    public MyQueue() {
        s1=new Stack<>();
        s2=new Stack<>();
    }
    
    public void push(int x) {
        s1.push(x);
        /*if(!s1.isEmpty()){
            s1.push(x);
       }
       else{
            s2.push(x);
       }*/
    }
    
    public int pop() {
        if(empty()){
            return -1;
        }
        int top=-1;

        if(!s1.isEmpty()){
            while(!s1.isEmpty()){
                top=s1.pop();

                if(s1.isEmpty()){
                    break;
                }
                s2.push(top);
            }
        }
        else{
            while(!s2.isEmpty()){
                top=s2.pop();

                if(s2.isEmpty()){
                    break;
                }
                s1.push(top);
            }
        }
        return top;
    }
    
    public int peek() {
        if(empty()){
            return -1;
        }
        int top=-1;

        if(!s1.isEmpty()){
            while(!s1.isEmpty()){
                top=s1.pop();
                s2.push(top);
            }
        }
        else{
            while(!s2.isEmpty()){
                top=s2.pop();
                s1.push(top);
            }
        }
        return top;
    }
    
    public boolean empty() {
        return s1.isEmpty() && s2.isEmpty();
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

## 3. Implement Minimum Stack (155)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Example 1:**

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

```java
class MinStack {
    Deque<Integer> d;
    public MinStack() {
        d=new LinkedList<>();
    }
    
    public void push(int val) {
        d.addLast(val);
    }
    
    public void pop() {
        d.removeLast();
    }
    
    public int top() {
        return d.getLast();
    }
    
    public int getMin() {
        int min=Integer.MAX_VALUE;
        for(int x: d){
            if(x<min){
                min=x;
            }
        }
         return min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

## 4. First Non Repeating Letter in Stream of Char

Given a string **s** consisting of only lowercase alphabets, for each index **i** in the string (0 ≤ i < n), find the first **non-repeating** character in the prefix **s[0..i]**. If no such character exists, use **'#'**.

**Examples:**

```
Input:s = "aabc"
Output:a#bb
Explanation:
At i=0 ("a"): First non-repeating character is 'a'.
At i=1 ("aa"): No non-repeating character, so '#'.
At i=2 ("aab"): First non-repeating character is 'b'.
At i=3 ("aabc"): Non-repeating characters are 'b' and 'c'; 'b' appeared first, so 'b'
```

```java
class Solution {
    public String firstNonRepeating(String s) {
      StringBuilder sb=new StringBuilder();
      
      int freq[]=new int[26];
      Queue<Character> q=new LinkedList<>(); 
      
      for(int i=0; i<s.length(); i++){
          char ch=s.charAt(i);
          
          q.add(ch);
          freq[ch-'a']++;
          
          while(!q.isEmpty() && freq[q.peek()-'a']>1){
              q.remove();
          }
          if(q.isEmpty()){
              sb.append("#");
          }
          else{
              sb.append(q.peek());
          }
      }
      return sb.toString();
        
    }
}

```

## 5. Interleave 2 half of Queue

```java
class Solution {
    public void rearrangeQueue(Queue<Integer> q) {
        int size=q.size();
        Queue<Integer> firsthalf=new LinkedList<>();
        for(int i=0; i<size/2; i++){
            firsthalf.add(q.remove());
        }
        
        while(!firsthalf.isEmpty()){
            q.add(firsthalf.remove());
            q.add(q.remove());
        }
        
    }
}

```

## 6. Stock Span Problem (901)

The stock span problem is a financial problem where we have a series of daily price quotes for a stock and we need to calculate the span of stock price for all days.You are given an array **arr[]** representing daily stock prices, the stock span for the **i-th** day is the number of consecutive days up to day i (including day i itself) for which the price of the stock is **less than or equal** to the price on day **i**. Return the span of stock prices for each day in the given sequence.

**Examples:**

```
Input: arr[] = [100, 80, 90, 120]
Output: [1, 1, 2, 4]
Explanation: Traversing the given input span 100 is greater than equal to 100 and there are no more days behind it so the span is 1, 80 is greater than equal to 80 and smaller than 100 so the span is 1, 90 is greater than equal to 90 and 80 so the span is 2, 120 is greater than 90, 80 and 100 so the span is 4. So the output will be [1, 1, 2, 4].
```

![Screenshot 2025-11-27 130544.png](Screenshot_2025-11-27_130544.png)

- In this Type of Problem the Stock price of the company is Given in the form of Graph/ Candle or anything 
it define the the price of stock in that day

![image.png](image%2013.png)

- Stock is Given in the problem 
Span - we need to calculate it by our own

for ex- today some stock value is 100 
so before today how many consecutive days the` stock price is less than or equal to this price

![image.png](image%2014.png)

- for span Consider for 70 and 80
is 70≤60- no 
is 70≤80 -yes
for that we will store previous high
- so For calculating this previous high we need O(n)
and our overall problem will take O(N^2) 
for that we use stack

![image.png](image%2015.png)

![image.png](image%2016.png)

![image.png](image%2017.png)

```java
class Solution {
    public ArrayList<Integer> calculateSpan(int[] arr) {
        
        ArrayList<Integer> span=new ArrayList<>();
        int n=arr.length;
        
        Stack<Integer> s=new Stack<>();
        
        span.add(1);
        s.push(0);
        
        for(int i=1; i<n; i++){
            int curr=arr[i];
            
            while(!s.isEmpty()&& curr>=arr[s.peek()]){
                s.pop();
            }
            if(s.isEmpty()){
                span.add(i+1);
            }
            else{
                int prevHigh=s.peek();
                span.add(i-prevHigh);
            }
            s.push(i);
        }
        return span;
        
    }
}
```

```java
import java.util.Stack;

class StockSpanner {
    public Stack<int[]> st;

    public StockSpanner() {
        st = new Stack<>();
    }

    public int next(int price) {
        int span = 1;

        while (!st.isEmpty() && st.peek()[0] <= price) {
            span += st.pop()[1];
        }

        st.push(new int[]{price, span});
        return span;
    }
}

```

## 7. Next Greater Element (496)

The **next greater element** of some element `x` in an array is the **first greater** element that is **to the right** of `x` in the same array.

You are given two **distinct 0-indexed** integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return *an array* `ans` *of length* `nums1.length` *such that* `ans[i]` *is the **next greater element** as described above.*

**Example 1:**

```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
```

![image.png](image%2018.png)

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

![image.png](image%2019.png)

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

![image.png](image%2020.png)

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int n1=nums1.length;
        int n2=nums2.length;
        int res[]=new int[n1];

        Stack<Integer> s=new Stack<>();
        HashMap<Integer, Integer> hm=new HashMap<>();

        for(int i=n2-1; i>=0; i--){
            int val=nums2[i];
            while(!s.isEmpty() && s.peek()<val){
                s.pop();
            }

            if(s.isEmpty()){
               hm.put(val, -1);
            }
            else{
                hm.put(val, s.peek());
            }
            s.push(val);
        }
         for (int i = 0; i < n1; i++) {
            res[i] = hm.getOrDefault(nums1[i], -1);
        }
        return res;
    }
}
```

### -Next Greater Element {Left}

```java
public class NextGreaterElement {
    public static int[] nextgre(int arr[], int nextGreater[]){

        Stack<Integer> s=new Stack<>();
        int n=arr.length;
        for(int i=0; i<=n; i--){
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

### -Next Smallest Element {Right}

```java
public class NextGreaterElement {
    public static int[] nextgre(int arr[], int nextGreater[]){

        Stack<Integer> s=new Stack<>();
        int n=arr.length;
        for(int i=n-1; i>=0; i--){
            while(!s.isEmpty()&& s.peek()>=arr[i]){
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

### -Next Smallest Element {Left}

```java
public class NextGreaterElement {
    public static int[] nextgre(int arr[], int nextGreater[]){

        Stack<Integer> s=new Stack<>();
        int n=arr.length;
        for(int i=0; i<n; i--){
            while(!s.isEmpty()&& s.peek()>=arr[i]){
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

## 8. Next Greater Element II (503)

Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return *the **next greater number** for every element in* `nums`.

The **next greater number** of a number `x` is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.

**Example 1:**

```
Input: nums = [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2;
The number 2 can't find next greater number.
The second 1's next greater number needs to search circularly, which is also 2.
```

- It is a same problem like Next Greatest Element but here the difference is this array is circular 
for ex- consider for a 1, 1 next greatest element is 2 not -1, it is because of circular array
- so in this problem instead of traversing the array twice for the next greatest element we can make a new array of double the size and store same content but in repeated manner , which reduces the TC to O(n) insted of O(n2)

- so After making array at the time of mapping 
there will be one problem that is the new array will be of size 2N and our stack and answer array is of size n 
so mapping will be not proper
so we use

```jsx
index=i% n;
```

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n=nums.length;
        int res[]=new int[n];
        Stack<Integer> s=new Stack<>();

        for(int i=((2*n)-1); i>=0 ; i--){
            while(s.size()>0 && nums[s.peek()]<=nums[i%n]){
                s.pop();
            }
            if(s.isEmpty()){
                res[i%n]=-1;
            }
            else{
                res[i%n]=nums[s.peek()];
            }
            s.push(i%n);
        }
        return res;
    }
}
```

## 9. Duplicate Parenthesis

![image.png](image%2021.png)

```java
import java.util.*;

public class DuplicateParenthesis {
    public static boolean dup(String str){
        Stack<Character> s=new Stack<>();

        for(int i=0; i<str.length(); i++){
            char c=str.charAt(i);

            //closing
            if(c==')'){
                // it is a closing bracket
                int count=0;
                while(s.pop() != '('){
                    count++;
                }
                if(count<1){
                    return true;
                }
            }
            else{
                s.push(c);
            }
        }
        return false;
    }
    public static void main(String[] args) {
        String str="((a+b))"; //true
        String str2="(a-b)";//false
        System.out.println(dup(str));
    }
}

```

## 10. Largest Rectangle in Histogram (84)

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return *the area of the largest rectangle in the histogram*.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```

- The bar like structure is called as Histogram, and the width of each bar is 1

![image.png](image%2022.png)

- Consider for this much area 
how we find the boundary
if we are on 5 then right side me 5 se chote wale se just pahale wala i.e 2 ke pahale -6
and left side me bhi 5 se chote wale se just bad means 1 ke bad i.e 5 itself
- so boundary became 5 to 6 and we take min of it 
i.e min(5,6)=5 and there is 2 heights so width will be 2 
5*2= 10 area for 5
- so to calculate width we need 2 things
    - suppose while iterating in a loop we are on 5
    then we need to find New smallest left and new smallest right

![image.png](image%2023.png)

![image.png](image%2024.png)

- we write a 2 function similar to next Greater 
but the thing is here we need to write a function of next smaller in left and right
- so we make 2 array in that we store the index of next smaller in left and next smaller in right

- There is small change in code while finding next smaller right and suppose for a element we do not find smaller element in right then at that time insted of assigning -1 
we will assign that to n(length of array ) 
because we want to calculate width 
width=j-i-1 
there already exist -1 and if we also add -1 
then -1-1= -2 
which makes our answer wrong

![image.png](image%2025.png)

![image.png](image%2026.png)

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        
        int maxArea=0;
        int n=heights.length;

        Stack<Integer> s =new Stack<>();
      
        //next Smallest right
        int nsr[]=new int[n];
        for(int i=n-1; i>=0; i--){

            while(!s.isEmpty() && heights[i]<=heights[s.peek()]){
                s.pop();
            }
            if(s.isEmpty()){
                nsr[i]=n;
            }
            else{
                nsr[i]=s.peek();
            }
            s.push(i);
        }

        //next smallest lleft
        int nsl[]=new int[n];
        s=new Stack<>();
        for(int i=0; i<n ; i++){
            
            while(!s.isEmpty() && heights[i]<=heights[s.peek()]){
                s.pop();
            }
            if(s.isEmpty()){
                nsl[i]=-1;
            }
            else{
                nsl[i]=s.peek();
            }
            s.push(i);
        }

        //Area= height*wridth

        for(int i=0; i<n ;i++){
            int ht=heights[i];
            int width=nsr[i]-nsl[i]-1;

            int area=ht*width;

            maxArea=Math.max(maxArea, area);
        }
        return maxArea;
    }
}
```

## 11. Maximal Rectangle (85)

Given a `rows x cols` binary `matrix` filled with `0`'s and `1`'s, find the largest rectangle containing only `1`'s and return *its area*.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/maximal.jpg)

```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 6
Explanation: The maximal rectangle is shown in the above picture.

```

**Example 2:**

```
Input: matrix = [["0"]]
Output: 0
```

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
          if (matrix == null || matrix.length == 0) return 0;
        int n=matrix.length;
        int m=matrix[0].length;
         int[] heights = new int[m];
        int maxArea=0;

        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                
                if(matrix[i][j]=='1'){
                    heights[j]+=1;
                }
                else{
                    heights[j]=0;
                }
            }
             maxArea = Math.max(maxArea, largestRectArea(heights));
        }
        return maxArea;
    }
    public int largestRectArea(int heights[]){
        int n=heights.length;

        Deque<Integer> d=new LinkedList<>();
        int maxArea=0;

        for(int i=0; i<=n; i++){
            int h;
            if(i==n){
                h=0;
            }
            else{
                h=heights[i];
            }

            while(!d.isEmpty() && h<heights[d.getLast()]){
                int height=heights[d.removeLast()];
                int width;
                if(d.isEmpty()){
                    width=i;
                }
                else{
                    width=i-d.getLast()-1;
                }
                maxArea=Math.max(maxArea, height*width);
            }
            d.addLast(i);

        }
        return maxArea;
    }
}
```

## 12. Simplify Path(71)

You are given an *absolute* path for a Unix-style file system, which always begins with a slash `'/'`. Your task is to transform this absolute path into its **simplified canonical path**.

The *rules* of a Unix-style file system are as follows:

- A single period `'.'` represents the current directory.
- A double period `'..'` represents the previous/parent directory.
- Multiple consecutive slashes such as `'//'` and `'///'` are treated as a single slash `'/'`.
- Any sequence of periods that does **not match** the rules above should be treated as a **valid directory or** **file name**. For example, `'...'` and `'....'` are valid directory or file names.

The simplified canonical path should follow these *rules*:

- The path must start with a single slash `'/'`.
- Directories within the path must be separated by exactly one slash `'/'`.
- The path must not end with a slash `'/'`, unless it is the root directory.
- The path must not have any single or double periods (`'.'` and `'..'`) used to denote current or parent directories.

Return the **simplified canonical path**.

**Example 1:**

**Input:** path = "/home/"

**Output:** "/home"

**Explanation:**

The trailing slash should be removed.

**Example 2:**

**Input:** path = "/home//foo/"

**Output:** "/home/foo"

**Explanation:**

Multiple consecutive slashes are replaced by a single one.

**Example 3:**

**Input:** path = "/home/user/Documents/../Pictures"

**Output:** "/home/user/Pictures"

**Explanation:**

A double period `".."` refers to the directory up a level (the parent directory).

**Example 4:**

**Input:** path = "/../"

**Output:** "/"

**Explanation:**

Going one level up from the root directory is not possible.

**Example 5:**

**Input:** path = "/.../a/../b/c/../d/./"

**Output:** "/.../b/d"

**Explanation:**

`"..."` is a valid name for a directory in this problem.

![image.png](image%2027.png)

```java
class Solution {
    public String simplifyPath(String path) {
        String arr[]=path.split("/");
        Stack<String> st=new Stack<>();
        for(String i:arr){
            if(i.equals("..") && !st.empty()){
                st.pop();
            }
            else if(!i.equals("") && !i.equals(".") && !i.equals("..")){
                st.push(i);
            }
        }

        StringBuilder sb=new StringBuilder();
        for(String i:st){
            sb.append("/");
            sb.append(i);
        }
        if(sb.length()==0){
            return "/";
        }
        else{
             return sb.toString();
        }
       
    }
}
```

## 13. Decode a String(394)

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `105`.

**Example 1:**

```
Input: s = "3[a]2[bc]"
Output: "aaabcbc"

```

**Example 2:**

```
Input: s = "3[a2[c]]"
Output: "accaccacc"

```

**Example 3:**

```
Input: s = "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"
```

```java
class Solution {
    public String decodeString(String s) {
        StringBuilder sb=new StringBuilder();
        Stack<Character> chr=new Stack<>();
        Stack<Integer> count=new Stack<>();

        int num=0;
         //If we found number push on a count stack
       //If we found a anything else than "]" push it on a chr stack

       //If we get "[", start poppoing from chr stack until we get "]"

        for(int i=0; i<s.length(); i++){
            char ch=s.charAt(i);

            if(Character.isDigit(ch)){
                num=num*10+(ch-'0');//makes char to int
            }
            else if(ch=='['){
                count.push(num);  //push the no
                num=0;
                chr.push(ch);  //push [ to mark boundary
            }
            else if(ch==']'){
                //pop string until [
                    StringBuilder sn=new StringBuilder();
                    while(!chr.isEmpty() && chr.peek()!='['){
                        sn.append(chr.pop());
                    }
                    //pop [
                    chr.pop();
                    sn.reverse();

                    int repeat=count.pop();

                    //repeat the string
                    StringBuilder sc=new StringBuilder();
                    for(int j=0; j<repeat; j++){
                        sc.append(sn);
                    }

                    //push all repeated character back to stack
                    for(char x:sc.toString().toCharArray()){
                        chr.push(x);
                    }
            }
            else{
                chr.push(ch);
            }
        }
        StringBuilder result=new StringBuilder();
        while(!chr.isEmpty()){
            result.append(chr.pop());
        }
        return result.reverse().toString();

      
    }
}
```

## 14. Tapping a Rainwater (42)

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9
```

![image.png](image%2028.png)

### Method -1

- Tc- O(n)
- SC- O(n)

```java
class Solution {
    public int trap(int[] height) {
        int n=height.length;
        int lmax[]=new int[n];
        int rmax[]=new int[n];

        //for lmax
        lmax[0]=height[0];
        for(int i=1; i<n; i++){
            lmax[i]=Math.max(lmax[i-1], height[i]);
        }

        //for rmax
        rmax[n-1]=height[n-1];
        for(int i=n-2; i>=0; i--){
            rmax[i]=Math.max(rmax[i+1], height[i]);
        }
        
        //calculate water
        int water=0;
        for(int i=0; i<n; i++){
            water+=Math.min(lmax[i], rmax[i])-height[i];
        }
        return water;
    }
}
```

### Method -2

Using 2 pointer

- TC- O(n)
- sc- O(1)

```java
class Solution {
    public int trap(int[] height) {
        int n=height.length;
        int ans=0;
        int l=0, r=n-1;
        int lmax=0, rmax=0;

        while(l<r){
            lmax=Math.max(lmax, height[l]);
            rmax=Math.max(rmax, height[r]);

            if(lmax<rmax){
                ans+=lmax-height[l];
                l++;
            }
            else{
                ans+=rmax-height[r];
                r--;
            }
        }
        return ans;
        
    }
}
```

## 15. Sum of Subarray Maximum (907)

Given an array of integers arr, find the sum of `min(b)`, where `b` ranges over every (contiguous) subarray of `arr`. Since the answer may be large, return the answer **modulo** `109 + 7`.

**Example 1:**

```
Input: arr = [3,1,2,4]
Output: 17
Explanation:
Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4].
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.
Sum is 17.

```

**Example 2:**

```
Input: arr = [11,81,94,43,3]
Output: 444
```

### -Brute Force

```java
class Solution {
    public int sumSubarrayMins(int[] arr) {
        int n=arr.length;
        int sum=0;
        int mod=(int) (1e9+7);

        for(int i=0; i<n; i++){
            int mini=arr[i];
            for(int j=i; j<n; j++){
                mini=Math.min(mini, arr[j]);
                sum+=mini%mod;
            }
        }
        return sum;
    }
}
```

### Method 2

Using Next Smaller Element

![image.png](image%2029.png)

![image.png](image%2030.png)

```java
class Solution {
    public int sumSubarrayMins(int[] arr) {
        int n=arr.length;
        int MOD=(int) (1e9+7);

      
        int nsl[]=new int[n];

        
        Stack<Integer> st=new Stack<>();
        //Next Smaller right
        int nsr[]=new int[n];
        for(int i=n-1; i>=0; i--){
            while(!st.isEmpty() && arr[i]<=arr[st.peek()]){
                st.pop();
            }
            if(st.isEmpty()){
                nsr[i]=n;
            }
            else{
                nsr[i]=st.peek();
            }
            st.push(i);
        }

        //for Next Smaller left
        st=new Stack<>();
        for(int i=0; i<n; i++){
            while(!st.isEmpty() && arr[i]<arr[st.peek()]){
                st.pop();
            }
            if(st.isEmpty()){
                nsl[i]=-1;
            }
            else{
                nsl[i]=st.peek();
            }
            st.push(i);
        }

       long total = 0L;
        for (int i = 0; i < n; i++) {
            long left = i - nsl[i];
            long right = nsr[i] - i;
            long contrib = (left * right) % MOD * (arr[i] % MOD) % MOD;
            total = (total + contrib) % MOD;
        }
        return (int)total;
    }
}
```

## 16. Asteroid Collision (735)

We are given an array `asteroids` of integers representing asteroids in a row. The indices of the asteroid in the array represent their relative position in space.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**

```
Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.

```

**Example 2:**

```
Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.

```

**Example 3:**

```
Input: asteroids = [10,2,-5]
Output: [10]
Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.
```

```java
import java.util.*;

class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Deque<Integer> stack = new ArrayDeque<>();
        
        for (int a : asteroids) {
            boolean alive = true;
            
            if (a > 0) {
                stack.addLast(a);
            } else {
            
                while (alive && !stack.isEmpty() && stack.peekLast() > 0) {
                    int top = stack.peekLast();
                    if (top < -a) {
                       
                        stack.removeLast();
                        continue;
                    } else if (top == -a) {
                       
                        stack.removeLast();
                        alive = false;
                        break;
                    } else { 
                        alive = false;
                        break;
                    }
                }
                if (alive) {
                 
                    stack.addLast(a);
                }
            }
        }
        
     
        int sz = stack.size();
        int[] res = new int[sz];
        for (int i = sz - 1; i >= 0; i--) {
            res[i] = stack.removeLast();
        }
        return res;
    }
}

```

## 17. Sum of Subarray Ranges (2104)

You are given an integer array `nums`. The **range** of a subarray of `nums` is the difference between the largest and smallest element in the subarray.

Return *the **sum of all** subarray ranges of* `nums`*.*

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

```
Input: nums = [1,2,3]
Output: 4
Explanation: The 6 subarrays of nums are the following:
[1], range = largest - smallest = 1 - 1 = 0
[2], range = 2 - 2 = 0
[3], range = 3 - 3 = 0
[1,2], range = 2 - 1 = 1
[2,3], range = 3 - 2 = 1
[1,2,3], range = 3 - 1 = 2
So the sum of all ranges is 0 + 0 + 0 + 1 + 1 + 2 = 4.
```

**Example 2:**

```
Input: nums = [1,3,3]
Output: 4
Explanation: The 6 subarrays of nums are the following:
[1], range = largest - smallest = 1 - 1 = 0
[3], range = 3 - 3 = 0
[3], range = 3 - 3 = 0
[1,3], range = 3 - 1 = 2
[3,3], range = 3 - 3 = 0
[1,3,3], range = 3 - 1 = 2
So the sum of all ranges is 0 + 0 + 0 + 2 + 0 + 2 = 4.
```

```java
import java.util.*;

class Solution {
    public long subArrayRanges(int[] nums) {
        int n = nums.length;
        return sumOfMax(nums, n) - sumOfMin(nums, n);
    }

    private long sumOfMax(int[] a, int n) {
        long res = 0L;
        Deque<Integer> st = new ArrayDeque<>();

        // next greater to right (>= pops on right)
        int[] nextGreater = new int[n];
        for (int i = n - 1; i >= 0; i--) {
            while (!st.isEmpty() && a[st.peekLast()] <= a[i]) st.removeLast();
            nextGreater[i] = st.isEmpty() ? n : st.peekLast();
            st.addLast(i);
        }

        st.clear();
        int[] prevGreater = new int[n];
        for (int i = 0; i < n; i++) {
            while (!st.isEmpty() && a[st.peekLast()] < a[i]) st.removeLast();
            prevGreater[i] = st.isEmpty() ? -1 : st.peekLast();
            st.addLast(i);
        }

        for (int i = 0; i < n; i++) {
            long left = i - prevGreater[i];
            long right = nextGreater[i] - i;
            res += (long) a[i] * left * right;
        }
        return res;
    }

    private long sumOfMin(int[] a, int n) {
        long res = 0L;
        Deque<Integer> st = new ArrayDeque<>();

        // next smaller to right (>= pops on right)
        int[] nextSmaller = new int[n];
        for (int i = n - 1; i >= 0; i--) {
            while (!st.isEmpty() && a[st.peekLast()] >= a[i]) st.removeLast();
            nextSmaller[i] = st.isEmpty() ? n : st.peekLast();
            st.addLast(i);
        }

        st.clear();
        int[] prevSmaller = new int[n];
        for (int i = 0; i < n; i++) {
            while (!st.isEmpty() && a[st.peekLast()] > a[i]) st.removeLast();
            prevSmaller[i] = st.isEmpty() ? -1 : st.peekLast();
            st.addLast(i);
        }

        for (int i = 0; i < n; i++) {
            long left = i - prevSmaller[i];
            long right = nextSmaller[i] - i;
            res += (long) a[i] * left * right;
        }
        return res;
    }
}

```

## 18. Remove K digit (402)

Given string num representing a non-negative integer `num`, and an integer `k`, return *the smallest possible integer after removing* `k` *digits from* `num`.

**Example 1:**

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.

```

**Example 2:**

```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.

```

**Example 3:**

```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

```java
class Solution {
    public String removeKdigits(String num, int k) {
        if (k >= num.length()) return "0";
        StringBuilder st = new StringBuilder(); // will act like a stack

        for (int i = 0; i < num.length(); i++) {
            char c = num.charAt(i);

           
            while (k > 0 && st.length() > 0 && st.charAt(st.length() - 1) > c) {
                st.deleteCharAt(st.length() - 1);
                k--;
            }

            st.append(c);
        }

       
        while (k > 0 && st.length() > 0) {
            st.deleteCharAt(st.length() - 1);
            k--;
        }

       
        int idx = 0;
        while (idx < st.length() && st.charAt(idx) == '0') idx++;

        String ans = (idx == st.length()) ? "0" : st.substring(idx);
        return ans;
    }
  
}

```

## 19. Generate Binary Number

Given a number **n**. The task is to generate all **binary numbers** with decimal values from **1 to n**.

**Examples:**

```
Input:n = 4
Output:["1", "10", "11", "100"]
Explanation:Binary numbers from 1 to 4 are 1, 10, 11 and 100.

```

```
Input:n = 6
Output:["1", "10", "11", "100", "101", "110"]
Explanation:Binary numbers from 1 to 6 are 1, 10, 11, 100, 101 and 110.
```

```java
class Solution {
    public ArrayList<String> generateBinary(int n) {
        ArrayList<String> result = new ArrayList<>();
        Queue<String> q = new LinkedList<>();

        q.add("1"); // first binary number

        while (n > 0) {
            String curr = q.poll();
            result.add(curr);

            // generate next two binary numbers
            q.add(curr + "0");
            q.add(curr + "1");
            
            n--;
        }

        return result;
    }
}

```

## 20. Connect N ropes with Minimum Cost

Given an array, **arr[]** of rope lengths, connect all ropes into a single rope with the **minimum total cost**. The **cost** to connect two ropes is the **sum of their lengths**.

**Examples:**

```
Input:arr[] = [4, 3, 2, 6]
Output:29
Explanation: First connect 2 and 3 to get [4, 5, 6] with a cost of 5, then connect 4 and 5 to get [9, 6] with a cost of 9, and finally connect 9 and 6 to get one rope with a cost of 15, giving a total minimum cost of 29. Any other order, such as connecting 4 and 6 first, results in a higher total cost of 38.
```

```
Input:arr[] = [4, 2, 7, 6, 9]
Output:62
Explanation:First, connect ropes 4 and 2, which makes the array [6, 7, 6, 9]. Cost of this operation 4 + 2 = 6. Next, add ropes 6 and 6, which results in [12, 7, 9]. Cost of this operation 6 + 6 = 12. Then, add 7 and 9, which makes the array [12,16]. Cost of this operation 7 + 9 = 16. And finally, add these two which gives [28]. Hence, the total cost is 6 + 12 + 16 + 28 = 62.

```

```
Input:arr[] = [10]
Output:0
Explanation: Since there is only one rope, no connections are needed, so the cost is 0.
```

```java
class Solution {
    public static int minCost(int[] arr) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int x : arr) {
            pq.add(x);
        }

        int total = 0;

        while (pq.size() > 1) {
            int a = pq.poll();
            int b = pq.poll();

            int sum = a + b;
            total += sum;

            pq.add(sum);
        }

        return total;
    }
}

```