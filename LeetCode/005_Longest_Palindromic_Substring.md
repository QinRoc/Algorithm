# 5. Longest Palindromic Substring


## Review
1. break immediately;

- - -


## Problem
Given a string s, find the longest palindromic 回文 substring in s. You may assume that the maximum length of s is 1000.

Example 1:

    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.
Example 2:

    Input: "cbbd"
    Output: "bb"

## Process
### 1

```int length = s.length```

```String boxString = s.subString(index,boxSize-1-index);```
should be `substring`

```if(!s.charAt(index).equals(s.charAt(length-1-index))){```

>Line 37: error: char cannot be dereferenced

>Google:java char equal
直接用==


>Line 44: error: bad operand type char for unary operator '!'

>Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: 3
	at java.lang.String.charAt(String.java:614)
 
```java
class Solution {
    public String longestPalindrome(String s) {
        //the result length is between [2,s.length]
        //how to go over the string
        //a box slip
        //how to check palindromic
        int length = s.length();
       
        int boxSize = length;
        // check from the longest
        while(boxSize>1){
            int offset = length-boxSize;
            
            int index = 0;
            while(index<=offset){
                String boxString = s.substring(index,boxSize-1-index);
                if(isPalindromic(boxString)){
                    return boxString;
                }
                index++;
            }
            
            boxSize--;
        }
        
        return null;
        
    }
    
    private boolean isPalindromic(String s){
        int length = s.length();
        int median = length/2;
        int index = median;
        boolean isEven = length%2==0;
        if(isEven){
            while(index<length){
                if(s.charAt(index)!=s.charAt(length-1-index)){
                    return false;
                }
                index++;
            }
        }else{
            while(index<length-1){
                if(s.charAt(index+1)!=s.charAt(length-2-index)){
                    return false;
                }
                index++;
            }
            
        }
        return true;
    }
}
```

>Submission Result: Wrong Answer 
Input:
"cbbd"
Output:
""
Expected:
"bb"

```String boxString = s.substring(index,length-1-index);```

>Your input
"babad"
Your answer
""
Expected answer
"aba"

debug with print
>Google:java print

substring not include the end

```String boxString = s.substring(index,length-index+offset);```
                

>Submission Result: Wrong Answer 
Input:
""
Output:
null
Expected:
""

>Submission Result: Wrong Answer 
Input:
"a"
Output:
""
Expected:
"a"

add         
```java
if(length==1){
            return s;
        }
```


>Submission Result: Wrong Answer 
Input:
"ac"
Output:
""
Expected:
"a"


```return s.charAt(0);```

>Submission Result: Compile Error 
Line 29: error: incompatible types: char cannot be converted to String

```return s.substring(0,0);```
        
```return s.substring(0,1);```

        
>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: 1
	at java.lang.String.substring(String.java:1919)
	at Solution.longestPalindrome(Solution.java:29)
	at __DriverSolution__.__helper__(__Driver__.java:10)
	at __Driver__.main(__Driver__.java:54)
Last executed input:
""

```java
if(length<=1){
    return s;
}
```

```java
class Solution {
    public String longestPalindrome(String s) {
        //the result length is between [2,s.length]
        //how to go over the string
        //a box slip
        //how to check palindromic
        int length = s.length();
        if(length<=1){
            return s;
        }
       
        int boxSize = length;
        // check from the longest
        while(boxSize>1){
            int offset = length-boxSize;
            
            int index = 0;
            while(index<=offset){
                String boxString = s.substring(index,index+boxSize);
                if(isPalindromic(boxString)){
                    return boxString;
                }
                index++;
            }
            
            boxSize--;
        }
        
        return s.substring(0,1);
        
    }
    
    private boolean isPalindromic(String s){
        int length = s.length();
        int median = length/2;
        int index = median;
        boolean isEven = length%2==0;
        if(isEven){
            while(index<length){
                if(s.charAt(index)!=s.charAt(length-1-index)){
                    return false;
                }
                index++;
            }
        }else{
            while(index<length-1){
                if(s.charAt(index+1)!=s.charAt(length-2-index)){
                    return false;
                }
                index++;
            }
            
        }
        return true;
    }
}
```
        
>You are here! 
Your runtime beats 5.13 % of java submissions.
103 / 103 test cases passed.
Status: Accepted
Runtime: 721 ms


- - -

optimize the method for checking palindromic

