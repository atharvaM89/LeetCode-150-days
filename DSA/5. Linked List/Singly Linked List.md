# LL

# Singly LL

## Intro

```java
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
```

## 1. Add Node in LL

### A. Add in First

```java
  public void addfirst(int data){   //we are not set it as static beacsue we do not access it directly inside a mainn fuction we will access this using obj of main class
       
        //step1- Create New Node
        Node newNode=new Node(data);     //creating object for a Node class
        size++;

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
```

### B. Add in Last

```java
public void addLast(int data){
        //Step1- Crete a new node
        Node newNode=new Node(data);
        size++;

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

```java
class Solution {
    public static Node tail;

    public Node insertAtEnd(Node head, int x) {
        Node newNode = new Node(x);

        if (head == null) {
            head = tail = newNode;
            return head;
        }

        tail.next = newNode;  
        tail = newNode;       
        return head;
    }
}
```

### C. Add in Middle

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

            if(newNode.next==null){
                tail=newNode;
            }
    }

```

```java
class Solution {
    public static Node tail;

    public Node insertPos(Node head, int pos, int val) {
        Node newNode = new Node(val);

        if (pos == 0) {
            if (head == null) {
                head = tail = newNode;
                return head;
            }
            newNode.next = head;
            head = newNode;
            return head;
        }

        int i = 0;
        Node temp = head;

        while (i < pos - 1 && temp != null) {
            temp = temp.next;
            i++;
        }

        if (temp == null) {
            System.out.println("Position out of range!");
            return head;
        }

        if (temp.next == null) {
            temp.next = newNode;
            tail = newNode;
            return head;
        }

        newNode.next = temp.next;
        temp.next = newNode;

        return head;
    }
}

```

## 2. Remove Node form LL

### A. Remove First

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

### B. Remove Last

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

```java
class Solution {
    public static Node tail;
    public Node removeLastNode(Node head) {
        if(head==null){
            return null;
        }
        else if(head.next==null){
            head=tail=null;
            return null;
        }
        Node temp=head;
        while(temp.next.next!=null){
            temp=temp.next;
        }
        temp.next=null;
        tail=temp;
        return head;
        
    }
}
```

### C. Remove Form Middle

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

## 2. Delete Node in Linked List(237)

```
Input: head = [4,5,1,9], node = 5
Output: [4,1,9]
Explanation:You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.
```

![image.png](image.png)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public static ListNode head;
    public static ListNode tail;

    public void deleteNode(ListNode node) {
      
     node.val=node.next.val;
      node.next=node.next.next;
    }
}
```

## 3. Find Length of LL

### A. Iterative Traversal

```
public static int countNodes(Node head) {
    int count = 0;
    
    Node curr = head;
    while (curr != null) {

        count++;
        curr = curr.next;
    }
    return count;
}
```

### B. Recursive Traversal

```
public static int countNodes(Node head) {
    if (head == null) {
        return 0;
    }
    return 1 + countNodes(head.next);
}

```

### C. Mannual Method

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

## 4. Print Linked List

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

## 5. Search an Element in LL

### A. Iterative Search

```java
public int itrSearch(int key){
        Node temp=head;
        int i=0;
        while(temp!=null){
            if(temp.data==key){
                return i;
            }
            temp=temp.next;
            i++;
        }
        return -1;
    }
```

### B. Recursive Search

```java
   public int helper(Node  head, int key){     // this method is responisble for all the output
        if(head==null){
            return -1;
        }
             if(head.data==key){
                return 0;
            }
            int indx=helper(head.next, key);

            if(indx==-1){
                return -1;
            }
            return indx+1;
        
    }
    public int recSearch(int key){     // this method is used only for abstraction we can also elimnate this
        return helper(head, key);
    }

```

## 6. Middle of Linked List (876)

Given the `head` of a singly linked list, return *the middle node of the linked list*.

If there are two middle nodes, return **the second middle** node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.

```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

```
Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow=head;
        ListNode fast=head;

        while(fast!=null && fast.next !=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        return slow;
    }
}
```

## 7. Reverse Linked List Iterative (206)

Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
Input: head = [1,2]
Output: [2,1]

```

**Example 3:**

```
Input: head = []
Output: []
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public static ListNode head;
    public static ListNode tail;
    public ListNode reverseList(ListNode head) {
        ListNode prev=null;
        ListNode curr=tail=head;
        ListNode next;

        while(curr!=null){
            next=curr.next;
            curr.next=prev;
            prev=curr;
            curr=next;
        }
        head=prev;
        
        return prev;

    }
}
```

## 8. Reverse a Linked List -Recursive (206)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }

        ListNode newHead=reverseList(head.next);
        head.next.next=head;
        head.next=null;

        return newHead;
    }
}
```

## 9. Detect a Cycle / Loop in the LL (141)

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

