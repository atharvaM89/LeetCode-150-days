# BS

### - Implement Lower Bound

The lower bound algorithm finds the first and smallest index in a sorted array where the value at that index is greater than or equal to a given key i.e. x.

```
Input: arr[] = [2, 3, 7, 10, 11, 11, 25], target = 9
Output: 3
Explanation: 3 is the smallest index in arr[] where element (arr[3] = 10) is greater than or equal to 9.
```

```java
class Solution {
    public int lowerBound(int[] nums, int x) {
       int a=0;
        for(int i=0; i<nums.length; i++){
            if(nums[i]==x){
                a=i;
                break;
            }
            else if(nums[i]>x){
                a=i;
                break;
            }
            else{
                a=nums.length;
            }
        }
        return a;
     }
}
```

```java
static int lowerBound(int[] arr, int target) {
        int n = arr.length;

        for (int i = 0; i < n; ++i) {
            if(arr[i] >= target) {
                return i;
            }
        }
        return n;
    }
```

### - Implement Upper Bound

The **upper bound** of a number is defined as the smallest **index** in the sorted array where the element is greater than the given number.

```
Input:arr[] = [2, 3, 7, 10, 11, 11, 25], target = 9
Output: 3
Explanation: 3 is the smallest index in arr[], at which element (arr[3] = 10) is larger than 9.
```

```java
class Solution {
    int upperBound(int[] arr, int target) {
        int n=arr.length;
    
    for(int i=0; i<n; i++){
        if(arr[i]>target){
            return i;
        }
    }
    return n;
        
    }
}
```

### -Floor Ceil in Sorted Array

Given a sorted array nums and an integer x. Find the **floor** and **ceil** of x in nums. The floor of x is the largest element in the array which is smaller than or equal to x. The ceiling of x is the smallest element in the array greater than or equal to x. If no floor or ceil exists, output -1.

Input : nums =[3, 4, 4, 7, 8, 10], x= 5

Output: 4 7

Explanation: The floor of 5 in the array is 4, and the ceiling of 5 in the array is 7.

```java
class Solution {
    public int[] getFloorAndCeil(int[] nums, int x) {
       int n=nums.length;
       int arr[]=new int[2];
       int a=0;

      for(int i=n-1; i>=0; i--){
        if(nums[i]<=x){
            arr[0]=nums[i];
            break;
        }
      }
      for(int i=0; i<n; i++){
        if(nums[i]>=x){
            arr[1]=nums[i];
            break;
        }
      }
      return arr;
    }
}
```

## 1. Binary Search (704)

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

```java
class Solution {
    public int search(int[] nums, int target) {
        int si=0;
        int ei=nums.length-1;
        
        while(si<=ei){
            int mid=(si+ei)/2;
            if(nums[mid]==target){
            return mid;
        }
        else if(nums[mid]>target){
            ei=mid-1;

        }
        else{
            si=mid+1;
        }
        }
        return -1;
        
    }
}
```

## 2. Search Insert Position (35)

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [1,3,5,6], target = 5
Output: 2
```

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int si=0;
        int ei=nums.length-1;
      
        while(si<=ei){
            int mid=si+(ei-si)/2;

            if(nums[mid]==target){
                return mid;
            }
            else if(nums[mid]<target){
                si=mid+1;
            }
            else{
                ei=mid-1;
            }
        }
        return si;
    }
}
```

## 3. Find First and Last Position of Element in Sorted Array (34)

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int arr[]={-1,-1};
        if(nums.length==0){
            return arr;
        }

        int si=0;
        int ei=nums.length-1;

			//For First Position
        while(si<=ei){
            int mid =si+(ei-si)/2;

            if(nums[mid]==target){
                arr[0]=mid;
                ei=mid-1;   // keep searching on Left Side
            }
            else if(nums[mid]<target){
                si=mid+1;
            }
            else{
                ei=mid-1;
            }
        }
        si=0;
        ei=nums.length-1;
        

			//For Last Position
        while(si<=ei){
            int mid =si+(ei-si)/2;

            if(nums[mid]==target){
                arr[1]=mid;
                si=mid+1;  // Keep Searching on Right side
            }
            else if(nums[mid]<target){
                si=mid+1;
            }
            else{
                ei=mid-1;
            }
        }
        return arr;
    }
}
```

## 4. Search in Rotated Sorted Array (33)

Given the array `nums` **after** the possible rotation and an integer `target`, return *the index of* `target` *if it is in* `nums`*, or* `-1` *if it is not in* `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

