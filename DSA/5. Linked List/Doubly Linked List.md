# Doubly

# Doubly LL

## Intro

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
```

## 1. Add Node in Doubly LL

### A. Add First

```java
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
```

### B. Add in Last

```java
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
```

### C. Add in Middle

```java
public void addAtPos(int data, int position) {
    Node newNode = new Node(data);

    // Case 1: If list is empty
    if (head == null) {
        head = tail = newNode;
        return;
    }

    // Case 2: Insert at beginning
    if (position == 0) {
        newNode.next = head;
        head.prev = newNode;
        head = newNode;
        return;
    }

    // Traverse to the position where we want to insert
    Node temp = head;
    int i = 0;
    while (temp != null && i < position - 1) {
        temp = temp.next;
        i++;
    }

    // Case 3: Insert at end if position > size
    if (temp == tail || temp == null) {
        tail.next = newNode;
        newNode.prev = tail;
        tail = newNode;
        return;
    }

    // Case 4: Insert in the middle
    newNode.next = temp.next;
    newNode.prev = temp;
    temp.next.prev = newNode;
    temp.next = newNode;
}
```

## 2.. Remove Node from Doubly LL

### A.  Remove Element from First

```java
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
```

### B. Remove Element From Last

```java
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

### C. Remove Element From Middle

```java
public void removeAtPos(int position) {
    // Case 1: Empty list
    if (head == null) {
        System.out.println("Linked List is Empty");
        return;
    }

    // Case 2: Invalid position (negative)
    if (position < 0) {
        System.out.println("Invalid position!");
        return;
    }

    // Case 3: Remove first element
    if (position == 0) {
        if (head.next == null) { // only one node
            head = tail = null;
        } else {
            head = head.next;
            head.prev = null;
        }
        size--;
        return;
    }

    // Traverse to the node at the given position
    Node temp = head;
    int i = 0;
    while (temp != null && i < position) {
        temp = temp.next;
        i++;
    }

    // Case 4: If position is out of range
    if (temp == null) {
        System.out.println("Position out of range!");
        return;
    }

    // Case 5: Remove last element
    if (temp.next == null) {
        tail = tail.prev;
        tail.next = null;
    } 
    // Case 6: Remove from middle
    else {
        temp.prev.next = temp.next;
        temp.next.prev = temp.prev;
    }

    size--;
}
```

## 3. Find Length of Doubly LL

1. Where we Define 

```java
public static Node head;
public static Node tail;
public static int size;
```

1. In Each Method

```java
public void addFirst(int data) {
    Node newNode = new Node(data);
    size++;

    if (head == null) {
        head = tail = newNode;
        return;
    }

    newNode.next = head;
    head.prev = newNode;
    head = newNode;
}
```

```java
public void addLast(int data) {
    Node newNode = new Node(data);
    size++;

    if (head == null) {
        head = tail = newNode;
        return;
    }

    tail.next = newNode;
    newNode.prev = tail;
    tail = newNode;
}
```

```java
public void addAtPos(int data, int position) {
    Node newNode = new Node(data);
    size++;

    if (position == 0) {
        addFirst(data);
        return;
    }

    Node temp = head;
    int i = 0;
    while (temp != null && i < position - 1) {
        temp = temp.next;
        i++;
    }

    if (temp == null || temp.next == null) {
        addLast(data);
        return;
    }

    newNode.next = temp.next;
    newNode.prev = temp;
    temp.next.prev = newNode;
    temp.next = newNode;
}
```

1. Print it

```java
System.out.println("Length of Doubly Linked List = " + size);
```

## 4. Print Doubly LL

### A. Print From head to tail

```java
public void printForward() {
    if (head == null) {
        System.out.println("Doubly Linked List is Empty");
        return;
    }

    Node temp = head;
    System.out.print("Doubly Linked List (Forward): ");
    while (temp != null) {
        System.out.print(temp.data + " ");
        temp = temp.next;
    }
    System.out.println();
}
```

### B. Print from tail to head

```java
public void printBackward() {
    if (tail == null) {
        System.out.println("Doubly Linked List is Empty");
        return;
    }

    Node temp = tail;
    System.out.print("Doubly Linked List (Backward): ");
    while (temp != null) {
        System.out.print(temp.data + " ");
        temp = temp.prev;
    }
    System.out.println();
}
```

## 5. Reverse a Doubly LL

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

## 6. **Delete all occurrences of a given key in a doubly linked list**

You are given the **head_ref** of a doubly Linked List and a **Key**. Your task is to **delete all occurrences** of the given key if it is present and return the new DLL.

**Example1:**

```
Input:
2<->2<->10<->8<->4<->2<->5<->2
2
Output:
10<->8<->4<->5
Explanation:All Occurences of 2 have been deleted.
```