Return `true` *if there is a cycle in the linked list*. Otherwise, return `false`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {

        ListNode slow=head;
        ListNode fast=head;

        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;

            if(slow==fast){
                return true;
            }

        }
        return false;
        
    }
}
```

## 10. Remove Loop from Linked List (142)
             OR
      Linked List Cycle II (142)

Given the `head` of a linked list, return *the node where the cycle begins. If there is no cycle, return* `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (**0-indexed**). It is `-1` if there is no cycle. **Note that** `pos` **is not passed as a parameter**.

**Do not modify** the linked list.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![image.png](image%201.png)

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

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public static ListNode head;
    public static ListNode tail;

    public ListNode detectCycle(ListNode head) {

        //base case

        if (head==null || head.next==null){
            return null;
        }
        //detect if cycle is present or not
        ListNode slow=head;
        ListNode fast=head;
        boolean cycle=false;
        
        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
            if(slow==fast){
                cycle=true;
                break;
            }
        }
        if(cycle==false){
            return null;
        }

        //find the meeting point in the cycel
        slow=head;
        ListNode prev=null;

        while(slow!=fast){
            prev=fast;
            slow=slow.next;
            fast=fast.next;
        }
        return slow;

        //break the loop
        
    }
}
```

## 11. Length of Loop in Linked List

Given the **head** of a linked list, determine whether the list contains a **loop**. If a loop is present, return the **number of nodes** in the loop, otherwise return **0**.

**Note:** Internally, pos(1 based index) is used to denote the position of the node that tail's next pointer is connected to. If pos = 0, it means the last node points to null, indicating there is no loop. Note that pos is not passed as a parameter.

**Examples:**

```
Input:pos = 2,

Output:4
Explanation:There exists a loop in the linked list and the length of the loop is 4
```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/904501/Web/Other/blobid0_1756186026.webp)

```java
/*
class Node {
    int data;
    Node next;

    Node(int x) {
        data = x;
        next = null;
    }
}
*/

class Solution {
    public int lengthOfLoop(Node head) {
       Node slow=head;
       Node fast=head;
  
       
       while(fast!=null && fast.next!=null){
           fast=fast.next.next;
           slow=slow.next;
           
           
           if(fast==slow){
               int count=1;
               
               Node temp=slow.next;
               
               while(temp!= slow){
                   count++;
                   temp=temp.next;
               }
               return count;
           }
       }
       return 0;
        
    }
}
```

## 12. Check if Linked List is Palindrome or Not (234)

Given the `head` of a singly linked list, return `true` *if it is a palindrome or* `false` *otherwise*.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public static ListNode head;
    public static ListNode tail;

    
    public ListNode middle(ListNode head){
        ListNode slow=head;
        ListNode fast=head;

        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        return slow;

    }
    public boolean isPalindrome(ListNode head) {

        if(head==null || head.next==null){
            return true;
        }
        //find mid
        ListNode mid=middle(head);

        //reverse 2nd hald
        ListNode prev=null;
        ListNode curr=mid;
        ListNode next;

        while(curr!=null){
            next=curr.next;
            curr.next=prev;
            prev=curr;
            curr=next;
        }
        ListNode right= prev;   //head of right part
        ListNode left=head;

        //check if 1st part is equals to 2nd part 
        while(right!=null){
            if(left.val!=right.val){
                return false;
            }
            left=left.next;
            right=right.next;
        }
        return true;
    }
}
```

## 13. Remove Nth Node from End of a List (19)

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 */

