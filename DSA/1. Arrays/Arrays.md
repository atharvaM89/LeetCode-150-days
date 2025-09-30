# Arrays

### Largest Element in Array O(n)

```java
class Solution {
    public int largestElement(int[] nums) {
        int max=0;
    for(int i=0; i<nums.length; i++){
        if(nums[i]>max){
            max=nums[i];
        }
    }
    return max;
    }
}
```

### Second Largest Element in Array  (N log n +N)

- Sorting: O(n log n)
- Loop: O(n)
- Total = **O(n log n + n) = O(n log n)** ✅

```java
class Solution {
    public int secondLargestElement(int[] nums) {
    Arrays.sort(nums);
    int last=nums[nums.length-1];
    int secondlargest=0;
    boolean set=false;
    for(int i=nums.length-2; i>=0; i--){
        if(nums[i]<last){
            secondlargest=nums[i];
            set=true;
            break;
        }
    }
    if(set){
        return secondlargest;
    }
    else{
        return-1;
    }
    }
}
```

### Linear Search O(n)

```java
class Solution {
    public int linearSearch(int nums[], int target) {
		for(int i=0; i< nums.length; i++){
        if(nums[i]==target){
          return i;
        }
    }
    return -1;
    }
}
```

### Binary SearchO(log n)

```java
public class App {
    public static int binary_search(int number[], int key){

        int s=0;
        int e=number.length-1;

               while(s<=e){
           int mid=(s+e)/2;
           if(number[mid]==key){
            return mid;
           }
           else if(number[mid]>key){
            
            e=mid-1;

           }
           else{
            s=mid+1;
            
           }
        }
        return -1;
    }
    
    public static void main(String[] args) throws Exception {
        int number[]={5,10,15,20,25,30,35,50};
        int key=50;
        int index=binary_search(number, key);
        if(index==-1){
            System.out.println("Element not found");
        }
        else{
            System.out.println(index);
        }
    }
}

```

### Reverse an Array O(n)

```java
public class App {
    public static void reverse(int number[]){
        int first=0;
        int last=number.length-1;

        while(first<last){
            int temp=number[last];
            number[last]=number[first];
            number[first]=temp;

            first++;
            last--;
        }
    }
    public static void main(String[] args) throws Exception {
        int number[]={2,3,5,8};
        reverse(number);
        for(int i=0; i<number.length;i++){
            System.out.print(number[i]);
        }
    }
}

```

### Pairs in Array O(n2)

```java
public class App {
    public static void pair(int number[]){
        int tp=0;

        for(int i=0; i<number.length;i++){
            int current=number[i];
            for(int j=i+1; j<number.length; j++){
                System.out.print("("+current+","+number[j]+")");
                tp++;
            }
            System.out.println("");
        }
        System.out.println("Total no of pairs= "+tp);
    }
    public static void main(String[] args) throws Exception {
        int number[]={1,3,4,56,78};

        pair(number);

    }
}

```

## 1. Check if Array is Sorted and rotated (1752)   O(n)

**Example 1:**

```
Input: nums = [3,4,5,1,2]
Output: true
Explanation: [1,2,3,4,5] is the original sorted array.
You can rotate the array by x = 2 positions to begin on the element of value 3: [3,4,5,1,2].
```

```java
class Solution {
    public boolean check(int[] nums) {
        int count =0;
        int n=nums.length;

        if(nums[0]<nums[n-1])count++;

        for(int i=0; i<n-1; i++){
            if(nums[i]>nums[i+1]){
                count++;
            }
        }
        if(count>1){
            return false;
        }
        return true;
    }
}
```

## 2. Remove Duplicates From Array (26)   O(n)

**Example 1:**

```
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
```

```
class Solution {
    public int removeDuplicates(int[] nums) {
        int n=nums.length;
        int count=1;
        for(int i=1; i<n; i++){
          if(nums[i]!=nums[i-1]){
            nums[count]=nums[i];
            count++;
          }
        }
        return count;
    }
}
```

## 3. Rotate Array (189)

**O(n)** (three reversals, each linear in array size).

```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n=nums.length;
        k=k%n;

        reverse(nums, 0,n-1);
        reverse(nums, 0, k-1);
        reverse(nums, k, n-1);

    }
    public static void reverse(int nums[], int si, int ei){
        while(si<ei){
            int temp=nums[si];
            nums[si]=nums[ei];
            nums[ei]=temp;
            si++;
            ei--;
        }
    }
}
```