```java
// User function Template for Java

/* Structure of Doubly Linked List
class Node
{
    int data;
    Node next;
    Node prev;
    Node(int data)
    {
        this.data = data;
        next = prev = null;
    }
}*/
class Solution {
    static Node deleteAllOccurOfX(Node head, int x) {
   
      
      if(head==null ){
          return null;
      }
      
         Node temp=head;
      
      while(temp !=null){
          if(temp.data==x){
              if(temp==head){
                  head=head.next;
                  if(head!=null){
                      head.prev=null;
                  }
              }
              else{
                  temp.prev.next=temp.next;
                  if(temp.next!=null){
                      temp.next.prev=temp.prev;
                  }
              }
          }
          temp=temp.next;
      }
      return head;
        
    }
}
```

## 7. Find Pairs with given sum in doubly Linked List

Given a sorted doubly linked list of positive distinct elements, the task is to find pairs in a doubly-linked list whose sum is equal to given value **target**.

**Example 1:**

```
Input:1 <-> 2 <-> 4 <-> 5 <-> 6 <-> 8 <-> 9
target = 7
Output:(1, 6), (2,5)
Explanation:We can see that there are two pairs
(1, 6) and (2,5) with sum 7.
```

```java
/*

Definition for singly Link List Node
class Node
{
    int data;
    Node next,prev;

    Node(int x){
        data = x;
        next = null;
        prev = null;
    }
}

You can also use the following for printing the link list.
Node.printList(Node node);
*/

class Solution {
    public static ArrayList<ArrayList<Integer>> findPairsWithGivenSum(int target,
                                                                      Node head) {
  ArrayList<ArrayList<Integer>> result =new ArrayList<>();

  
  Node tail=head;
  while(tail.next!=null){
      tail=tail.next;
  }
  
  Node first=head;
  Node second=tail;
  
  
  while(first!= null && second!=null && first!=second && second.next!=first){
      int sum=first.data+second.data;
      
      if(sum==target){
          ArrayList<Integer> list=new ArrayList<>();
          list.add(first.data);
          list.add(second.data);
          result.add(list);
          
          first=first.next;
          second=second.prev;
      }
     else if (sum < target) {
                first = first.next; // Need bigger sum
            } 
            else {
                second = second.prev; // Need smaller sum
            }
  }

  return result;
        
    }
}

```

## 8. Remove Duplicates from a Sorted Doubly Linked List

Given a doubly linked list of **n** nodes sorted by values, the task is to remove duplicate nodes present in the linked list.

**Example 1:**

```
Input:
n = 61<->1<->1<->2<->3<->4
Output:
1<->2<->3<->4
Explanation:
Only the first occurance of node with value 1 is
retained, rest nodes with value = 1 are deleted.
```

```java
// User function Template for Java

class Solution {
    Node removeDuplicates(Node head) {
        if(head==null || head.next==null){
            return head;
        }
        
        Node temp=head;
        
        while(temp!=null && temp.next!= null){
            if(temp.next.data==temp.data){
                temp.next=temp.next.next;
                
                if(temp.next!=null){
                     temp.next.prev=temp;
                }
                
            }
            else{
                     temp=temp.next;
                }
        }
        return head;
    }
}
```

## 9. **Flatten a Multilevel Doubly Linked List (430)**

You are given a doubly linked list, which contains nodes that have a next pointer, a previous pointer, and an additional **child pointer**. This child pointer may or may not point to a separate doubly linked list, also containing these special nodes. These child lists may have one or more children of their own, and so on, to produce a **multilevel data structure** as shown in the example below.

Given the `head` of the first level of the list, **flatten** the list so that all the nodes appear in a single-level, doubly linked list. Let `curr` be a node with a child list. The nodes in the child list should appear **after** `curr` and **before** `curr.next` in the flattened list.

Return *the* `head` *of the flattened list. The nodes in the list must have **all** of their child pointers set to* `null`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/11/09/flatten11.jpg)

```
Input: head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
Output: [1,2,3,7,8,11,12,9,10,4,5,6]
Explanation: The multilevel linked list in the input is shown.
After flattening the multilevel linked list it becomes:

```

![](https://assets.leetcode.com/uploads/2021/11/09/flatten12.jpg)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;
}
*/

class Solution {
    public Node flatten(Node head) {
        if (head == null) return head;
        flattenDFS(head);
        return head;
    }

   
    private Node flattenDFS(Node node) {
        Node curr = node;
        Node last = null;

        while (curr != null) {
            Node nextNode = curr.next;

            // Case 1: If there is a child, flatten it first
            if (curr.child != null) {
                Node childTail = flattenDFS(curr.child); 

              
                curr.next = curr.child;
                curr.child.prev = curr;

                
                if (nextNode != null) {
                    childTail.next = nextNode;
                    nextNode.prev = childTail;
                }

             
                curr.child = null;
                last = childTail;
            } else {
                last = curr;
            }

            curr = nextNode;
        }

        return last;     }
}

```