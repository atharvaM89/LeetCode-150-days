# Notes

![image.png](../../Images/LL%20Notes/image.png)

![image.png](../../Images/LL%20Notes/image%201.png)

![image.png](../../Images/LL%20Notes/image%202.png)

![image.png](../../Images/LL%20Notes/image%203.png)

# 1. Basic Class Implementation for Node Class

```
public static class Node{  //Creating a class which is able to give implementation for other node
        int data;  //data for the node
        Node next;  //Pointer of the Next Node

        public Node(int data){   //Make A constructor to initilize the data for the node
            this.data=data;      //initilizing data as data
            this.next=null;      //initilization next as null
        }
```

# 2. Head and Tail node in a linked list

Head node-  A head node is a node which come first in a linked list

Tail Node-   It is a node which comes last in a linked list

              - It is not be the null node, It should be the last valid node 

- Even If we don’t have a tail node then also we are able to find it because we have the head node and head node contains data of next node 
in such a way we can find the tail node by traversing it
- For head and tail of a node we need to mention them inside a main class as a property

```java
ex - public static Node head;
		 public static Node tail;
		 
		 // we have to mention the class name of the object
public class LinkedList {

    public static class Node
     {  
        int data;  
        Node next;  

        public Node(int data)
        {  
            this.data=data;      
            this.next=null;
        }
      }
public static Node head;
public static Node tail;

public static void main(Strings args[])
	{
		linkedList ll=new LinkedList();  //we have to create a obj of main class
		ll.head=new Node(1);    //initilization head
		ll.next=new Node(2);    //initilization next
	}
}
```

Note- 

- In this example we initilize the node head and tail in main function
- Insted of writing that code in main function we will create a methods in main class that is in LInkedList Class

# **3. Add element in Linked List**

we can add nodes in linked list in three types

- Add in First
- Add in last
- Add in middle

## 1. Add First

![image.png](../../Images/LL%20Notes/image%204.png)

Steps

- create new node
- new node’s next=head
- make new node=head

Base Case

There is only one case in which by adding new node in first affects tail node 
i.e when our LL is empty

At that time new node will become head and tail  

```java
public class LinkedList {

    public static class Node{  //Creating a class which is able to give implementation for other node
        int data;  //data for the node
        Node next;  //Pointer of the Next Node

        public Node(int data){   //Make A constructor to initilize the data for the node
            this.data=data;      //initilizing data as data
            this.next=null;      //initilization next as null
        }
    }

    public static Node head;
    public static Node tail;  //properites for head and tail

    public void addfirst(int data){   //we are not set it as static beacsue we do not access it directly inside a mainn fuction we will access this using obj of main class
       
       
        //step1- Create New Node
        Node newNode=new Node(data);     //creating object for a Node class

        //base Case- when LL is Empty

        if(head==null){
            head=tail=newNode;  
            return;
        } 

        //step2 - New Node's next=head
        newNode.next=head;

        //step3- newNode=head;
        head=newNode;

    }
    public static void main(String[] args) throws Exception {
        LinkedList ll=new LinkedList();
        ll.addfirst(1);
        ll.addfirst(2);
        
        
    }
}

```

Time Complexity -O(1)

![image.png](../../Images/LL%20Notes/image%205.png)

## 2. ADD in last

![image.png](../../Images/LL%20Notes/image%206.png)

Steps

- Create new Node

Base case

- tails next=new node
- tail=newNode;

Base Case

when LL is null New Node will become head and tail 

```java
 public void addLast(int data){
        //Step1- Crete a new node
        Node newNode=new Node(data);

        //base case
        if(head==null){
            head=tail=newNode;
            return;
        }

        //step2-Tail's node next=newNode
        tail.next=newNode;

        //step3- make new node tail
        tail=newNode;
    }

```

## 3. ADD in Middle

![image.png](../../Images/LL%20Notes/image%207.png)

![image.png](../../Images/LL%20Notes/image%208.png)

![image.png](../../Images/LL%20Notes/image%209.png)

Steps

- first thing we need to find is previous index
- For Previous Index-
    
    ```java
    Node temp=head;
    
    indx=2;
    i=0;
    
    while(i<indx-1){
        temp=temp.next;
        i++;
    }
    ```
    

So temp is our Previous

1. newNode.next=temp.next;
2. temp.next=newNode;

