# 7. Reverse Integer

## Problem
Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

    Input: 123
    Output: 321
Example 2:

    Input: -123
    Output: -321
Example 3:

    Input: 120
    Output: 21
Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Process

### 22 ms

>Run Code Status: Time Limit Exceeded

```java
class Solution {
    public int reverse(int x) {
        int level = 10;
        int digitNum = 0;
        
        int tmpIn = x;
        while(tmpIn!=0){
            //int temp = tmpIn%10;
            digitNum++;
            tmpIn = tmpIn/level;
        }
        //System.out.println("digitNum="+digitNum);
        
        int result = 0;
        tmpIn = x;
        int limit = Integer.MAX_VALUE;
        while(tmpIn!=0){
            int temp = tmpIn%10;
            //System.out.println("temp="+temp);
            int tmpDigit = digitNum;
            while(tmpDigit>1){
                temp = temp*10;
                tmpDigit--;
            }
            //System.out.println("temp="+temp);
            result=result+temp;
            //System.out.println("result="+result);
            if(result>limit){
                return 0;
            }
            digitNum--;
            tmpIn = tmpIn/level;
        }
        
        if(x<0){
            result = -1*result;
        }
        
        return result;
        
        
    }
}
```

>Submission Result: Wrong Answer 
Input:
-123
Output:
321
Expected:
-321

wrong way to reverse the positive or negative.
change from ```result = -1*result;``` to ```result = 0-result;```

```int temp = tmpIn%10;``` is already negative, so should remove
```java
        if(x<0){
            result = -1*result;
        }
```

>Submission Result: Wrong Answer 
Input:
1534236469
Output:
1056389759
Expected:
0

limit=2147483647

debug
>Finished in 68 ms
digitNum=10
limit=2147483647
temp=9
temp=410065408
result=410065408
temp=6
temp=600000000
result=1010065408
temp=4
temp=40000000
result=1050065408
temp=6
temp=6000000
result=1056065408
temp=3
temp=300000
result=1056365408
temp=2
temp=20000
result=1056385408
temp=4
temp=4000
result=1056389408
temp=3
temp=300
result=1056389708
temp=5
temp=50
result=1056389758
temp=1
temp=1
result=1056389759
result=1056389759
1056389759

```java
while(tmpDigit>1){
                temp = temp*10;
                if(temp>limit){
                    return 0;
                }
                tmpDigit--;
            }
```
 still wrong
          
```
while(tmpDigit>1){
                if(temp>limit/10){
                    return 0;
                }
                temp = temp*10;
                tmpDigit--;
            }
```            
            
>Input:
-2147483648
Output:
126087180
Expected:
0

```java
class Solution {
    public int reverse(int x) {
        int level = 10;
        int digitNum = 0;
        
        int tmpIn = x;
        while(tmpIn!=0){
            //int temp = tmpIn%10;
            digitNum++;
            tmpIn = tmpIn/level;
        }
        //System.out.println("digitNum="+digitNum);
        
        int result = 0;
        tmpIn = x;
        int maxLimit = Integer.MAX_VALUE;
        int minLimit = Integer.MIN_VALUE;
        while(tmpIn!=0){
            int temp = tmpIn%10;
            //System.out.println("temp="+temp);
            int tmpDigit = digitNum;
             while(tmpDigit>1){
                if(temp>maxLimit/10||temp<minLimit/10){
                    return 0;
                }
                temp = temp*10;
                tmpDigit--;
            }
            //System.out.println("temp="+temp);
            result=result+temp;
            //System.out.println("result="+result);
            if(result>maxLimit||result<minLimit){
                return 0;
            }
            digitNum--;
            tmpIn = tmpIn/level;
        }
    
        
        return result;
        
        
    }
}
```

>Submission Result: Wrong Answer 
Input:
1563847412
Output:
-2147483645
Expected:
0

debug
>Finished in 52 ms
temp=2
temp=2000000000
result=2000000000
temp=1
temp=100000000
result=2100000000
temp=4
temp=40000000
result=2140000000
temp=7
temp=7000000
result=2147000000
temp=4
temp=400000
result=2147400000
temp=8
temp=80000
result=2147480000
temp=3
temp=3000
result=2147483000
temp=6
temp=600
result=2147483600
temp=5
temp=50
result=-2147483646
temp=1
temp=1
result=-2147483645
-2147483645

```java
class Solution {
    public int reverse(int x) {
        int level = 10;
        int digitNum = 0;
               
        boolean isPositive = x>0;
        
        int tmpIn = x;
        while(tmpIn!=0){
            //int temp = tmpIn%10;
            digitNum++;
            tmpIn = tmpIn/level;
        }
        //System.out.println("digitNum="+digitNum);
        
        int result = 0;
        tmpIn = x;
        int maxLimit = Integer.MAX_VALUE;
        int minLimit = Integer.MIN_VALUE;
        while(tmpIn!=0){
            int temp = tmpIn%10;
            //System.out.println("temp="+temp);
            int tmpDigit = digitNum;
             while(tmpDigit>1){
                if(temp>maxLimit/10||temp<minLimit/10){
                    return 0;
                }
                temp = temp*10;
                tmpDigit--;
            }
            //System.out.println("temp="+temp);
            result=result+temp;
            //System.out.println("result="+result);
            if(result>maxLimit||result<minLimit||isPositive!=(result>0)){
                return 0;
            }
        
            digitNum--;
            tmpIn = tmpIn/level;
        }
    
        
        return result;
        
        
    }
}
```

>Submission Result: Wrong Answer 
Input:
120
Output:
0
Expected:
21


```boolean isPositive = x>=0;```
```if(result>maxLimit||result<minLimit||isPositive!=(result>=0)){```

>Submission Result: Wrong Answer 
Input:
-10
Output:
0
Expected:
-1

```boolean isPositive = x>0;```
```if(result!=0&&isPositive!=(result>0)){```

```java
class Solution {
    public int reverse(int x) {
        int level = 10;
        int digitNum = 0;
               
        boolean isPositive = x>0;
        
        int tmpIn = x;
        while(tmpIn!=0){
            //int temp = tmpIn%10;
            digitNum++;
            tmpIn = tmpIn/level;
        }
        //System.out.println("digitNum="+digitNum);
        
        int result = 0;
        tmpIn = x;
        int maxLimit = Integer.MAX_VALUE;
        int minLimit = Integer.MIN_VALUE;
        while(tmpIn!=0){
            int temp = tmpIn%10;
            //System.out.println("temp="+temp);
            int tmpDigit = digitNum;
             while(tmpDigit>1){
                if(temp>maxLimit/10||temp<minLimit/10){
                    return 0;
                }
                temp = temp*10;
                tmpDigit--;
            }
            //System.out.println("temp="+temp);
            result=result+temp;
            //System.out.println("result="+result);
            if(result>maxLimit||result<minLimit){
                return 0;
            }
            if(result!=0&&isPositive!=(result>=0)){
                return 0;
            }
        
            digitNum--;
            tmpIn = tmpIn/level;
        }
        
        return result;
    }
}
```

>1032 / 1032 test cases passed.
Status: Accepted
Runtime: 22 ms
You are here! 
Your runtime beats 92.43 % of java submissions.