```java
if(isEven){
            String former = s.substring(0,median-1);
            String latter = s.substring(median,length);
            if(!former.equals(latter.reverse())){
                return false;
            }
            
        }else{
            String former = s.substring(0,median);
            String latter = s.substring(median+1,length);
            if(!former.equals(latter.reverse())){
                return false;
            }
        }
```


java string reverse

there is no string method reverse()

---

optimize find the target

abcba
2 char repeat
so the target size is 

```java
 Set stringSet = new HashSet();
        for(int i=0;i<length;i++){
            stringSet.add(s.charAt(i));
        }
        int targetSize = length-stringSet.size();
       
        int boxSize = targetSize;
```

Your input
"babad"
Your answer
"b"
Expected answer
"aba"

        int targetSize = length-stringSet.size()+1;

but probably multi same char

>Submission Result: Wrong Answer 
Input:
"aba"
Output:
"a"
Expected:
"aba

```java
public String longestPalindrome(String s) {
        //the result length is between [2,s.length]
        //how to go over the string
        //a box slip
        //how to check palindromic
        int length = s.length();
        if(length<=1){
            return s;
        }
        
        Set stringSet = new HashSet();
        for(int i=0;i<length;i++){
            stringSet.add(s.charAt(i));
        }
        int targetSize = (length-stringSet.size())*2+1;
       
        int boxSize = targetSize;
        // check from the longest
        int offset = length-boxSize;

        int index = 0;
        while(index<=offset){
            String boxString = s.substring(index,index+boxSize);
            if(isPalindromic(boxString)){
                return boxString;
            }
            index++;
        }
              
        return s.substring(0,1);
        
    }
```

>Your input
"babad"
Your answer
"b"
Expected answer
"aba"

5-3=2
2*2或2*2+1


- - -

if a char has repeat then it might be the start char in the target string


                if((int index = s.indexOf(c,i))>i){

Line 15: error: '.class' expected

```java
for(int i =0;i<length;i++){
            for(int j =i;j<length;j++){
                char c = s.charAt(i);
                int index;
                if((index = s.indexOf(c,i))>i){
                    //the char has repeat and the repeat char might be the end
                    String boxString = s.substring(i,index);
                    if(isPalindromic(boxString)){
                        return boxString;
                    }

                }
            }
           
        }
```
               int index= s.indexOf(c,j);
should be
               int index= s.indexOf(c,j+1);

```java
for(int i =0;i<length;i++){
            char c = s.charAt(i);
            for(int j=i;j<length;j++){
               int index= s.indexOf(c,j+1);
                if(index>i){
                    //the char has repeat and the repeat char might be the end
                    String boxString = s.substring(i,index+1);
                    if(isPalindromic(boxString)){
                        return boxString;
                    }
                    j = index;
                }else{
                    break;
                }
            }
           
        }
```

Submission Result: Wrong Answer 
Input:
"ccc"
Output:
"cc"
Expected:
"ccc"

```language
for(int i =0;i<length;i++){
            char c = s.charAt(i);
            for(int j=length;j>i;j--){
               int index= s.lastIndexOf(c,j-1);
                if(index>i){
                    //the char has repeat and the repeat char might be the end
                    String boxString = s.substring(i,index+1);
                    if(isPalindromic(boxString)){
                        return boxString;
                    }
                    j = index;
                }else{
                    //no repeat
                    break;
                }
            }
           
        }
```

>Submission Result: Wrong Answer 
Input:
"abacab"
Output:
"aba"
Expected:
"bacab"

```language
int resultLength = 1;
        String resultString = s.substring(0,1);
        
        for(int i =0;i<length;i++){
            if(length-i<resultLength){
                break;
            }
            char c = s.charAt(i);

            for(int j=length;j>i;j--){
               int index= s.lastIndexOf(c,j-1);
                if(index-i+1>resultLength){
                    //the char has repeat and the repeat char might be the end
                    String boxString = s.substring(i,index+1);

                    if(isPalindromic(boxString)){
                        resultString = boxString;
                        resultLength = index+1-i;
                    }
                    j = index;
                }else{
                    //no repeat
                    break;
                }
            }
           
        }
              
        return resultString;
```

>Submission Result: Wrong Answer 
Input:
"aaabaaaa"
Output:
"aabaa"
Expected:
"aaabaaa"

i=0 char=a
i=0 index=7 boxString=aaabaaaa
i=0 index=5 boxString=aaabaa
i=0 index=2 boxString=aaa
j-1和j--重复
