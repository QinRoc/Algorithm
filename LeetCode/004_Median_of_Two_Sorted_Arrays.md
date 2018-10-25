# Median of Two Sorted Arrays   

## Problem
There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

Example 1:

    nums1 = [1, 3]
    nums2 = [2]

    The median is 2.0
Example 2:

    nums1 = [1, 2]
    nums2 = [3, 4]

    The median is (2 + 3)/2 = 2.5

## Process
### 1

wrong way to create array:```int[] combineNums = new int[combineLength]{};```
```int[] combineNums = new int[combineLength];```

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int length1 = nums1.length;
        int length2 = nums2.length;
        int combineLength = length1+length2;

        int[] combineNums = new int[combineLength];
        int index1 = 0;
        int index2 = 0;
        int combineIndex = 0;
        
        while(combineIndex<combineLength){
            if(nums1[index1]<nums2[index2]){
                combineNums[combineIndex] = nums1[index1];
                index1++;
                combineIndex++;
            }else {
                combineNums[combineIndex] = nums2[index2];
                index2++;
                combineIndex++;
            }
        }
        
        if(combineLength%2==0){
            //even
            return (combineNums[combineLength/2-1]+combineNums[combineLength/2])/2.0;
        }else{
            //odd
            return (double)combineNums[combineLength/2];
        }
    }
}
```


>Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 1
	at Solution.findMedianSortedArrays(Solution.java:13)

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int length1 = nums1.length;
        int length2 = nums2.length;
        int combineLength = length1+length2;

        int[] combineNums = new int[combineLength];
        int index1 = 0;
        int index2 = 0;
        int combineIndex = 0;
        
        while(combineIndex<combineLength){
            if(index1<length1 && index2<length2){
               if(nums1[index1]<nums2[index2]){
                    combineNums[combineIndex] = nums1[index1];
                    index1++;
                    combineIndex++;
               }else {
                    combineNums[combineIndex] = nums2[index2];
                    index2++;
                    combineIndex++;
               }
            } else if(index1<length1 && index2>=length2){
                combineNums[combineIndex] = nums1[index1];
                index1++;
                combineIndex++;
            } else if(index1>=length1 && index2<length2){
                combineNums[combineIndex] = nums2[index2];
                index2++;
                combineIndex++;
            }
        }
        
        if(combineLength%2==0){
            //even
            return (combineNums[combineLength/2-1]+combineNums[combineLength/2])/2.0;
        }else{
            //odd
            return (double)combineNums[combineLength/2];
        }
    }
}
```

>2084 / 2084 test cases passed.
Status: Accepted
Runtime: 38 ms
You are here! 
Your runtime beats 59.00 % of java submissions.


```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int length1 = nums1.length;
        int length2 = nums2.length;
        int combineLength = length1+length2;

        int[] combineNums = new int[combineLength];
        int index1 = 0;
        int index2 = 0;
        int combineIndex = 0;
        
        while(combineIndex<combineLength){
            if(index1<length1 && index2<length2){
               if(nums1[index1]<nums2[index2]){
                    combineNums[combineIndex] = nums1[index1];
                    index1++;
                    combineIndex++;
               }else {
                    combineNums[combineIndex] = nums2[index2];
                    index2++;
                    combineIndex++;
               }
            } else if(index2>=length2){
                combineNums[combineIndex] = nums1[index1];
                index1++;
                combineIndex++;
            } else if(index1>=length1){
                combineNums[combineIndex] = nums2[index2];
                index2++;
                combineIndex++;
            }
        }
        
        if(combineLength%2==0){
            //even
            return (combineNums[combineLength/2-1]+combineNums[combineLength/2])/2.0;
        }else{
            //odd
            return (double)combineNums[combineLength/2];
        }
    }
}
```

>2084 / 2084 test cases passed.
Status: Accepted
Runtime: 56 ms
You are here! 
Your runtime beats 22.56 % of java submissions.

---

break when arrive median Index;

```java
        int medianIndex;
        if(combineLength%2==0){
            //even
            medianIndex = combineLength/2-1;
        }else{
            //odd
            medianIndex = combineLength/2;
        }
```

no need to judge two situation,


```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int length1 = nums1.length;
        int length2 = nums2.length;
        int combineLength = length1+length2;

        int[] combineNums = new int[combineLength];
        int index1 = 0;
        int index2 = 0;
        int combineIndex = 0;
        
        int medianIndex = combineLength/2;
        
        while(combineIndex<combineLength){
            if(index1<length1 && index2<length2){
               if(nums1[index1]<nums2[index2]){
                    combineNums[combineIndex] = nums1[index1];
                    index1++;                
               }else {
                    combineNums[combineIndex] = nums2[index2];
                    index2++;
               }
            } else if(index2>=length2){
                combineNums[combineIndex] = nums1[index1];
                index1++;
            } else if(index1>=length1){
                combineNums[combineIndex] = nums2[index2];
                index2++;
               
            }
            
            if(combineIndex==medianIndex){
                break;
            }
            combineIndex++;
        }
        
        if(combineLength%2==0){
            //even
            return (combineNums[combineLength/2-1]+combineNums[combineLength/2])/2.0;
        }else{
            //odd
            return (double)combineNums[combineLength/2];
        }
    }
}
```

>2084 / 2084 test cases passed.
Status: Accepted
Runtime: 36 ms
You are here! 
Your runtime beats 65.10 % of java submissions.

---

###　Use List method

```combineList.add(nums1);```
        
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        List<Integer> combineList = new ArrayList<Integer>();
        for(int tmp:nums1){
            combineList.add(tmp);
        }
        for(int tmp:nums2){
            combineList.add(tmp);
        }
        Collections.sort(combineList);
        
        int length = combineList.size();
        if(length%2==0){
            //even
            return (combineList.get(length/2)+combineList.get(length/2+1))/2;
        }else{
            //odd
            return (double)combineList.get(length/2+1);
        }
    }
}
```

>Run Code Result:
Your input
[1,3]
[2]
Your answer
3.0
Expected answer
2

index start from 0


```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        List<Integer> combineList = new ArrayList<Integer>();
        for(int tmp:nums1){
            combineList.add(tmp);
        }
        for(int tmp:nums2){
            combineList.add(tmp);
        }
        Collections.sort(combineList);
        
        int length = combineList.size();
        if(length%2==0){
            //even
            return (combineList.get(length/2-1)+combineList.get(length/2))/2;
        }else{
            //odd
            return (double)combineList.get(length/2);
        }
    }
}
```

>Input:
[1,2]
[3,4]
Output:
2.0
Expected:
2.5

```return (combineList.get(length/2-1)+combineList.get(length/2))/2.0;```

>2084 / 2084 test cases passed.
Status: Accepted
Runtime: 72 ms
You are here! 
Your runtime beats 12.54 % of java submissions.
