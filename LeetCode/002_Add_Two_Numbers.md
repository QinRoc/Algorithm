# Add Two Numbers

## Review
1. Not hurry, keep clam to solve the problem.
2. Debug with handwriting is low efficient.
[ ] TODO: Read the articles of Discuss Section and keep optimizing the efficiency.

---

## Problem

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## Process



```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
```



ListNode没有用过，Google



https://courses.cs.washington.edu/courses/cse143/18sp/lectures/ListNode.java

> ListNode is a class for storing a single node of a linked list storing integer values.  It has two public data fields for the data and the link to the next node in the list and has three constructors:
>
> public ListNode()//     creates node with data 0, null link
>
> public ListNode(int data)//     creates node with given data, null link
>
> public ListNode(int data, ListNode next)//     creates node with given data and given link



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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1.next!=null||l2.next!=null){
            sum = l1.val*level+l2.val*level+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
            
            if(level==1){
                resultNode.val = sum;
                resultNode.next = tmpNode;
            }else{
                tmpNode.val = sum;
                tmpNode.next = new ListNode(highNum);
                tmpNode = tmpNode.next;
            }
            
            level = 10*level;
            
            if(l1.next!=null){
                l1 = l1.next;
            }else{
                l1.val =0;
            }
            
            if(l2.next!=null){
                l2 = l2.next;
            }else{
                l2.val =0;
            }
            
        }
        
        return resultNode;
    }
}
```

while条件变更
```while(l1!=null||l2!=null){```language
```

>内存溢出


- - -



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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
            }
            
            sum = part1*level+part2*level+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
            
            if(level==1){
                resultNode.val = sum;
                resultNode.next = tmpNode;
            }else{
                tmpNode.val = sum;
                tmpNode.next = new ListNode(highNum);
                tmpNode = tmpNode.next;
            }
            
            level = 10*level;
            
            l1 = l1.next;
            
            l2 = l2.next;
            
        }
        
        return resultNode;
    }
}
```language
```

>Your input
[2,4,3]
[5,6,4]
Your answer
[7,0,1,1]
Expected answer
[7,0,8]

忘记结果要求了，不需要level了

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
            }
            
            sum = part1+part2+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
            
            if(level==1){
                resultNode.val = sum;
                resultNode.next = tmpNode;
            }else{
                tmpNode.val = sum;
                tmpNode.next = new ListNode(highNum);
                tmpNode = tmpNode.next;
            }
            
            level = 10*level;
            
            l1 = l1.next;
            
            l2 = l2.next;
            
        }
        
        return resultNode;
    }
}
```

>Your input
[2,4,3]
[5,6,4]
Your answer
[7,0,8,0]
Expected answer
[7,0,8]

增加
 ```      resultNode.next = null;```

>Your input
[2,4,3]
[5,6,4]
Your answer
[7]
Expected answer
[7,0,8]

改为```tmpNode = null;```

>Your input
[2,4,3]
[5,6,4]
Your answer
[7,0,8,0]
Expected answer
[7,0,8]

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
            }
            
            sum = part1+part2+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
                 
            level = 10*level;
            
            l1 = l1.next;
            
            l2 = l2.next;
            
            if(level==1){
                resultNode.val = sum;
                resultNode.next = tmpNode;
            }else{
                tmpNode.val = sum;
                if(l1!=null&&l2!=null){
                    tmpNode.next = new ListNode(highNum);
                    tmpNode = tmpNode.next;
                }
            }
       
            
        }
                
        return resultNode;
    }
}
```language
```

>Your input
[2,4,3]
[5,6,4]
Your answer
[0]
Expected answer
[7,0,8]


```if(l1!=null||l2!=null){```

>Your input
[2,4,3]
[5,6,4]
Your answer
[0]
Expected answer
[7,0,8]

```level = 10*level;位置放的不对```
            
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
            }
            
            sum = part1+part2+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
                 
            
            l1 = l1.next;
            
            l2 = l2.next;
            
            if(level==1){
                resultNode.val = sum;
                resultNode.next = tmpNode;
            }else{
                tmpNode.val = sum;
                if(l1!=null||l2!=null){
                    tmpNode.next = new ListNode(highNum);
                    tmpNode = tmpNode.next;
                }
            }
            
                        level = 10*level;

       
            
        }
                
        return resultNode;
    }
}
```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NullPointerException
	at Solution.addTwoNumbers(Solution.java:45)
	at __DriverSolution__.__helper__(__Driver__.java:8)
	at __Driver__.main(__Driver__.java:54)
Last executed input:
[1,8]
[0]


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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
                            l1 = l1.next;

            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
                            l2 = l2.next;

            }
            
            sum = part1+part2+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
                 
            
            
            
            if(level==1){
                resultNode.val = sum;
                resultNode.next = tmpNode;
            }else{
                tmpNode.val = sum;
                if(l1!=null||l2!=null){
                    tmpNode.next = new ListNode(highNum);
                    tmpNode = tmpNode.next;
                }
            }
            
                        level = 10*level;

       
            
        }
                
        return resultNode;
    }
}
```

>Submission Result: Wrong Answer 
Input:
[0]
[0]
Output:
[0,0]
Expected:
[0]


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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
                            l1 = l1.next;

            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
                            l2 = l2.next;

            }
            
            sum = part1+part2+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
                 
            
            
            
            if(level==1){
                resultNode.val = sum;
                                if(l1!=null||l2!=null){
                                                    resultNode.next = tmpNode;

                                }

            }else{
                tmpNode.val = sum;
                if(l1!=null||l2!=null){
                    tmpNode.next = new ListNode(highNum);
                    tmpNode = tmpNode.next;
                }
            }
            
                        level = 10*level;

       
            
        }
                
        return resultNode;
    }
}
```

