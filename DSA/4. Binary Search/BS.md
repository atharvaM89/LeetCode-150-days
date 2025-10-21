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

# Pattern 1- BS on 1D Arrays

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

# Pattern 2 - BS (Min) or (Max)

## 9. Sqrt {x}  (69)

Bruteforce

```cpp
class Solution {
public:
    int mySqrt(int x) {
         int result=0;
        for(int i=1; i<=x; i++){
            int res=i*i;
           
            if(res==x){
                result=i;
                break;
            }
            else if(res>x){
                result=i-1;
                break;
            }
        }
        return result;
    }
};
```

Optimal Solun

```cpp
class Solution {
public:
    int mySqrt(int x) {
        if(x==0 || x==1){
            return x;
        }
        int si=1;
        int ei=x;
        int res=0;
        

        while(si<=ei){
            long mid=si+(ei-si)/2;
            long sq=mid*mid;
            

            if(sq==x){
                return mid;
            }
            else if(sq<x){
               res=mid;
                si=mid+1;
            }
            else{
                ei=mid-1;
            }
        }
        return res;
    }
};
```

## 10. Find nth root of m

You are given 2 numbers **n and m,** the task is to find **n√m** (nth root of m). If the root is not integer then returns **-1**.

**Examples :**

```
Input:n = 3, m = 27
Output:3
Explanation:33 = 27
```

```java
**class Solution {
    public int nthRoot(int n, int m) {
        int si=1;
        int ei=m;
        int res=0;
        
        while(si<=ei){
            int mid=si+(ei-si)/2;
            int ans=1;
            for(int i=0; i<n; i++''){
                ans=ans*mid;
            }
            
            if(ans==m){
                return mid;
            }
            else if(ans<m){
                si=mid+1;
            }
            else{
                ei=mid-1;
            }
        }
        return -1;
        
    }
}**
```

## 11. Koko Eating Bananas (875)

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return *the minimum integer* `k` *such that she can eat all the bananas within* `h` *hours*.

**Example 1:**

```
Input: piles = [3,6,7,11], h = 8
Output: 4
```

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
       int max=0;

       for(int pile: piles){
        max=Math.max(max, pile);
       }

       for(int k=1; k<=max; k++){
        long hour=0;
        for(int pile:piles){
            hour+=(pile+(long)k-1)/k;
        }
        if(hour<=h){
            return k;
        }
       }
       return max;
    }
}
```

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
       int max=0;

       for(int pile: piles){
        max=Math.max(max, pile);
       }
        
    int si=1;
    int ei=max;
    int ans=max;
    while(si<=ei){
        int mid=si+(ei-si)/2;
        long hour=time(piles, mid);

        if(hour<=h){
           ans=mid;
           ei=mid-1;
        }
        else {
            si=mid+1;
        }
       }
       return ans;
    }
    public long time(int piles[], int mid){
        long hour =0;
        for(int pile: piles){
            hour+=(pile+(long)mid-1)/mid;
        }
        return hour;
    }
}
```

## 12. Minimum No of days to make m Bouquets (1482)

You want to make `m` bouquets. To make a bouquet, you need to use `k` **adjacent flowers** from the garden.

The garden consists of `n` flowers, the `ith` flower will bloom in the `bloomDay[i]` and then can be used in **exactly one** bouquet.

Return *the minimum number of days you need to wait to be able to make* `m` *bouquets from the garden*. If it is impossible to make m bouquets return `-1`.

**Example 1:**

```
Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
Output: 3
Explanation: Let us see what happened in the first three days. x means flower bloomed and _ means flower did not bloom in the garden.
We need 3 bouquets each should contain 1 flower.
After day 1: [x, _, _, _, _]   // we can only make one bouquet.
After day 2: [x, _, _, _, x]   // we can only make two bouquets.
After day 3: [x, _, x, _, x]   // we can make 3 bouquets. The answer is 3.
```

