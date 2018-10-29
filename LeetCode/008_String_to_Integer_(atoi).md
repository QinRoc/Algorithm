
# 8. String to Integer (atoi)

https://leetcode.com/problems/string-to-integer-atoi/description/

## Problem
Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

Note:

- Only the space character ' ' is considered as whitespace character.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

Example 1:

    Input: "42"
    Output: 42

Example 2:

    Input: "   -42"
    Output: -42
    Explanation: The first non-whitespace character is '-', which is the minus sign.
                 Then take as many numerical digits as possible, which gets 42.

Example 3:

    Input: "4193 with words"
    Output: 4193
    Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.

Example 4:

    Input: "words and 987"
    Output: 0
    Explanation: The first non-whitespace character is 'w', which is not a numerical 
                 digit or a +/- sign. Therefore no valid conversion could be performed.

Example 5:

    Input: "-91283472332"
    Output: -2147483648
    Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
                 Thefore INT_MIN (−231) is returned.

## Process

### 32 ms 

```String result = '';```

>Line 32: error: empty character literal

```String result = "";```
        
        
```result + = tmp;```

>Line 39: error: illegal start of expression

```result = result + tmp;```

```java
class Solution {
    public int myAtoi(String str) {
        //The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. 
        str = str.trim();
        //If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
        int length = str.length();
        if(str==null||length==0){
                //If no valid conversion could be performed, a zero value is returned.

            return 0;
        }
        //Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
        int index=0;
        char firstChar = str.charAt(index);
        boolean isPositive = true;
        switch(firstChar){
            case '+':
                index++;
                break;
            case '-':
                index++;
                isPositive = false;
                break;
            default:
                if(firstChar<'0'||firstChar>'9'){
                        //If no valid conversion could be performed, a zero value is returned.

                    return 0;
                }
        }
        
        String result = "";
        while(index< length){
            char tmp = str.charAt(index);
            if(firstChar<'0'||firstChar>'9'){
                //The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
                break;
            }
            result = result + tmp;
            
            index++;
        }
        
        Integer intResult = Integer.parseInt(result);
        if(intResult<0){
            //the numerical value is out of the range of representable values
            if(isPositive){
                return Integer.MAX_VALUE;
            } else{
                return Integer.MIN_VALUE;
            }
        }
        
         if(isPositive){
                return intResult;
            } else{
                return 0-intResult;
        }
        
    //If no valid conversion could be performed, a zero value is returned.

        //Only the space character ' ' is considered as whitespace character.
    //Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
        

    }
}
```


>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: ""
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:548)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:44)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"   -42"

```java
           char tmp = str.charAt(index);
            if(tmp<'0'||tmp>'9'){
```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: "91283472332"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:539)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:44)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"-91283472332"

```int maxLength = Integer.MAX_VALUE.toString.length();```

>Line 32: error: int cannot be dereferenced

```java
        int maxLength = String.valueOf(Integer.MAX_VALUE).length();

            if(index>maxLength){
                break;
            }
```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: "9128347233"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:539)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:51)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"-91283472332"

```java
            if(result.length()>maxLength){
                break;
            }
```
            
>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: "91283472332"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:539)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:51)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"-91283472332"

not allow to parse out of range String

```java
        Integer intResult = Integer.parseInt(result);
        if(intResult<0){
            //the numerical value is out of the range of representable values
            if(isPositive){
                return Integer.MAX_VALUE;
            } else{
                return Integer.MIN_VALUE;
            }
        }
```        
not helpful
        
```java
class Solution {
    public int myAtoi(String str) {
        //The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. 
        str = str.trim();
        //If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
        int length = str.length();
        if(str==null||length==0){
                //If no valid conversion could be performed, a zero value is returned.

            return 0;
        }
        //Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
        int index=0;
        char firstChar = str.charAt(index);
        boolean isPositive = true;
        switch(firstChar){
            case '+':
                index++;
                break;
            case '-':
                index++;
                isPositive = false;
                break;
            default:
                if(firstChar<'0'||firstChar>'9'){
                        //If no valid conversion could be performed, a zero value is returned.

                    return 0;
                }
        }
        
        String maxString = String.valueOf(Integer.MAX_VALUE);
        int maxLength = maxString.length();
        
        String result = "";
        while(index< length){
            char tmp = str.charAt(index);
            if(tmp<'0'||tmp>'9'){
                //The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
                break;
            }
            
            if(result.length()>=maxLength){
                //the numerical value is out of the range of representable values
                for(int i = 0;i<maxLength;i++){

                    if(result.charAt(i)>maxString.charAt(i)){
                        //out of range
                        if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }
                }
                
                break;
            }
            
            result = result + tmp;
            
            index++;
        }
        
        Integer intResult = Integer.parseInt(result);
        
         if(isPositive){
                return intResult;
            } else{
                return 0-intResult;
        }
        
    //If no valid conversion could be performed, a zero value is returned.

        //Only the space character ' ' is considered as whitespace character.
    //Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
        

    }
}
```

        
>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: ""
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:548)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:65)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"+"