## 4. Move zero to ends (283)   O(n)

**Example 1:**

```
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int len=nums.length;
        int nz=0;
        
        for(int i=0; i<len; i++){
            if(nums[i]!=0){
                nums[nz]=nums[i];
                nz++;
            }
            
        }
        for(int i=nz; i<len; i++){
            nums[i]=0;
        }
    }
}
```

## 5. Union of Two Sorted Array   O((n+m)^2)

**O((n + m)²)** (checking `list.contains()` inside loops makes it quadratic, plus O((n+m) log(n+m)) for sorting).

**Examples:**

**Input**: nums1 = [1, 2, 3, 4, 5], nums2 = [1, 2, 7]

**Output**: [1, 2, 3, 4, 5, 7]

**Explanation**:

The elements 1, 2 are common to both, 3, 4, 5 are from nums1 and 7 is from nums2

```java
class Solution {
    public ArrayList<Integer> unionArray(int[] a, int[] b) {
        
        ArrayList<Integer> list=new ArrayList<>();
        
        for(int i=0; i<a.length; i++){
            if(!list.contains(a[i])){
                list.add(a[i]);
            }
        }
        for(int i=0; i<b.length; i++){
            if(!list.contains(b[i])){
                list.add(b[i]);
            }
        }
        Collections.sort(list);
        return list;
        
    }
}
```

## 6. Find Missing Number in a Range (268)  O(n2)  due to list.contain

**Example 1:**

**Input:** nums = [3,0,1]

**Output:** 2

**Explanation:**

`n = 3` since there are 3 numbers, so all numbers are in the range `[0,3]`. 2 is the missing number in the range since it does not appear in `nums`.

```java
class Solution {
    public int missingNumber(int[] nums) {
        int small=0;
        int largest=0;

        for(int i=0; i<nums.length; i++){
            if(nums[i]>largest){
                largest=nums[i];
            }
            if(nums[i]<small){
                small=nums[i];
            }
        }
        ArrayList<Integer> list=new ArrayList<>();
    
        for(int i=0; i<nums.length; i++){
            list.add(nums[i]);

        }

        
        for(int i=small; i<=largest; i++){
            if(!list.contains(i)){
                return i;
            }

        }
        return largest+1;
    }
}
```

## 7. [**Maximum Consecutive Ones](https://takeuforward.org/data-structure/count-maximum-consecutive-ones-in-the-array/) (485)   O(n)**

**Example 1:**

```
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.
```

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max=0;
        int curr=0;
        for(int i=0; i<nums.length; i++){
            if(nums[i]==1){
                curr++;
                max=Math.max(curr, max);
            }
            else{

                curr=0;
            }
        }
        return max;
    }
}
```

## 8. Number that Appear Onces (136)   O(nlogn)

**Example 1:**

**Input:** nums = [2,2,1]

**Output:** 1

```java
class Solution {
    public int singleNumber(int[] nums) {

        int n=nums.length;
        Arrays.sort(nums);

        if(n==1){
            return nums[0];
            }
        if(nums[0]!=nums[1]){
                return nums[0];
            }

        for(int i=1; i<nums.length-1; i++){
            if( nums[i]!=nums[i-1] && nums[i]!=nums[i+1]){
                return nums[i];
            }
            
        }
        return nums[n-1];
        
    }
}
```

## 9. Longest Subarray with sum K    O(n2)

**Input**: nums = [10, 5, 2, 7, 1, 9],  k=15

**Output**: 4

**Explanation**:

The longest sub-array with a sum equal to 15 is [5, 2, 7, 1], which has a length of 4. This sub-array starts at index 1 and ends at index 4, and the sum of its elements (5 + 2 + 7 + 1) equals 15. Therefore, the length of this sub-array is 4.

```java
class Solution {
    public int longestSubarray(int[] arr, int k) {
    
        int max=0;
        int n=arr.length;
        for(int i=0; i<n; i++){
            int sum=0;
            for(int j=i; j<n; j++){
               sum+=arr[j];
               
               if(sum==k){
                   int len=j-i+1;
                   max=Math.max(len, max);
               }
               
            }
        }
        return max;
    }
}

