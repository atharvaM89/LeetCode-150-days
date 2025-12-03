# Notes

# Queue

- It is a type of Data Structure, which is Similar to Stack 
for visualization consider a stack which is horizontal
- For ex- People waiting for booking counter in a Queue
- Input 1, 2,3
Output 1,2,3
- The major difference is
    - stack is LIFO - last In First Out
    - In stack when we need to pop element which is in last
    - When we want to push element at that time element is inserted at the end of the stack
    
    ![image.png](image.png)
    
    - Queue is FIFO - First In First Out
    - In Queue When we want to pop the element we do that from the front
    - and when we push element it goes in rear same like Stack

![image.png](image%201.png)

# Operations

- In the Queue we use two pointers 
front - It is a fix Pointer, pointing to 1st element form the Queue
rear - It is not a fixed pointer, changed whenever new element is added in the Queue

### Add O(1)- Enqueue

- When ever we add some in Element in the Queue that Element goes at the end of the Queue and rear will point to the new element in the Queue

![image.png](image%202.png)

### Remove O(1)- Dequeue

- Deque- it is an Double Ended Queue
- Dequeue - Removing an Element

![image.png](image%203.png)

### Peek O(1)- Front

- Accessing Element which is in the Front of the Queue

# Implementation of Queue

## A. Implementation of Queue Using Array

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

## B. Circular Queue Using Array

- The Concept of Circular Queue Implemented because
the TC of Remove Operation is O(n) and we want to Decrease to O(1)
- In this type of Queue while Deleting we just Simply Move our Front Pointer to next instead of moving complete array to front

![image.png](image%204.png)

- If want to Add to some Elements in the Queue at that time we check the array is full or not 
by checking the rear position
- but here should be a condition where the rear is at the last position and there is Extra Space at Front, at that time we use

```jsx
rear=(rear+1)% size;
```

![image.png](image%205.png)

![image.png](image%206.png)

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

## C. Implementation of Queue Using Linked List

- Implementing Queue using Linked List is Very Easy
- When we need to insert new data , we need to make [tail.next](http://tail.next) =newnode 
and make new node=tail
- when we need to delete element from front just simply move head=head.next
and when no other node pointing to that node 
then that node will be automatically deleted by java’s garbage collector

![image.png](image%207.png)

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

## D. Implementation of Queue Using Java Collection Framework

```java
import java.util.*;

public class QueueUsingJCF {
    public static void main(String[] args) {
        Queue<Integer> q=new LinkedList<>();//Queueu is not a class it is just a interface 

          Queue<Integer> q=new ArrayDeque<>();
        //Queue is Either made by Linked list class or by a ArrayDequeue Class
    
         q.add(1);
         q.add(2);
         q.add(3);
        // System.out.println(q.remove());
        // System.out.println(q.peek());

         while(!q.isEmpty()){
            System.out.print(q.peek()+" ");
            q.remove();
         }
    }
}

```

## E. Implementation of Queue Using Two Stacks

- Using 2 stack means we have 2 LIFO DS
using that we want to make a Queue (FIFO)

- There are two ways to implement it  - it is not a optimized way
    - push/ add in O(n)  and Pop and peek in O(1)   or
    - push/add in O(1) and pop and peek in O(n)

- So basically it is a 3 Step process
- consider initially two stack s1 and s2 both are empty and we want to insert 1 2 3 in the stack
    - add 1 in s1 (s1 is not empty)
    - we need to add 2 in s1, so transfer 1 to s2
    - add 2 in s2, after that transfer 1 in s1
    so s1 will contain 1 and 2 and s2 is empty
    - now we need to add 3 and s1 is not empty
    - Transfer 1 and 2 to s2
    - add 3 in s2
    - transfer 1 and 2 in s1 
    now it will become the final output
    
    ![image.png](image%208.png)
    

```java
while(!s1.isEmpty()){
                s2.push(s1.pop());
            }
            s1.push(data);

            while(!s2.isEmpty()){
                s1.push(s2.pop());
            }
```

- so the steps will be
    - add new element in s1
    - s1 to s2
    - s1 push
    - s2 to s1

```java
import java.util.*;

public class QueueUsingStack{
    static class Queue{
        static Stack<Integer> s1=new Stack<>();
        static Stack<Integer> s2=new Stack<>();

        public static boolean isEmpty(){
            return s1.isEmpty();
        }

        //add  O(n)
        public static void add(int data){
            while(!s1.isEmpty()){
                s2.push(s1.pop());
            }
            s1.push(data);

            while(!s2.isEmpty()){
                s1.push(s2.pop());
            }
        }

        public static int remove(){  //O(1)
            if(s1.isEmpty()){
                System.out.println("Queue is Empty");
                return -1;
            }
            return s1.pop(); 
        }

        public static int peek(){
            if(s1.isEmpty()){
                System.out.println("Queue is Empty");
                return -1;
            }
            return s1.peek();
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

- Method 2 - Pop and peek in O(n)

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

## F. Implement Queue Using Deque

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

# Implementation of Deque

- It is an Double Ended Queue, In which insertion and deletion is happen form both the end

![image.png](image%209.png)

## Operation in Queue

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

![image.png](image%2010.png)