```java
class Solution {
    public int minDays(int[] bloomDay, int m, int k) {
        int n=bloomDay.length;
        if((long)m*k>n){
            return -1;
        }
        int min=Integer.MAX_VALUE;
        int max=Integer.MIN_VALUE;

        for(int day:bloomDay){
            min=Math.min(min, day);
            max=Math.max(max, day);
        }

        int ans=-1;
        int si=min;
        int ei=max;

        while(si<=ei){
            int mid=si+(ei-si)/2;

            if(canMake(bloomDay, mid, m, k)){
                ans=mid;
                ei=mid-1;
            }
            else{
                si=mid+1;
            }
        }
        return ans;
    }

    public boolean canMake(int bloomDay[], int day, int m, int k){
        int flower=0, bouq=0;

        for(int d: bloomDay){
            if(d<=day){
                flower++;
                if(flower==k){
                    bouq++;
                    flower=0;
                }
            }
            else{
                    flower=0;
                }
        }
        return bouq>=m;
    }
}
```

## 13. Find a Smallest Divisor given in Threshold (1283)

Each result of the division is rounded to the nearest integer greater than or equal to that element. (For example: `7/3 = 3` and `10/2 = 5`).

The test cases are generated so that there will be an answer.

**Example 1:**

```
Input: nums = [1,2,5,9], threshold = 6
Output: 5
Explanation: We can get a sum to 17 (1+2+5+9) if the divisor is 1.
If the divisor is 4 we can get a sum of 7 (1+1+2+3) and if the divisor is 5 the sum will be 5 (1+1+1+2).
```

```java
class Solution {
    public int smallestDivisor(int[] nums, int threshold) {
        int max=0;

        for(int no:nums){
            max=Math.max(max, no);
        }
           
           
        for(int i=1; i<=max; i++){
             int sum=0;
          for(int nu:nums){
            sum+=(nu+i-1)/i;
          }
          if(sum<=threshold){
            return i;
          }
        }
        return max;
    }
}
```

Method 2- Optimal

```java
class Solution {
    public int smallestDivisor(int[] nums, int threshold) {
        int max=Integer.MIN_VALUE;

        for(int no:nums){
            max=Math.max(max, no);
           
        }
        int si=1;
        int ans=max;
        int ei=max;

        while(si<=ei){
            int mid=si+(ei-si)/2;
            int div=divisor(nums, mid);

            if(div<=threshold){
                ans=mid;
                ei=mid-1;
            }
            else{
                si=mid+1;
            }
        }
        return ans;
    }
     public int divisor(int nums[], int mid){
            int sum=0;
            for(int nu:nums){
                sum+=(nu+mid-1)/mid;
            }
            
        return sum;
        }
}
```

## 14. Capacity to Ship Packages Within D Days (1011)

The `ith` package on the conveyor belt has a weight of `weights[i]`. Each day, we load the ship with packages on the conveyor belt (in the order given by `weights`). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `days` days.

**Example 1:**

```
Input: weights = [1,2,3,4,5,6,7,8,9,10], days = 5
Output: 15
Explanation: A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.
```

```java
class Solution {
    public int shipWithinDays(int[] weights, int days) {
        int max=Integer.MIN_VALUE;
        int sum=0;

        for(int load:weights){
            sum+=load;
            max=Math.max(max, load);
        }
       
        int si=max;
        int ei=sum;
        int ans=sum;
        while(si<=ei){
            int mid=si+(ei-si)/2;
             if(Possible(weights, mid, days)){
                ans=mid;
                ei=mid-1;
             }
             else{
                si=mid+1;
             }
        }
        return ans;
    }

    public boolean Possible(int weights[], int mid, int days){
        int dayCount=1;
        int currentLoad=0;

        for(int w:weights){
            if(currentLoad+w>mid){
                dayCount++;
                currentLoad=0;
            }
            currentLoad+=w;
        }
        return dayCount<=days;
    }
}
```

## 15. Kth Missing Positive Number (1539)