```java
public void AddMiddle(int data, int indx){

         //base case- if indx=0

         if(indx==0){
            addfirst(data);  // we call this step before creation of node because we already declared that inside addFirst
            return;
         }

        //Step1- Create New Node
        Node newNode=new Node(data);
           
            //Step 2- Find Prev - i.e temp
             Node temp=head;
            int i=0;
           

            while(i<indx-1){
                temp=temp.next;
                i++;
            }

            //Step 3- connect new node to prev node and next node

            newNode.next=temp.next;
            temp.next=newNode;
            
            //step4 - checks if the newnode's next is null if it is so then tail = newNode
            if(newNode.next==null){
                tail=newNode;
            }

    }
```

## 4. Print a Linked List

![image.png](../../Images/LL%20Notes/image%2010.png)

```java
public void print(){

        if(head==null){
            System.out.println("Linked list is Empty");
        }

        Node temp=head;
        
        while(temp!=null){
            System.out.println(temp.data+" ");
            temp=temp.next;
        }
        System.out.println();
        
    }
```

## 5. Size of a Linked List

![image.png](../../Images/LL%20Notes/image%2011.png)

1. Where we Define

```java
 public static Node head;
    public static Node tail;  //properites for head and tail
    public static int size;  //we make it int because when we change it, it should be chnage dynamically
```

1. In each Method

```java
 public void addfirst(int data){   //we are not set it as static beacsue we do not access it directly inside a mainn fuction we will access this using obj of main class
       
       
        //step1- Create New Node
        Node newNode=new Node(data);     //creating object for a Node class
        size++;
```

```java
public void addLast(int data){
        //Step1- Crete a new node
        Node newNode=new Node(data);
        size++;
```

```java
public void AddMiddle(int data, int indx){

         //base case- if indx=0

         if(indx==0){
            addfirst(data);  // we call this step before creation of node because we already declared that inside addFirst
            return;
         }

        //Step1- Create New Node
        Node newNode=new Node(data);
        size++;
```

1. Print size

```java
 System.out.println(size);
```

# **4. Remove element from Linked List**

## 1. Remove First

![image.png](../../Images/LL%20Notes/image%2012.png)

- For Removing any Element
we do not need to delete any thing
- we just need to update our head
i.e  head=head.next;
- The previous node is Automatically deleted by the Garbage Collector

There are 2 Specical case

case1-  When LL is Empty (i.e) size =0
               Sop - LL is Empty

Case 2- When the size of LL is 1 then head=tail=null;

```java
public int removeFirst(){
        if(size==0){
            System.out.println("linked List is Empty");
            return Integer.MIN_VALUE;
        }
        else if(size==1){
            int val=head.data;
            head=tail=null;
            size=0;
            return val;
        }
        
        int val=head.data;
        head=head.next;
        size--;
        return val;
    }
```

## 2. Remove Last

here we just need to update our tail 
1. we need to find prev of tail

- for prev of tail
while(i<size){
temp=temp.next;
i++;
}
- after that we need to manage aur tail
temp.next=null;
temp=tail;

There are 2 Special Cases

Case1-  When LL is Empty (i.e) size =0
               Sop - LL is Empty

Case 2- When the size of LL is 1 then head=tail=null;

```java
public void removeLast(){   //we make this fun void inseted of int (Nothing will change)
        if(size==0){
            System.out.println("Linked LIst is Empty");
        }
        else if(size==1){
            head=tail=null;
            size=0;
        }
        Node temp=head;
        int i=0;
        while(i<size-2){
            temp=temp.next;
            i++;
        }
        temp.next=null;
        tail=temp;
        size--;
    }
```

## 3. Remove element from Middle

```java
public void DeleteFromMillde(int index){
        Node temp=head;
        Node curr=head;

        if(size==0){
            System.out.println("Linked List is Empty");
        }
        else if(size==1){
            head=tail=null;
            size=0;
        }
        int i=0;
        int j=0;

        while(i<size-index-1){
            temp=temp.next;
            i++;
        }
        while(j<size-index){
            curr=curr.next;
            j++;
        }
        temp.next=curr.next;
        size--;

        
    }

```

# 5. Slow Fast Concept

- So basically it act as two pointer concepts
- we use this concept to find middle value (mostly)

- In which initially we initilize both pointer with same value
slow=head
fast=head;