```

## 10. Two Sum (1)  O(n2)

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        
        int len= nums.length;
       for(int i=0; i<len; i++){
        for(int j=i+1; j<len; j++){
            if(nums[i] + nums[j]==target){
                return new int[] {i,j};
            }
        }
       } 
       return new int [] {};
    }
}
```

Method 2 - Optimal Solun

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];

            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            map.put(nums[i], i);
        
        return new int[]{}; // no solution case
    }
}
```

## 11. Sort Array of 0’s, 1’s and 2’s     (75)
    OR    Merge Sort 
    OR   Sort Colors     O(n log n)

**Example 1:**

```
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

```java
class Solution {
    public static int[] mergesrt(int nums[], int si, int ei){
        if(si>=ei){
            int A[]={nums[si]};
            return A;
        }
        int mid=si+(ei-si)/2;

        int arr1[]=mergesrt(nums,si,mid);
        int arr2[]=mergesrt(nums,mid+1, ei);

        int arr3[]=merge(arr1, arr2);
        return arr3;
    }
    public static int[] merge(int arr1[], int arr2[]){
        int m=arr1.length;
        int n=arr2.length;

        int arr3[]=new int[m+n];

        int i=0, j=0, k=0;

        while(i<m && j<n){
            if(arr1[i]<arr2[j]){
                arr3[k++]=arr1[i++];
            }
            else{
                arr3[k++]=arr2[j++];
            }
        }
        while(i<m){
            arr3[k++]=arr1[i++];
        }
        while(j<n){
            arr3[k++]=arr2[j++];
        }
         return arr3;
    }
    public void sortColors(int[] nums) {
         int sorted[]= mergesrt(nums, 0, nums.length-1);
          for(int i=0; i<nums.length;i++){
              nums[i] = sorted[i];
          }
    }
}

```

## 12. Majority Elements (>N/2 Times)  (169)   O(n log n)

**Example 1:**

```
Input: nums = [3,2,3]
Output: 3
```

method 1

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        int n=nums.length;
        return nums[n/2];
    }
}
```

method 2 - Using Hash Map

```java
class Solution {
    public int majorityElement(int[] nums) {
        int n = nums.length;
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < n; i++) {
            map.put(nums[i], map.getOrDefault(nums[i], 0) + 1);
        }

        n = n / 2;
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() > n) {
                return entry.getKey();
            }
        }

        return 0;
    }
}
```

## 13. Maximum Sub-Array Sum (53)

Brute Force

```java
    public static void maxArray(int number[]){
            int max=Integer.MIN_VALUE;
            int sum=0;
            int tc=0;

            for(int i=0; i<number.length; i++){
                for(int j=i; j<number.length; j++){
                    sum=0;
                    for(int k=i; k<=j; k++){
                        
                        sum+=number[k];
                    }
                    
                    System.out.println(sum);
                    if(max<sum){
                        max=sum;
                    }
                    tc++;
                 }
            }
```

Kadane’s Algo

```java
class Solution {
    public int maxSubArray(int[] nums) {
          int max = nums[0];
        int sum = 0;
        for(int i=0;i<nums.length;i++)
        {
          if(sum<0)
              sum = 0; 
          sum += nums[i];
          max = Math.max(sum,max);  
        }
        return max;
    }
}
```

## 14. Best Time to Buy and Sell Stocks (121)

```java
    class Solution {
        public int maxProfit(int[] prices) {
            int buyprice=Integer.MAX_VALUE;
            int maxprofit=0;

            for(int i=0; i<prices.length; i++){
                if(buyprice<prices[i]){
                    int profit=prices[i]-buyprice;
                    maxprofit=Math.max(profit, maxprofit);
                }
                else{
                    buyprice=prices[i];
                }
            }
            return maxprofit;
            
        }
    }
```

## 15. Rearrange Array Element in alternate position of positive and negative items (2149)

```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n=nums.length;
        int arr[]=new int[n];
        int p=0, q=1;
         
        for(int i=0; i<n; i++){
            if(nums[i]>=0){
                arr[p]=nums[i];
                p=p+2;
            }
            else{
                arr[q]=nums[i];
                q=q+2;
            }
        }
        return arr;
    }
}
```

## 16. Leaders in Array

```
Input:arr = [16, 17, 4, 3, 5, 2]
Output:[17, 5, 2]
Explanation:Note that there is nothing greater on the right side of 17, 5 and, 2
```

Method 1- Brute Force

```java
class Solution {
		static ArrayList<Integer> leaders(int arr[]) {

			ArrayList<Integer> list=new ArrayList<>();
			int n=arr.length;
    for(int i=0; i<n; i++){
        int j;
        for(j=i+1; j<n; j++){
            if(arr[i]<arr[j]){
                break;
            }
        }
        if(j==n){
            list.add(arr[i]);
        }
    }
    return list;
}
}
```

Method 2 - Optimal

```java
class Solution {
		static ArrayList<Integer> leaders(int arr[]) {
    
    ArrayList<Integer> list=new ArrayList<>();
    int n=arr.length;
    int max=arr[n-1];
    list.add(max);

    for(int i=n-2; i>=0; i-- ){
        if(arr[i]>=max){
            max=arr[i];
            list.add(max);
        }
    }
    Collections.reverse(list);
    return list;
}
}
```

## 17. Longest Consecutive Sequence (128)

```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is[1, 2, 3, 4]. Therefore its length is 4..
Example 3:

Input: nums = [1,0,1,2]
Output: 3
 
```

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        int count=1;
        int n=nums.length;
        Arrays.sort(nums);
        int max=1;

        if(n==0){
            return 0;
        }

        for(int i=1; i<n; i++){
            
            if(nums[i]==nums[i-1]+1){
                count++;
            }else if(nums[i]==nums[i-1]){
                continue;
            }
            else if(nums[i]!=nums[i-1]+1){
                count=1;
            }
            
          max=Math.max(count, max);
        }
        return max;
    }
}
```

## 18. Sub- Array sum equals k (560)

**Example 1:**

```
Input: nums = [1,1,1], k = 2
Output: 2

```

**Example 2:**

```
Input: nums = [1,2,3], k = 3
Output: 2
```

Method 1- Brute Force

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
      int n=nums.length;
      
      int max=0;

      for(int i=0; i<n; i++){
         int sum=0;
       
        for(int j=i; j<n;j++){
            sum+=nums[j];
          if(sum==k){
            max++;
            break;
          }
           
        }
      } 
      return max; 
    }
}
```

Method 2- Optimal (using Hashing)

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> subNum = new HashMap<>();
        subNum.put(0, 1);
        int total = 0, count = 0;

        for (int n : nums) {
            total += n;

            if (subNum.containsKey(total - k)) {
                count += subNum.get(total - k);
            }

            subNum.put(total, subNum.getOrDefault(total, 0) + 1);
        }

        return count;
    }
}
```

## 19. Largest Sub-Array With Sum 0

**Input:** arr = [15, -2, 2, -8, 1, 7, 10, 23]

**Output:** 5

**Explanation:**

The subarray [-2, 2, -8, 1, 7] sums up to 0 and has the maximum length among all such subarrays.

```java
class Solution {
    public int maxLen(int[] arr) {
        int n=arr.length;
        int maxlength=0;

        for(int i=0; i<n; i++){
          int currsum=0;
          for(int j=i; j<n; j++){
            currsum+=arr[j];

            if(currsum==0){
              maxlength=Math.max(maxlength, j-i+1);
            }
          }
        }
        return maxlength;
    }
}

```

## 20. Maximum Product Sub-Array (152)

find a subarray that has the largest product, and return *the product*.