Given an array `arr` of positive integers sorted in a **strictly increasing order**, and an integer `k`.

Return *the* `kth` ***positive** integer that is **missing** from this array.*

**Example 1:**

```
Input: arr = [2,3,4,7,11], k = 5
Output: 9
Explanation:The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.
```

```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int index=0;
        int missingCount=0;
        int num=1;

        while(true){
            if(index<arr.length && arr[index]==num){
                index++;
            }
            else{
                missingCount++;
                if(missingCount==k){
                    return num;
                }
            }
            num++;
        }
    }
}
```

# Pattern 3- BS on MIN of MAX || MAX of MIN

## 16. Aggressive Cows

You are given an array with unique elements of **stalls[]**, ****which denote the positions of **stalls**. You are also given an integer **k** which denotes the number of aggressive cows. The task is to assign **stalls** to **k** cows such that the **minimum distance** between any two of them is the **maximum** possible.

**Examples:**

```
Input:stalls[] = [1, 2, 4, 8, 9], k = 3
Output:3
Explanation:The first cow can be placed at stalls[0],
the second cow can be placed at stalls[2] and
the third cow can be placed at stalls[3].
The minimum distance between cows in this case is 3, which is the largest among all possible ways.
```

Method 1 - Brute Force

```java
class Solution {
    public int aggressiveCows(int[] stalls, int k) {
        Arrays.sort(stalls);
        int n=stalls.length;
        int min=1;
        int max=stalls[n-1]-stalls[0];
        int ans=0;
        
        
        for(int i=min; i<=max; i++){
            if(canWePlace(stalls, k, i)){
               ans=i;
            }
            else{
                break;
            }
           
        }
         return ans;
    }
    
    public boolean canWePlace(int stalls[], int cows, int dist){
        int count=1;
        int last=stalls[0];
        
        for(int i=1; i<stalls.length; i++){
            if(stalls[i]-last>=dist){
                count++;
                last=stalls[i];
            }
            if(count==cows){
                return true;
            }
        }
    
        return false;
    }
    
}
```

Method 2- Optimized

```java
class Solution {
    public int aggressiveCows(int[] stalls, int k) {
        Arrays.sort(stalls);
        int n=stalls.length;
        
        int si=1;
        int high=stalls[n-1]-stalls[0];
        int ans=0;
        
        while(si<=high){
            int mid=si+(high-si)/2;
            
            if(canPossible(stalls, k, mid)){
                ans=mid;
                si=mid+1;
            }
            else{
                high=mid-1;
            }
        }
        return ans;
    }
    public boolean canPossible(int stalls[], int cows, int dist){
        int count=1;
        int lastPos=stalls[0];
        
        for(int i=1; i<stalls.length; i++){
            if(stalls[i] - lastPos>=dist){
                count++;
                lastPos=stalls[i];
            }
            if(count==cows){
                return true;
            }
        }
        return false;
    }
}
```

## 17. Allocate Minimum Pages

The objective is to **minimize the maximum number of pages** assigned to any student. In other words, out of all possible allocations, find the arrangement where the student who receives the most pages still has the **smallest possible maximum**.

**Note:** If it is not possible to allocate books to all students, return **-1**.

**Examples:**

```
Input:arr[] = [12, 34, 67, 90], k = 2
Output:113
Explanation:Allocation can be done in following ways:
=> [12] and [34, 67, 90] Maximum Pages = 191
=> [12, 34] and [67, 90] Maximum Pages = 157
=> [12, 34, 67] and [90] Maximum Pages = 113.
The third combination has the minimum pages assigned to a student which is 113.
```

