
# Longest Substring Without Repeating Characters
## Problem

Given a string, find the length of the longest substring without repeating characters.

Example 1:

    Input: "abcabcbb"
    Output: 3 
    Explanation: The answer is "abc", with the length of 3. 

Example 2:

    Input: "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.
Example 3:

    Input: "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.


## Record

### 1

```String tmp = s.indexOf(j);```

```subStringSet.empty();```

>Google:java set empty


```subStringSet.clear();```


```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    subStringSet.clear();
                    if(result<tmpLength){
                        result = tmpLength;
                    }
                    break;
                }
            }
        }
        
        return result;
    }
}
```

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    subStringSet.clear();
                    if(result<tmpLength){
                        result = tmpLength;
                    }
                    break;
                }
            }
            if(result==(length-i)){
                break;
            }
        }
        
        return result;
    }
}
```

>Submission Result: Wrong Answer 
Input:
" "
Output:
0
Expected:
1




- - -

#### success 145 ms

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    subStringSet.clear();
                    if(result<tmpLength){
                        result = tmpLength;
                    }
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            if(result==(length-i)){
                break;
            }
        }
        
        return result;
    }
}
```

>987 / 987 test cases passed.
Status: Accepted
Runtime: 145 ms
You are here! 
Your runtime beats 10.79 % of java submissions.


- - -


#### success 88 ms

```if(result>=(length-i)){```


>987 / 987 test cases passed.
Status: Accepted
Runtime: 88 ms
You are here! 
Your runtime beats 17.64 % of java submissions.

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();
                 
                    if(result<tmpLength){
                        result = tmpLength;
                    }
                    
                    //next loop start here
                    i=j;
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            if(result>=(length-i)){
                break;
            }
            
        }
        
        return result;
    }
}
```

>Submission Result: Wrong Answer 
Input:
"aab"
Output:
1
Expected:
2

```if(result>(length-i)){```
            
>Submission Result: Wrong Answer 
Input:
"aab"
Output:
1
Expected:
2

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            int startIndex = i;
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();
                 
                    if(result<tmpLength){
                        result = tmpLength;
                    }
                    
                    //next loop start here
                    startIndex=j;
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            if(result>(length-i)){
                break;
            }
            i = startIndex;
            
        }
        
        return result;
    }
}
```

>Submission Result: Wrong Answer 
Input:
"aab"
Output:
1
Expected:
2

            if(result>=(length-i)){

>Submission Result: Wrong Answer 
Input:
"aab"
Output:
1
Expected:
2


- - -

#### success 107 ms

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            //int startIndex = i;
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();        
                    
                    //next loop start here
                    //startIndex=j;
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            //length-i-1 = next loop max length
            if(result>=(length-i-1)){
                break;
            }
            //i = startIndex;
            
        }
        
        return result;
    }
}
```

>987 / 987 test cases passed.
Status: Accepted
Runtime: 107 ms
You are here! 
Your runtime beats 14.93 % of java submissions.


next loop start here找的地方是错误的，如abac
aba重现重复时不能直接从第二个a处开始
应该是tmp的index的下一处
```startIndex=s.indexOf(tmp);```

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            int startIndex = i;
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();        
                    
                    //next loop start here
                    startIndex=s.indexOf(tmp);
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            //length-i-1 = next loop max length
            if(result>=(length-i-1)){
                break;
            }
            
            i = startIndex;
        }
        
        return result;
    }
}
```

>Time Limit Exceeded
Run Code Result:
Your input
"abcabcbb"
Your answer
Expected answer
3

死循环


- - -


```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            int startIndex = i;
            String tmpString = "";
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                tmpString += tmp;
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();        
                    
                    //next loop start here
                    startIndex=s.indexOf(tmpString);
                    tmpString = "";
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            //length-i-1 = next loop max length
            if(result>=(length-i-1)){
                break;
            }
            
            i = startIndex;
        }
        
        return result;
    }
}
```

>Submission Result: Time Limit Exceeded 
Last executed input:
"bbbbb"

- - -