>Submission Result: Wrong Answer 
Input:
[5]
[5]
Output:
[0]
Expected:
[0,1]


``` if(l1!=null||l2!=null||highNum!=0){```

>Submission Result: Wrong Answer 
Input:
[5]
[5]
Output:
[0,0]
Expected:
[0,1]


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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
                l1 = l1.next;
            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
                l2 = l2.next;
            }
            
            sum = part1+part2+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
            if(level==1){
                resultNode.val = sum;
                if(l1!=null||l2!=null||highNum!=0){
                    tmpNode = new ListNode(highNum);
                    resultNode.next = tmpNode;
                }

            }else{
                tmpNode.val = sum;
                if(l1!=null||l2!=null){
                    tmpNode.next = new ListNode(highNum);
                    tmpNode = tmpNode.next;
                }
            }
            
            level = 10*level;
        }
                
        return resultNode;
    }
}
```

>Submission Result: Wrong Answer 
Input:
[1]
[9,9]
Output:
[0,0]
Expected:
[0,0,1]

```if(l1!=null||l2!=null||highNum!=0){```

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //result
        ListNode resultNode = new ListNode(0);
        //each unit sum
        int sum = 0;
        //liangji
        int level = 1;
        //jinwei
        int highNum = 0;
        
        ListNode tmpNode = new ListNode(highNum);
        
        while(l1!=null||l2!=null){
            int part1 = 0;
            if(l1!=null){
                part1 = l1.val;
                l1 = l1.next;
            }
            
             int part2 = 0;
            if(l2!=null){
                part2 = l2.val;
                l2 = l2.next;
            }
            
            sum = part1+part2+highNum;
            if(sum>9){
                highNum = 1;
                sum = sum%10;
            }else{
                highNum = 0;
            }
            
            if(level==1){
                resultNode.val = sum;
                if(l1!=null||l2!=null||highNum!=0){
                    tmpNode = new ListNode(highNum);
                    resultNode.next = tmpNode;
                }

            }else{
                tmpNode.val = sum;
                if(l1!=null||l2!=null||highNum!=0){
                    tmpNode.next = new ListNode(highNum);
                    tmpNode = tmpNode.next;
                }
            }
            
            level = 10*level;
        }
                
        return resultNode;
    }
}
```

>Submission Detail
1563 / 1563 test cases passed.
Status: Accepted
Runtime: 45 ms
You are here! 
Your runtime beats 22.26 % of java submissions.