```java      
        if(result.length()==0){
            return 0;
        }
```      
        
        
>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: "2147483648"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:543)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:69)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"-2147483648"


```java

class Solution {
    public int myAtoi(String str) {
        //The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. 
        str = str.trim();
        //If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
        int length = str.length();
        if(str==null||length==0){
                //If no valid conversion could be performed, a zero value is returned.

            return 0;
        }
        //Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
        int index=0;
        char firstChar = str.charAt(index);
        boolean isPositive = true;
        switch(firstChar){
            case '+':
                index++;
                break;
            case '-':
                index++;
                isPositive = false;
                break;
            default:
                if(firstChar<'0'||firstChar>'9'){
                        //If no valid conversion could be performed, a zero value is returned.

                    return 0;
                }
        }
        
        String maxString = String.valueOf(Integer.MAX_VALUE);
        int maxLength = maxString.length();
        
        String result = "";
        while(index< length){
            char tmp = str.charAt(index);
            if(tmp<'0'||tmp>'9'){
                //The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
                break;
            }
            
            
            
            result = result + tmp;
            
            index++;
        }
        
        int resultLength = result.length();
        if(resultLength>=maxLength){
                //the numerical value is out of the range of representable values
                for(int i = 0;i<maxLength;i++){

                    if(result.charAt(i)>maxString.charAt(i)){
                        //out of range
                        if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }
                }
                
            }
        
        if(resultLength==0){
            return 0;
        }
        
        Integer intResult = Integer.parseInt(result);
        
         if(isPositive){
                return intResult;
            } else{
                return 0-intResult;
        }
        
    //If no valid conversion could be performed, a zero value is returned.

        //Only the space character ' ' is considered as whitespace character.
    //Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
        

    }
}
```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: "20000000000000000000"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:539)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:71)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"20000000000000000000"

```java
class Solution {
    public int myAtoi(String str) {
        //The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. 
        str = str.trim();
        //If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
        int length = str.length();
        if(str==null||length==0){
                //If no valid conversion could be performed, a zero value is returned.

            return 0;
        }
        //Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
        int index=0;
        char firstChar = str.charAt(index);
        boolean isPositive = true;
        switch(firstChar){
            case '+':
                index++;
                break;
            case '-':
                index++;
                isPositive = false;
                break;
            default:
                if(firstChar<'0'||firstChar>'9'){
                        //If no valid conversion could be performed, a zero value is returned.

                    return 0;
                }
        }
        
        String maxString = String.valueOf(Integer.MAX_VALUE);
        int maxLength = maxString.length();
        
        String result = "";
        while(index< length){
            char tmp = str.charAt(index);
            if(tmp<'0'||tmp>'9'){
                //The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
                break;
            }
            
            
            
            result = result + tmp;
            
            index++;
        }
        
        int resultLength = result.length();
        if(resultLength==maxLength){
                //the numerical value is out of the range of representable values
                for(int i = 0;i<maxLength;i++){

                    if(result.charAt(i)>maxString.charAt(i)){
                        //out of range
                        if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }
                }
                
            }else if(resultLength>maxLength){
            if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }
        
        
        if(resultLength==0){
            return 0;
        }
        
        Integer intResult = Integer.parseInt(result);
        
         if(isPositive){
                return intResult;
            } else{
                return 0-intResult;
        }
        
    //If no valid conversion could be performed, a zero value is returned.

        //Only the space character ' ' is considered as whitespace character.
    //Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
        

    }
}
```

>Submission Result: Wrong Answer 
Input:
"  0000000000012345678"
Output:
2147483647
Expected:
12345678


```java     
            if(result.length()!=0||tmp!='0'){
                            result = result + tmp;

            }
```
 
>Submission Result: Wrong Answer 
Input:
"1095502006p8"
Output:
2147483647
Expected:
1095502006