```java
class Solution {
    public int findPages(int[] arr, int k) {
       
        int n=arr.length;
        
        if(k>n){
            return -1;
        }
        
        int low=0, high=0;
        
        for(int pages:arr){
            low=Math.max(low, pages);
            high+=pages;
        }
        int ans=-1;
        
        while(low<=high){
            int mid=low+(high-low)/2;
            
            if(possible(arr, n, k, mid)){
                ans=mid;
                high=mid-1;
            }
            else{
                low=mid+1;
            }
        }
        return ans;
    }
    
    public boolean possible(int arr[], int n, int k, int MaxPages){
        
        int studentCount=1;
        int sum=0;
        
        for(int pages:arr){
            if(sum+pages>MaxPages){
                studentCount++;
                sum=pages;
                
                if(studentCount>k){
                    return false;
                }
            }
            else{
                sum+=pages;
            }
        }
        return true;
    }
}
```

## 18. Split Array Largest Sum (410)

Given an integer array `nums` and an integer `k`, split `nums` into `k` non-empty subarrays such that the largest sum of any subarray is **minimized**.

Return *the minimized largest sum of the split*.

A **subarray** is a contiguous part of the array.

**Example 1:**

```
Input: nums = [7,2,5,10,8], k = 2
Output: 18
Explanation: There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8], where the largest sum among the two subarrays is only 18.
```

```java
class Solution {
    public int splitArray(int[] nums, int k) {
        int low=0, high=0;

        for(int num: nums){
            low=Math.max(low, num);
            high +=num;
        }

        int ans=high;

        while(low<=high){
            int mid=low+(high-low)/2;

            if(possible(nums, k, mid)){
                ans=mid;
                high=mid-1;
            }
            else{
                low=mid+1;
            }
        }
        return ans;
    }
    public boolean possible(int nums[], int k, int mid){
        int count=1;
        int sum=0;

        for(int num:nums){
            if(sum+num>mid){
                count++;
                sum=num;

                if(count>k){
                    return false;
                }
            }
             else{
                    sum+=num;
                }
        }
         return true;
    }
}
```

## 19. Painter’s Partition Problem

Given an array **arr[]** where each element denotes the length of a board, and an integer **k** representing the number of **painters** available. Each painter takes **1** unit of time to paint **1 unit length** of a board.

Determine the **minimum** amount of time required to paint all the boards, under the constraint that each painter can paint only a **contiguous** sequence of boards (no skipping or splitting allowed).

**Examples:**

```
Input:arr[] = [5, 10, 30, 20, 15], k = 3
Output: 35
Explanation:The optimal allocation of boards among 3 painters is -
Painter 1 → [5, 10] → time = 15
Painter 2 → [30] → time = 30
Painter 3 → [20, 15] → time = 35
Job will be done when all painters finish i.e. at time = max(15, 30, 35) = 35
```

```java
class Solution {
    public int minTime(int[] arr, int k) {
        int n=arr.length;
        
        int low=0, high=0;
        
        for(int val:arr){
            high+=val;
            low=Math.max(low, val);
        }
        
        int ans=high;
        
        while(low<=high){
            
            int mid=low+(high-low)/2;
            
            if(possible(arr, n, k, mid)){
                ans=mid;
                high=mid-1;
            }
            else{
                low=mid+1;
            }
        }
        return ans;
    }
    
    public boolean possible(int arr[], int n , int k, int mid){
        int painter=1;
        int time=0;
        
        for(int val:arr){
            if(time+val<=mid){
                time+=val;
            }else{
                painter++;
                time=val;
                if(painter>k){
                    return false;
                }
            }
        }
        return true;
    }
}

```

## 20. Minimize Max Distance to Gas Station (774)

We have a **horizontal** number line. On that number line, we have gas **stations** at positions stations[0], stations[1], ..., stations[n-1]. Now, we add **k** more gas stations so that **d**, the maximum distance between adjacent gas stations, is minimized. We have to find the smallest possible value of d. Find the answer **exactly** to 2 decimal places.**Note**: **`stations`** is in a **strictly increasing** order.

**Examples:**

```
Input:stations[] = [1, 2, 3, 4, 5], k = 2
Output: 1.00
Explanation:Since all gaps are already equal (1 unit each), adding extra stations in between does not reduce the maximum distance.
```