class Solution {
    public static ListNode head;
    public static ListNode tail;
    public ListNode removeNthFromEnd(ListNode head, int n) {
       
       int sz=0;
       ListNode si=head;
       while(si!=null){
        si=si.next;
        sz++;
       }
       
       if(sz==n){
        return head=head.next;
       }

       int i=0;
       ListNode temp=head;
       while(i<sz-n-1){
        temp=temp.next;
        i++;
       }
       temp.next=temp.next.next;
       return head;
       

    }
}
```

## 14. Odd Even Linked List (328)

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return *the reordered list*.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

```
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }

        ListNode odd=head;
        ListNode even=head.next;

        ListNode evenLink=even;
        
        while(even !=null && even.next!=null){

            odd.next=even.next;
            odd=odd.next;

            even.next=even.next.next;
            even=odd.next;
        }
        odd.next=evenLink;
        return head;
    }
}
```

## 15. Delete the Middle Node in the Linked List(2095)

You are given the `head` of a linked list. **Delete** the **middle node**, and return *the* `head` *of the modified linked list*.

The **middle node** of a linked list of size `n` is the `⌊n / 2⌋th` node from the **start** using **0-based indexing**, where `⌊x⌋` denotes the largest integer less than or equal to `x`.

- For `n` = `1`, `2`, `3`, `4`, and `5`, the middle nodes are `0`, `1`, `1`, `2`, and `2`, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/11/16/eg1drawio.png)

```
Input: head = [1,3,4,7,1,2,6]
Output: [1,3,4,1,2,6]
Explanation:
The above figure represents the given linked list. The indices of the nodes are written below.
Since n = 7, node 3 with value 7 is the middle node, which is marked in red.
We return the new list after removing this node.
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteMiddle(ListNode head) {
        if(head==null || head.next==null){
            return null;
        }

        ListNode slow=head;
        ListNode fast=head;
        ListNode prev=head;

        while(fast !=null && fast.next!=null){
            prev=slow;
            slow=slow.next;
            fast=fast.next.next;
        }
        prev.next=slow.next;
        return head;

    }
}
```

## 16. Sort Linked List (148)

Given the `head` of a linked list, return *the list after sorting it in **ascending order***.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

```
Input: head = [4,2,1,3]
Output: [1,2,3,4]
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode merge(ListNode head1, ListNode head2){
        ListNode mergeLL=new ListNode(-1);
        ListNode temp=mergeLL;

        while(head1!=null && head2!=null){
            if(head1.val<=head2.val){
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

    public ListNode getMid(ListNode head){
        ListNode slow=head;
        ListNode fast=head.next;

        while(fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        return slow;
    }
    public ListNode sortList(ListNode head) {

        //boundary condition

        if(head==null || head.next==null){
            return head;
        }
        //get mid
        ListNode mid=getMid(head);

        //break the list in two parts
        ListNode Righthead=mid.next;
        mid.next=null;
        ListNode newleft=sortList(head);
        ListNode newright=sortList(Righthead);

        //merge both the list
        return merge(newleft, newright);
    }
}
```

## 17. Sort a Linked List of 0’s, 1’s and 2’s

Given the **head** of a linked list where nodes can contain values **0s**, **1s,** and **2s** only. Your task is to **rearrange** the list so that all **0s** appear at the beginning, followed by all **1s**, and all **2s** are placed at the end.

**Examples:**

```
Input:head =1 → 2 → 2 → 1 → 2 → 0 → 2 → 2

Output:0 → 1 → 1 → 2 → 2 → 2 → 2 → 2
Explanation:All the 0s are segregated to the left end of the linked list, 2s to the right end of the list, and 1s in between. The final list will be:

```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908245/Web/Other/blobid0_1756113569.jpg)

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908245/Web/Other/blobid1_1756113598.jpg)

```java
/*
class Node {
    int data;
    Node next;

    Node(int d)
    {
        data = d;
        next = null;
    }
}*/

class Solution {
    public Node segregate(Node head) {
     if(head==null || head.next==null){
         return head;
     }
     int count0=0;
     int count1=0;
     int count2=0;
     Node temp=head;
     
     while(temp!=null){
         if(temp.data==0){
             count0++;
         }
         else if(temp.data==1){
             count1++;
         }
         else{
             count2++;
         }
         temp=temp.next;
     }
     
     
     temp=head;
     while(temp!=null){
         if(count0>0){
             temp.data=0;
             count0--;
         }
         else if(count1>0){
             temp.data=1;
             count1--;
         }
         else{
             temp.data=2;
             count2--;
         }
         temp=temp.next;
     }
     return head;
        
    }
}
```

## 18. Intersection of Two Linked List (160)

Given the heads of two singly linked-lists `headA` and `headB`, return *the node at which the two lists intersect*. If the two linked lists have no intersection at all, return `null`.

For example, the following two linked lists begin to intersect at node `c1`:

![image.png](image%202.png)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    if(headA== null || headB==null){
        return null;
    }

        ListNode A=headA;
        ListNode B=headB;

        while(A!=B){
           if(A==null){
            A=headB;
           }
           else{
            A=A.next;
           }

           if(B==null){
            B=headA;
           }
           else{
            B=B.next;
           }
        }
        return A;
    }
}
```

## 19. **Add 1 to a Linked List Number**

You are given a linked list where each element in the list is a node and have an integer data. You need to add **1** to the number formed by concatinating all the list node numbers together and return the head of the modified linked list.

**Note:** The head represents the first element of the given array.

**Examples :**

```
Input:LinkedList: 4->5->6
Output:457

Explanation: 4->5->6 represents 456 and when 1 is added it becomes 457.
```

![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700053/Web/Other/blobid0_1722278845.png)

```java
/*
class Node {
    int data;
    Node next;

    Node(int x) {
        data = x;
        next = null;
    }
}
*/

class Solution {
    public Node addOne(Node head) {
       
        head = reverse(head);

        Node temp = head;
        int carry = 1; 
        Node prev = null;

        while (temp != null) {
            int sum = temp.data + carry;
            temp.data = sum % 10;
            carry = sum / 10;

            prev = temp;
            temp = temp.next;
        }

        if (carry > 0) {
            prev.next = new Node(carry);
        }

        
        head = reverse(head);

        return head;
    }

    
    private Node reverse(Node head) {
        Node prev = null;
        Node curr = head;
        Node next = null;

        while (curr != null) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }

        return prev;
    }
}
```

## 20. Add 2 Numbers as a Linked List (2)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */

class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        
        ListNode dummy = new ListNode(0);
        ListNode temp = dummy;
        int carry = 0;

        while (l1 != null || l2 != null || carry != 0) {
            int sum = carry;

            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }

            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }

            carry = sum / 10;
            int digit = sum % 10;

            temp.next = new ListNode(digit);
            temp = temp.next;
        }

        return dummy.next;
    }
}
```