debug
>Finished in 80 ms
maxValue=2147483647
result=1 result.length()=1 maxLength=10
result=10 result.length()=2 maxLength=10
result=109 result.length()=3 maxLength=10
result=1095 result.length()=4 maxLength=10
result=10955 result.length()=5 maxLength=10
result=109550 result.length()=6 maxLength=10
result=1095502 result.length()=7 maxLength=10
result=10955020 result.length()=8 maxLength=10
result=109550200 result.length()=9 maxLength=10
result=1095502006 result.length()=10 maxLength=10
result=1095502006 result.length()=10 maxLength=10
result.charAt(i)=1 maxString.charAt(i)=2
result.charAt(i)=0 maxString.charAt(i)=1
result.charAt(i)=9 maxString.charAt(i)=4
2147483647

比较大小的写错了

debug
>Finished in 100 ms
maxValue=2147483647
result=1 result.length()=1 maxLength=10
result=10 result.length()=2 maxLength=10
result=109 result.length()=3 maxLength=10
result=1095 result.length()=4 maxLength=10
result=10955 result.length()=5 maxLength=10
result=109550 result.length()=6 maxLength=10
result=1095502 result.length()=7 maxLength=10
result=10955020 result.length()=8 maxLength=10
result=109550200 result.length()=9 maxLength=10
result=1095502006 result.length()=10 maxLength=10
result=1095502006 result.length()=10 maxLength=10
result.charAt(i)=1 maxString.charAt(i)=2
result.charAt(i)=0 maxString.charAt(i)=1
result.charAt(i)=9 maxString.charAt(i)=4
2147483647

```java
for(int i = 0;i<maxLength;i++){

                    if(result.charAt(i)>maxString.charAt(i)){
                        //out of range
                        if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }else{
                        break;
                    }
                }
```
                
>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.NumberFormatException: For input string: "2147483648"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:21)
	at java.lang.Integer.parseInt(Integer.java:543)
	at java.lang.Integer.parseInt(Integer.java:571)
	at Solution.myAtoi(Solution.java:83)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:48)
Last executed input:
"-2147483648"

```java
for(int i = 0;i<maxLength;i++){

                    if(result.charAt(i)>maxString.charAt(i)){
                        //out of range
                        if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }else if(result.charAt(i)<maxString.charAt(i)){
                        break;
                    }
                }
```                
                
```java
class Solution {
    public int myAtoi(String str) {
        //The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. 
        str = str.trim();
        //If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
        int length = str.length();
        if(str==null||length==0){
                //If no valid conversion could be performed, a zero value is returned.

            return 0;
        }
        //Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
        int index=0;
        char firstChar = str.charAt(index);
        boolean isPositive = true;
        switch(firstChar){
            case '+':
                index++;
                break;
            case '-':
                index++;
                isPositive = false;
                break;
            default:
                if(firstChar<'0'||firstChar>'9'){
                        //If no valid conversion could be performed, a zero value is returned.

                    return 0;
                }
        }
        
        String maxString = String.valueOf(Integer.MAX_VALUE);
        int maxLength = maxString.length();
        
        String result = "";
        while(index< length){
            char tmp = str.charAt(index);
            if(tmp<'0'||tmp>'9'){
                //The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
                break;
            }
            
            if(result.length()!=0||tmp!='0'){
                            result = result + tmp;

            }
            
            
            
            index++;
        }
        
        int resultLength = result.length();
        if(resultLength==maxLength){
                //the numerical value is out of the range of representable values
                for(int i = 0;i<maxLength;i++){

                    if(result.charAt(i)>maxString.charAt(i)){
                        //out of range
                        if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }else if(result.charAt(i)<maxString.charAt(i)){
                        break;
                    }
                }
                
            }else if(resultLength>maxLength){
            if(isPositive){
                            return Integer.MAX_VALUE;
                        } else{
                            return Integer.MIN_VALUE;
                        }
                    }
        
        
        if(resultLength==0){
            return 0;
        }
        
        Integer intResult = Integer.parseInt(result);
        
         if(isPositive){
                return intResult;
            } else{
                return 0-intResult;
        }
        
    //If no valid conversion could be performed, a zero value is returned.

        //Only the space character ' ' is considered as whitespace character.
    //Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
        

    }
}
```

>https://leetcode.com/submissions/detail/186135626/           
1079 / 1079 test cases passed.
Status: Accepted
Runtime: 32 ms          
You are here! 
Your runtime beats 42.94 % of java submissions.     


### RegEex