```java
class Solution {
    public double minMaxDist(int[] stations, int K) {
        int n=stations.length;
        double low=0, high=0;
        
        for(int i=1; i<n; i++){
            high=Math.max(high, stations[i]-stations[i-1]);
        }
        
        double esp= 1e-6;
        
        while(high-low>esp){
            double mid=low+(high-low)/2.0;
            
            if(possible(stations, K, mid)){
                high=mid;
            }
            else{
                low=mid;
            }
        }
        return high;
    }
    
    public boolean possible(int stations[], int k, double mid){
        int stat=0;
        
        for(int i=1; i<stations.length; i++){
            double gap=stations[i]-stations[i-1];
            stat+=(int)gap/mid;
        }
        return stat<=k;
    }
}

```

## 21. Median of 2 Sorted Array (4)

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n=nums1.length;
        int m=nums2.length;

        int merged[]=new int[n+m];
        int k=0;
        for(int i=0; i<n; i++){
            merged[k++]=nums1[i];
        }
        for(int i=0; i<m; i++){
            merged[k++]=nums2[i];
        }

        Arrays.sort(merged);
        int total=merged.length;

        if(total%2==1){
            return (double) merged[total/2];
        }
        else{
            int middle1=merged[total/2-1];
            int middle2=merged[total/2];
            return ((double) middle1+ (double) middle2)/2.0;
        }
    }
}
```

## 22. Kth Element of 2 Sorted Array

Given two sorted arrays **a[]** and **b[]** and an element **k**, the task is to find the element that would be at the **kth** position of the combined sorted array.

**Examples :**

```
Input:a[] = [2, 3, 6, 7, 9], b[] = [1, 4, 8, 10], k = 5
Output:6
Explanation:The final combined sorted array would be [1, 2, 3, 4, 6, 7, 8, 9, 10]. The 5th element of this array is 6.
```

```java
class Solution {
    public int kthElement(int a[], int b[], int k) {
      ArrayList<Integer> arr=new ArrayList<>();
      
      for(int i:a){
          arr.add(i);
      }
      for(int i:b){
      arr.add(i);
      }
      
      Collections.sort(arr);
      
      return arr.get(k-1);
    }
}
```

# Pattern 4- BS on 2-D Arrays

## 23. Row  with Maximum Once (2643)

Given a `m x n` binary matrix `mat`, find the **0-indexed** position of the row that contains the **maximum** count of **ones,** and the number of ones in that row.

In case there are multiple rows that have the maximum count of ones, the row with the **smallest row number** should be selected.

Return *an array containing the index of the row, and the number of ones in it.*

**Example 1:**

```
Input: mat = [[0,1],[1,0]]
Output: [0,1]
Explanation: Both rows have the same number of 1's. So we return the index of the smaller row, 0, and the maximum count of ones (1). So, the answer is [0,1].
```

```java
class Solution {
    public int[] rowAndMaximumOnes(int[][] mat) {
        int ans[]=new int[2];
        int max=0;
        for(int i=0; i<mat.length; i++){
            int count=0;
            for(int j=0; j<mat[i].length; j++){
                if(mat[i][j]==1){
                    count++;
                }
        }
            if(count>max){
                max=count;
                ans[0]=i;
                ans[1]=count;
            }
        }
        return ans;
    }
}
```

## 24. Search in 2D Matrix (74)

You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` *if* `target` *is in* `matrix` *or* `false` *otherwise*.

