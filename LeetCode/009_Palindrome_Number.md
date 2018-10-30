# 9. Palindrome Number
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:

    Input: 121
    Output: true
Example 2:

    Input: -121
    Output: false
    Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

Example 3:

    Input: 10
    Output: false
    Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

Follow up:
Coud you solve it without converting the integer to a string?

## Progress

### 32.22%


```java

class Solution {
    public boolean isPalindrome(int x) {
        
        if(x<0){
            return false;
        }
        
        if(x==0){
            return true;
        }
        
        //end with 0
        if(x%10==0){
            return false;
        }
        
        List digitList = new LinkedList();
        int tmp = x;
        while(tmp!= 0){
            digitList.add(tmp%10);
            tmp = tmp/10;
        }
        int length = digitList.size();
        //boolean isEven = length%2==0;
        //if(isEven){
            int index = 0;
            while(index<length/2){
                if(digitList.get(index)!=digitList.get(length-1-index)){
                    return false;
                }
                index++;
            }
        //}else{
            
        //}
        
        return true;
        
        
    }
}
```

>https://leetcode.com/submissions/detail/186358373/
11509 / 11509 test cases passed.
Status: Accepted
Runtime: 149 ms
You are here! 
Your runtime beats 32.22 % of java submissions.