#### success 40 ms

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int result = 0;
        int length = s.length();
        int maxResult = length;
        
        Set stringSet = new HashSet();
        for(int i = 0;i<length;i++){
            stringSet.add(s.charAt(i));
        }
        if(stringSet.size()==1){
            return 1;
        }else{
            maxResult = stringSet.size();
        }

        

        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            int startIndex = i;
            //String tmpString = "";
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                ////tmpString += tmp;
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();        
                    
                    //next loop start here
                    //startIndex=s.indexOf(tmpString);
                    //tmpString = "";
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            //probably max Result
            if(result == maxResult){
                break;
            }
            
            //length-i-1 = next loop max length
            if(result>=(length-i-1)){
                break;
            }
            
            //i = startIndex;
        }
        
        return result;
    }
}
```

>987 / 987 test cases passed.
Status: Accepted
Runtime: 40 ms
You are here! 
Your runtime beats 52.78 % of java submissions.


- - -

#### success 48ms


调整语句顺序，去除多余局部变量

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int length = s.length();
        
        int maxResult = length;
        Set stringSet = new HashSet();
        for(int i = 0;i<length;i++){
            stringSet.add(s.charAt(i));
        }
        if(stringSet.size()==1){
            return 1;
        }else{
            maxResult = stringSet.size();
        }  
        
        int result = 0;
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            //int startIndex = i;
            //String tmpString = "";
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                ////tmpString += tmp;
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();        
                    
                    //next loop start here
                    //startIndex=s.indexOf(tmpString);
                    //tmpString = "";
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            //probably max Result
            if(result == maxResult){
                break;
            }
            
            //length-i-1 = next loop max length
            if(result>=(length-i-1)){
                break;
            }
            
            //i = startIndex;
        }
        
        return result;
    }
}
```

>987 / 987 test cases passed.
Status: Accepted
Runtime: 48 ms
You are here! 
Your runtime beats 38.48 % of java submissions.


- - -

#### success 67ms

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int length = s.length();
        
        int maxResult = length;
        Set stringSet = new HashSet();
        for(int i = 0;i<length;i++){
            stringSet.add(s.charAt(i));
        }
        if(stringSet.size()==1){
            return 1;
        }else{
            maxResult = stringSet.size();
        }  
        
        int result = 0;
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            int startIndex = i;
            String tmpString = "";
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                tmpString += tmp;
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();        
                    
                    //next loop start here
                    if(s.indexOf(tmpString)==s.lastIndexOf(tmpString)){
                        startIndex=s.indexOf(tmpString);
                    }
                    tmpString = "";
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            //probably max Result
            if(result == maxResult){
                break;
            }
            
            //length-i-1 = next loop max length
            if(result>=(length-i-1)){
                break;
            }
            
            i = startIndex;
        }
        
        return result;
    }
}
```

>987 / 987 test cases passed.
Status: Accepted
Runtime: 67 ms
You are here! 
Your runtime beats 23.71 % of java submissions.



- - -

#### success 50ms

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int length = s.length();
        
        int maxResult = length;
        Set stringSet = new HashSet();
        for(int i = 0;i<length;i++){
            stringSet.add(s.charAt(i));
        }
        if(stringSet.size()==1){
            return 1;
        }else{
            maxResult = stringSet.size();
        }  
        
        int result = 0;
        Set subStringSet = new HashSet();
        for(int i = 0;i<length;i++){
            int tmpLength = 0;
            int startIndex = i;
            
            for(int j = i;j<length;j++){
                char tmp = s.charAt(j);
                if(!subStringSet.contains(tmp)){
                    subStringSet.add(tmp);
                    tmpLength++;
                }else{
                    //repeat character
                    subStringSet.clear();        
                    
                    //next loop start here
                    startIndex=s.indexOf(tmp,i);
                    break;
                }
            }
            
            if(result<tmpLength){
                result = tmpLength;
            }
            
            //probably max Result
            if(result == maxResult){
                break;
            }
            
            //length-i-1 = next loop max length
            if(result>=(length-i-1)){
                break;
            }
            
            i = startIndex;
        }
        
        return result;
    }
}
```

>987 / 987 test cases passed.
Status: Accepted
Runtime: 50 ms
You are here! 
Your runtime beats 35.45 % of java submissions.