You must write a solution in `O(log(m * n))` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {

        for (int i = 0; i < matrix.length; i++) {

            if (target <= matrix[i][matrix[0].length - 1]) {

                int l = 0;
                int r = matrix[i].length - 1;

                while (l <= r) {
                    int m = (l + r) / 2;

                    if (matrix[i][m] == target) {
                        return true;
                    }

                    else if (matrix[i][m] < target){
                         l = m + 1;
                    }
                    else{
                         r = m - 1;
                    }
                }
            }
        }
        return false;
    }
}
```

## 25. Search a 2D Matrix II (240)

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true
```

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int r = matrix.length;        
        int c= matrix[0].length;    
        int row = 0;                  
        int col = c - 1;        

        while (row < r && col >= 0) {

            int current = matrix[row][col];
            if (current == target){ 
                return true;
                }

            else if (target < current){
                col--;
            }    
            else {
                row++;
            }                        
        }
        return false; 
    }
}
```

## 26. Find Peak Element II (1901)

Medium

Topics

![premium lock icon](https://leetcode.com/_next/static/images/lock-a6627e2c7fa0ce8bc117c109fb4e567d.svg)

Companies

Hint

A **peak** element in a 2D grid is an element that is **strictly greater** than all of its **adjacent** neighbors to the left, right, top, and bottom.

Given a **0-indexed** `m x n` matrix `mat` where **no two adjacent cells are equal**, find **any** peak element `mat[i][j]` and return *the length 2 array* `[i,j]`.

You may assume that the entire matrix is surrounded by an **outer perimeter** with the value `-1` in each cell.

You must write an algorithm that runs in `O(m log(n))` or `O(n log(m))` time.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/06/08/1.png)

```
Input: mat = [[1,4],[3,2]]
Output: [0,1]
Explanation: Both 3 and 4 are peak elements so [1,0] and [0,1] are both acceptable answers.
```

```java
class Solution {
    public int[] findPeakGrid(int[][] mat) {
        int r = mat.length;
        int c = mat[0].length;
        int left = 0, right = c - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            int maxRow = 0;
            for (int i = 1; i < r; i++) {
                if (mat[i][mid] > mat[maxRow][mid]) {
                    maxRow = i;
                }
            }

            int current = mat[maxRow][mid];
            int leftVal = (mid - 1 >= 0) ? mat[maxRow][mid - 1] : -1;
            int rightVal = (mid + 1 < c) ? mat[maxRow][mid + 1] : -1;

            if (current > leftVal && current > rightVal) {
                return new int[]{maxRow, mid};
            } else if (leftVal > current) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return new int[]{-1, -1};
    }
}
```

## 27. Median in a row wise Sorted Matrix

Given a **row-wise sorted** matrix **mat[][]** of size n*m, where the number of rows and columns is always **odd**. Return the **median** of the matrix.

**Examples:**

```
Input: mat[][] = [[1, 3, 5],
                [2, 6, 9],
                [3, 6, 9]]
Output: 5
Explanation:
```

```java
class Solution {
    public int median(int[][] mat) {
      ArrayList<Integer> list=new ArrayList<>();
      
      for(int i=0; i<mat.length; i++){
          for(int j=0; j<mat[0].length; j++){
              list.add(mat[i][j]);
          }
      }
      Collections.sort(list);
      
      int mid=list.size()/2;
      return list.get(mid);
        
    }
}
```

## 28. **Search in a Row-Column sorted matrix**

Given a 2D integer matrix **mat**[][] of size **n x m**, where every row and column is sorted in increasing order and a number **x**, ****the task is to find whether element **x** is present in the matrix.

**Examples:**

```
Input: mat[][] = [[3, 30, 38],[20, 52, 54],[35, 60, 69]], x = 62
Output: false
Explanation: 62 is not present in the matrix, so output is false.
```

```java
class Solution {
    public static boolean matSearch(int mat[][], int x) {
        int n=mat.length;
        
        for(int i=0; i<n; i++){
            if(bs(mat[i], x)){
                return true;
            }
        }
        return false;
    }
    public static boolean bs(int mat[], int target){
        int low=0, high=mat.length-1;
        
        while(low<=high){
            int mid=(low+high)/2;
            
            if(mat[mid]==target){
                return true;
            }
            else if(target>mat[mid]){
                low=mid+1;
            }
            else{
                high=mid-1;
            }
        }
        return false;
    }
}
```