```java
class Solution {
    public static int Rotated(int nums[], int target, int si, int ei){
       
        if(si>ei){
            return -1;
        }
         int mid=si+(ei-si)/2;
        if(nums[mid]==target){
            return mid;
        }

        //1st Half is Sorted
        if(nums[si]<=nums[mid]){
            if(nums[si]<=target && target<nums[mid]){
                return Rotated(nums, target, si, mid-1);
            }
            else{
                return Rotated(nums, target, mid+1, ei);
            }

        }
        else{
            if(nums[mid]<target && nums[ei]>=target){
                return Rotated(nums, target, mid+1, ei);
            }
            else{
                return Rotated(nums, target, si,mid-1);
            }
        }
    }
    public int search(int[] nums, int target) {
        return Rotated(nums, target, 0, nums.length-1);

    }
}
```

## 5. **Search in Rotated Sorted Array II (81)**

Given the array `nums` **after** the rotation and an integer `target`, return `true` *if* `target` *is in* `nums`*, or* `false` *if it is not in* `nums`*.*

You must decrease the overall operation steps as much as possible.

**Example 1:**

```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

```java
class Solution {

    public static Boolean Rotated(int nums[], int target, int si, int ei){
        if(si>ei){
            return false;
        }
        int mid=si+(ei-si)/2;
        if(nums[mid]==target){
            return true;
        }

        if(nums[si]==nums[mid] && nums[ei]==nums[mid]){
            return Rotated(nums, target, si+1, ei-1);
        }

        //First Half is Sorted

        if(nums[mid]>=nums[si]){
            if(nums[si]<=target && nums[mid]>target){
                return Rotated(nums, target, si, mid-1);
            }
            else{
                return Rotated(nums, target, mid+1, ei);
            }
        }

        //Otherwise 2nd Half is Sorted
        else{
            if(nums[mid]<target && nums[ei]>=target){
                return Rotated(nums, target, mid+1, ei);
            }
            else{
                return Rotated(nums, target, si, mid-1);
            }
        }
    }
    public boolean search(int[] nums, int target) {
      return Rotated(nums, target, 0, nums.length-1);
        
    }
}
```

## 6. Find Minimum in Rotated Sorted Array (153)

**Example 1:**

```
Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.

```

Given the sorted rotated array `nums` of **unique** elements, return *the minimum element of this array*.

You must write an algorithm that runs in `O(log n) time`.

```java
class Solution {
    public int findMin(int[] nums) {
        int si=0;
        int ei=nums.length-1;

        while(si<ei){
            int mid=si+(ei-si)/2;

            if(nums[mid]<=nums[ei]){
                ei=mid;
            }
            else{
                si=mid+1;
            }
        }
        return nums[si];
    }
}
```

## 7. Single Element in Sorted Array (540)

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return *the single element that appears only once*.

Your solution must run in `O(log n)` time and `O(1)` space.

**Example 1:**

```
Input: nums = [1,1,2,3,3,4,4,8,8]
Output: 2
```

**Pattern:**

- Before the single element → pairs start at even indices
    
    (e.g., `0,1`, `2,3`, `4,5` …)
    
- After the single element → pairs start at odd indices

So,

- If `mid` is **even** and `nums[mid] == nums[mid+1]` → single is on **right**
- If `mid` is **odd** and `nums[mid] == nums[mid-1]` → single is on **right**
    
    Otherwise, it’s on **left**
    

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int si=0;
        int ei=nums.length-1;

        while(si<ei){
            int mid=si+(ei-si)/2;

            if(( mid%2==0 && nums[mid+1]==nums[mid]) || (mid%2==1 && nums[mid-1]==nums[mid])){
               si=mid+1;
            }
            else{
                ei=mid;
            }
        }
        return nums[si];
    }
}
```

## 8. Find Peak Element (162)

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You must write an algorithm that runs in `O(log n)` time.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int si=0;
        int ei=nums.length-1;
        while(si<ei){
            int mid=si+(ei-si)/2;

            if(nums[mid]>nums[mid+1]){
                ei=mid;
            }
            else{
                si=mid+1;
            }
        }
        return si;
    }
}
```