```
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

Method 1- Brute Force

```java
class Solution {
    public int maxProduct(int[] nums) {
        int n=nums.length;
        int result=nums[0];

        for(int i=0; i<n; i++){
           int product=1;
            for(int j=i; j<n; j++){
                product*=nums[j];
                result=Math.max(result, product);

            }
        }
        return result;
        
    }
}
```

Method 2- Optimal Code

```java
class Solution {
    public int maxProduct(int[] nums) {
        int maxProd = nums[0];
        for(int i=0; i<nums.length; i++){
            maxProd = Math.max(maxProd,nums[i]);
        }
        int currMax = 1, currMin = 1;
        for(int i=0; i<nums.length; i++){
            if(nums[i]==0){
                currMax = 1;
                currMin = 1;
                continue;
            }
            int temp = currMax*nums[i];
            currMax = Math.max(Math.max(temp,currMin*nums[i]),nums[i]);
            currMin = Math.min(Math.min(temp,currMin*nums[i]),nums[i]);
            maxProd = Math.max(maxProd,currMax);
        }
        return maxProd;
    }
```

## 21. Majority Elements II (229)

**Example 1:**

```
Input: nums = [3,2,3]
Output: [3]
```

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        ArrayList<Integer> list=new ArrayList<>();

        int n=nums.length;
        Arrays.sort(nums);

        int count=1;

        for(int i=1; i<n; i++){
            if(nums[i]==nums[i-1]){
                count++;
            }
            else{
                 if(count>(n/3)){
                list.add(nums[i-1]);
            }
                count=1;
            }
        }

        if(count>(n/3)){
            list.add(nums[n-1]);
        }
        return list;
    }
}
```

## 22. **Count subarrays with given xor K**

Given an array of integers nums and an integer k, return the total number of subarrays whose **XOR** equals to k.

**Examples:**

Input : nums = [4, 2, 2, 6, 4], k = 6

Output : 4

Explanation : The subarrays having XOR of their elements as 6 are [4, 2],  [4, 2, 2, 6, 4], [2, 2, 6], and [6]

Method 1 - Brute Force

```java
int count=0;

      for(int i=0; i<nums.length; i++){
        int XOR=0;
        for(int j=i; j<nums.length; j++){
            XOR=XOR^ nums[j];

            if(XOR==k){
                count++;
            }
        }
      }
      return count;
```

Method 2- Optimal 

```java
class Solution {
    public int subarraysWithXorK(int[] nums, int k) {
      Map<Integer, Integer> freq=new HashMap<>();
        int count=0, XOR=0;
        
        for(int num: nums){
            XOR^=num;
            
            if(XOR==k){
                count++;
            }
            
            int req=XOR^k;
            
            if(freq.containsKey(req)){
                count+=freq.get(req);
            }
            freq.put(freq.get(XOR, 0) + 1);
        }
        return count;
    }
}
```

## 23. Merge Overlapping Sub Intervals (56)

**Example 1:**

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        int m=intervals.length;
        int n=intervals[0].length;

        if(m==0){
            return new int[0][0];
        }

        Arrays.sort(intervals, (a,b) ->a[0] - b[0]);

        List<int []> ans=new ArrayList<>();
      
        int current[]=intervals[0];

        for(int i=1; i<m; i++){
          
            if(current[1]>=intervals[i][0]){
             current[1]=Math.max(current[1], intervals[i][1]);
            }
            else{
                  ans.add(current);
                current = intervals[i];
            }
        }
        ans.add(current);
        return ans.toArray(new int[ans.size()][]);
        
    }
}
```

## 24. Merge Sorted Arrays (88)

**Example 1:**

```
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
```

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i=m-1;
        int j=n-1;
        int k=m+n-1;

        while(i>=0 && j>=0){
            if(nums1[i]>nums2[j]){
                nums1[k--]=nums1[i--];
            }
            else{
                nums1[k--]=nums2[j--];
            }
        }
        while(j>=0){
            nums1[k--]=nums2[j--];
        }
    }
}
```

## 25. Find Missing and Repeated Values (2965)

You are given a **0-indexed** 2D integer matrix `grid` of size `n * n` with values in the range `[1, n2]`. Each integer appears **exactly once** except `a` which appears **twice** and `b` which is **missing**. The task is to find the repeating and missing numbers `a` and `b`.

Return *a **0-indexed** integer array* `ans` *of size* `2` *where* `ans[0]` *equals to* `a` *and* `ans[1]` *equals to* `b`*.*

**Example 1:**

```
Input: grid = [[1,3],[2,2]]
Output: [2,4]
Explanation: Number 2 is repeated and number 4 is missing so the answer is [2,4].
```

```java
class Solution {
    public int[] findMissingAndRepeatedValues(int[][] grid) {
        int m=grid.length;
        int n=m;
        int pt=0;
        int arr[]=new int[m*n];

        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                arr[pt]=grid[i][j];
                pt++;
            }
        }
       Arrays.sort(arr);
       int len=arr.length;
       int res[]=new int[2];

        for(int i=0; i<len-1; i++){
            if(arr[i]==arr[i+1]){
                res[0]=arr[i];
                break;
            }
        }

       
         if(arr[0]!=1){
                res[1]=1;
            }
        else{
                for(int j=0; j<len-1; j++){
                    if (arr[j + 1] != arr[j] && arr[j + 1] != arr[j] + 1){
                        res[1]=arr[j]+1;
                        break;
                    }
                }
        }
         if(res[1]==0){
                res[1]=len;
            }
        return res;
    }
}
```