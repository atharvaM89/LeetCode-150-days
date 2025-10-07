# Sorts

## 1. Bubble Sort

```java
public class App {
    public static void bubble(int arr[]){
        for(int i=0; i<arr.length-1; i++){
            for(int j=0; j<arr.length-1-i; j++){
                if(arr[j]>arr[j+1]){
                    int temp=arr[j];
                    arr[j]=arr[j+1];
                    arr[j+1]=temp;
                }
            }
        }
    }
    public static void print(int arr[]){
        for(int i=0; i<arr.length; i++){
            System.out.print(arr[i]+" ");
        }
        System.out.println("");
    }
    
    
    public static void main(String[] args) throws Exception {
        int arr[]={5,4,1,2,3};
        bubble(arr);
        print(arr);
        
    }
}

```

## 2. Selection Sort

```java
public class App {
    public static void selection(int num[]){
        int n=num.length;

        for(int i=0; i<n-1; i++){
            int min=i;
            for(int j=i+1; j<n; j++){
                if(num[j]<num[min]){
                    min=j;
                }
            }
            int temp=num[min];
            num[min]=num[i];
            num[i]=temp;
        }
    }
    public static void print(int num[]){
        for(int i=0; i<num.length; i++){
            System.out.print(num[i]+" ");
        }
        System.out.println("");
    }
    public static void main(String[] args) throws Exception {
       int num[]={5,6,46,46,1,6446};
       selection(num);
       print(num);
    }
}

```

## 3. Insertion Sort

```java
public class App {
    public static void insertion(int num[]){
        for(int i=1; i<num.length; i++){
            int curr=num[i];
            int prev=i-1;
            while(prev>=0 && num[prev]>curr){
                num[prev+1]=num[prev];
                prev--;

            }  
            num[prev+1]=curr;

        }
    }
    public static void print(int num[]){
        for(int i=0; i<num.length; i++){
            System.out.print(num[i]+" ");
        }
        System.out.println("");
    }
    public static void main(String[] args) throws Exception {
       int num[]={1,2,65,4,89,8};
       insertion(num);
       print(num);
    }
}

```

## 4. Inbuilt Sort

```java
import java.util.*;

public class App {
    public static void n_print(int arr[]){
        for(int i=arr.length-1; i>=0; i--){
            System.out.print(arr[i]+" ");
        }
        System.out.println("");
    }
    public static void main(String[] args) throws Exception {
        int arr[]={5,1,55,186,161,6,165,16,541};

        Arrays.sort(arr);
        n_print(arr);
    }
}

```

## 5. Counting Sort

```java
import java.util.*;

public class App {
    public static void counting(int arr[]){
        int largest=Integer.MIN_VALUE;

        for(int i=0; i<arr.length; i++){
            largest=Math.max(largest, arr[i]);
        }

        int count[]=new int[largest+1];

        for(int i=0; i<arr.length; i++){
            count[arr[i]]++;
        }

        //sorting
        int j=0;
        for(int i=0; i<arr.length; i++){
            while(count[i]>0){
                arr[j]=i;
                j++;
                count[i]--;
            }
        }
    }
    public static void print(int arr[]){
        for(int i=0; i<arr.length; i++){
            System.out.print(arr[i]+" ");
        }
        System.out.println("");
    }
    public static void main(String[] args) throws Exception {
        int arr[]={1,5,8,9,6,3,7};
        counting(arr);
        print(arr);
    }
}

```

## 6. Merge Sort

```java
public class App {
    public static void print(int arr3[]){
        for(int i=0; i<arr3.length; i++){
            System.out.print(arr3[i]+" ");
        }
    }

    public static int[] meregSort(int arr[], int si, int ei){
        if(si>=ei){
            int A[]={arr[si]};
            return A;
        }
        
        int mid=si+(ei-si)/2;
        int arr1[]= meregSort(arr, si, mid);
        int arr2[]= meregSort(arr, mid+1, ei);
        int arr3[]= merge(arr1, arr2);
        return arr3;

    }

    public static int[] merge(int arr1[],int arr2[]){

       int m=arr1.length;
       int n=arr2.length;
        int arr3[]=new int[m+n];
        // left(0,3)=4 n
        // rigfht(4,6)=3 elementy

        //(6-0)+1==7

        int i=0;  // iteration for left part
        int j=0;  //. iteration for right part
        int k=0;     // iteration for temp array

        while(i<m && j<n){

        if(arr1[i]<arr2[j]){
            arr3[k]=arr1[i];
            i++;
            k++;
        }
        else{
            arr3[k]=arr2[j];
            j++;
            k++;
        }
    }

    // for left part
    while(i<m){
        arr3[k]=arr1[i];
        i++;
        k++;
    }
//for right part
while(j<n){
    arr3[k++]=arr2[j++];
}
return arr3;

    }
    
    
    public static void main(String[] args) throws Exception {
       int arr[]={6,3,9,5,2,8};
       int arr3[]= meregSort(arr, 0, arr.length-1);
       print(arr3);

    }
}

```

## 7. Quick Sort

```java
public class App {
    public static void print(int arr[]){
        for(int i=0; i<arr.length; i++){
            System.out.print(arr[i]+" ");
           
        }
    }

    public static void quicksort(int arr[], int si, int ei){

        if(si>=ei){
            return;
        }
        int pidx=partition(arr, si,ei);  // gives the position of the piviot
        quicksort(arr, si, pidx-1);  //left part
        quicksort(arr, pidx+1, ei);  // right part

    }

    public static int partition(int arr[], int si, int ei){

        int piviot=arr[ei];
        int i=si-1;

        for(int j=si; j<ei; j++){
            if(arr[j]<=piviot){
                i++;
                int temp=arr[j];
                arr[j]=arr[i];
                arr[i]=temp;
            }
        }
        i++;
        int temp=piviot;
        arr[ei]=arr[i];
        arr[i]=temp;
        return i;
    }
    public static void main(String[] args) throws Exception {
      int arr[]={6,3,9,8,2,5};
      quicksort(arr, 0, arr.length-1);
      print(arr);
    }
}

```

## 8. Merge Sort to sort array of Strings

```java
public class App {
public static void print(String arr[]){
    for(int i=0; i<arr.length; i++){
        System.err.print(arr[i]+" ");
    }
}

public static String[] mergeSort(String arr[], int si, int ei){

    if(si>=ei){
        String A[]={arr[si]};
        return A;
    }

    int mid= si+(ei-si)/2;

    String arr1[]=mergeSort(arr, si, mid);
    String arr2[]=mergeSort(arr,mid+1, ei);

    String arr3[]= merge(arr1, arr2);
    return arr3;
}

public static String[] merge(String arr1[], String arr2[]){

    int m=arr1.length;
    int n=arr2.length;

    String arr3[]=new String[m+n];

    int i=0;  //iteration for left part
    int j=0;  //iteration for rightpart
    int k=0;  //iteration for temp array

    while(i<m && j<n){
       int cmp= arr1[i].compareTo(arr2[j]);
        if(cmp<0){
            arr3[k]=arr1[i];
            k++;
            i++;
        }
        else{// cmp>0
            arr3[k]=arr2[j];
            k++;
            j++;
        }
    }
    while(i<m){
        arr3[k]=arr1[i];
        i++;
        k++;
    }
    while(j<n){
        arr3[k]=arr1[j];
        j++;
        k++;
    }
    return arr3;

}

    public static void main(String[] args) throws Exception {
        String arr[]={"sun", "earth", " mars", "mercury"};

        mergeSort(arr, 0, arr.length-1);
        print(arr);
    }
}

```