- slow one increase by less values(ex by 1)     - turtle
fast one increase by more values (ex by 2)    -hare
- CASE 1- even case
    
    while(fast≠null)
    when fast pointer points to null
    slow pointer = middle value 
    

![image.png](../../Images/LL%20Notes/image%2013.png)

- CASE 2-  Odd case

while(fast.next≠null)

when [fast.next](http://fast.next) points to null 
slow points to middle

![image.png](../../Images/LL%20Notes/image%2014.png)

```java
//Slow fast- to find the middle node

public Node FindMiddle(Node head){
        Node slow=head;
        Node fast=head;

        while(fast!=null && fast.next!=null){
            slow=slow.next;       //+1
            fast=fast.next.next;    //+2
        }
        return slow;
    }
```

# 6. Floyds Cycle Finding algorithm

- we use Slow Fast algo

![image.png](../../Images/LL%20Notes/image%2015.png)

- when we find our slow and fast is on same node that time we say 
our linked list contains loop

```java
public boolean cycle(){
        Node slow=head;
        Node fast =head;

        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
            if(fast==slow){
                return true;
            }
        }
        return false;
         
    }
```

# 7. Removing a Cycle form a LL

![image.png](../../Images/LL%20Notes/image%2016.png)

![image.png](../../Images/LL%20Notes/image%2017.png)

![image.png](../../Images/LL%20Notes/image%2018.png)

Algo  

```java
 // Step1
 Detect a Cycle

//Step2
- If Cycle detects
- move slow=head

//Step 3
- also track a prev
initilize it with null
- Run a loop 
while(slow==fast)
{
		slow+1;
		prev= fast;
		fast+1;
}

//Step 4
- Find last node 
that node node is Previous of fast (when slow and fast meets)
- prev.next=null;
```

# 8. Java Collections Frame Work

![image.png](../../Images/LL%20Notes/image%2019.png)

Basically it is a Collections in java , collections of data structure which give various inbuilt methods which prevent us to not build the things from strach 

## Linked List in JCF

- First thing we need to do is import Linked list class

```java
import java.util.LinkedList;
```

```java
			  //create
        LinkedList<Integer> list=new LinkedList<>();     //
 
        //here we do not use primitive data types because it is a object type so we declare class type ex Integer

        //add
        list.addLast(1);
        list.addFirst(0);
        list.addLast(2);

        //print
        System.out.println(list);

        //remove
        list.removeLast();
        list.removeFirst();
	
```

# 9. Merge Sort on Linked List

```java
//1. we need to find the middle of the linked list
//we will find the middle in such a way that it will be the last node of the left part
```

![image.png](../../Images/LL%20Notes/image%2020.png)

```java
//2. Divide the linked list in two parts
//by making the
         mid.next=null
//before making the null
//store mid.next in right node

//then call recursively merge sort
```

```

        //3. merge both the parts
```

### 1. Find the middle

- To find the middle of the linked list we use slow fast concept
- but there is one change in slow fast concept we get out mid as fist node of 2nd part
    
    ![image.png](../../Images/LL%20Notes/image%2021.png)
    
- But we want our mid should be the last node of 1st part
    
    ```java
            Node slow=head;
            Node fast=head.next;
    
            while(fast!=null && fast.next!=null){
                slow=slow.next;
                fast=fast.next.next;
            }
            return slow;
    ```
    
- The only change we do is we shift our fast by one initially, so in end we get our slow less by one 
that is the last node of the first part

```java
public static Node getMid(Node head){
        Node slow=head;
        Node fast=head.next;

        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        return slow;
    }
```

### 2. Divide the Linked list in two parts

- we store the next node of mid in rightHead and make it as head of 2nd list
- make the next pointer of the mid to null

```java
Node rightHead=mid.next;
        mid.next=null;
```

### 3. Call recursively MergeSort

```java
  MergeSort(head) //left part
        MeregSort(rightHead) //right part
```

```java
 public static Node MergeSort(Node head){

        //boundary case
        if(head==null || head.next==null){
            return head;
        }

        //find middle
        Node mid=getMid(head);

        //break the list in two parts
        Node rightHead=mid.next;
        mid.next=null;
        Node newleft=MergeSort(head);
        Node newRight=MergeSort(rightHead);

        //merge 
        return Merge(newleft, newRight);

    }
```

### 4. Merge Both the list

- So in this Function have 3 things
left part
right part
temp list    - we also called it as a dummy list 
                    - in that dummy list we initilize this list with -1
- we will compare both the nodes of the list and if left part node is less than right one then we will point it to next in the temp list
    
    ![image.png](../../Images/LL%20Notes/image%2022.png)
    
- what will be our final linked list in that
head=mergeedLL.next

```java
public static Node Merge(Node head1, Node head2){
        Node mergeLL=new Node(-1);       //make new LL initilized with -1
        Node temp=mergeLL;                //make temp as it head;

        while(head1!=null && head2!=null){
            if(head1.data<=head2.data){
                temp.next=head1;
                head1=head1.next;
                temp=temp.next;
            }
            else{
                temp.next=head2;
                head2=head2.next;
                temp=temp.next;
            }
        }
        while(head1!=null){
            temp.next=head1;
            head1=head1.next;
            temp=temp.next;
        }
        while(head2!=null){
            temp.next=head2;
            head2=head2.next;
            temp=temp.next;
        }
        return mergeLL.next;
    }

```

# 10. Zig Zag Linked List

- In zig zag we have to point the last node after the first one and after that we have to point the 2nd node after that last 2nd and goes on

![image.png](../../Images/LL%20Notes/image%2023.png)

![image.png](../../Images/LL%20Notes/image%2024.png)

```java
	//1. find mid Node (last node of 1st part)
  //2. Reverse the 2nd part 
  //3. Alternate Merging
```

- We need 4 Node
Node leftHead     - points to head of 1st half
Node rightHead       - points to head to 2nd half which is reverse LL
Node nextleft               -points to next node of the left part        - only define it do not initilize it
Node nextright              -points to next node of the right part        - only define it do not initilize it

```
//we know the code for finding mid and reversing
//Alternate Merging
    while(leftHead != null && rightHead!=null){
        nextleft=leafthead.next;
        lefthead.next=rightHead;
        nextright=rightHead.next;
        righthead.next=nextleft;

        //update
        righthead=nextright;
        leftHead=nextleft;
    }
        
    }

```

![image.png](../../Images/LL%20Notes/image%2025.png)

# 11. Doubly Linked List

- In Doubly Linked List It has Contains 3 
Data of the Node
Pointer to the Next
Pointer to the previous

![image.png](../../Images/LL%20Notes/image%2026.png)

![image.png](../../Images/LL%20Notes/image%2027.png)

```java
 public class Node{
        int data;
        Node next;
        Node prev;

        public Node(int data){
            this.data=data;
            this.next=null;
            this.prev=null;
        }
    }
    public static Node head;
    public static Node tail;
    public static int size;
    
    public void addFirst(int data){
        Node newNode=new Node(data);
        size++;

        if(head==null){
            head=tail=newNode;
            return; 
        }

        newNode.next=head;
        head.prev=newNode;
        head=newNode;
    }

    public void addLast(int data){
        Node newNode=new Node(data);

        if(head==null){
            head=tail=newNode;
            return;
        }

        tail.next=newNode;
        newNode.prev=tail;
        tail=newNode;
    }
    public void removeFirst(){
        if(head==null){
            System.out.println("LL is empty");
            return;
        }
        else if(head.next==null){
            head=tail=null;
            size--;
            return;
        }
        head=head.next;
        head.prev=null;
        size--;
    }
    public void removeLast(){
        if(head==null){
            System.out.println("LL is Empty");
            return;
        }
        else if(head.next==null){
            head=tail=null;
            size--;
            return;
        }
        tail=tail.prev;
        tail.next=null;
        size--;

    }
```

# 12. Reverse Doubly Linked List

```java
public void reverseList(){
        Node prev=null;
        Node curr=tail=head;
        Node next;

        while(curr!=null){

            //old reversing 
            next=curr.next;
            curr.next=prev;

            //additonal change
            curr.prev=next;
            
            prev=curr;
            curr=next;
        }
        head=prev;
    }
```

# 13. Circular Linked List

- It is Formed when the last node of the list is Connected to first node Forming a cycle

![image.png](../../Images/LL%20Notes/image%2028.png)

- It can be single circular linked list or Doubly circular linked list
- There will two types of circular linked list
one is Singular circular Linked list
another is Doubly Circular Linked List
