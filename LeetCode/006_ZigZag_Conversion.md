# 6. ZigZag Conversion

## Problem
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility 易读性)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows);
Example 1:

    Input: s = "PAYPALISHIRING", numRows = 3
    Output: "PAHNAPLSIIGYIR"
Example 2:

    Input: s = "PAYPALISHIRING", numRows = 4
    Output: "PINALSIGYAHRPI"
    Explanation:

    P     I    N
    A   L S  I G
    Y A   H R
    P     I
    
## Process

### 64 ms
multi dimension array

```java
class Solution {
    public String convert(String s, int numRows) {
        int length = s.length();
        int columnNum = length/(numRows-1);
        char[][] resultArray = new char[numRows][columnNum];
        int stringIndex = 0;
        int rowIndex = 0;
        int columnIndex = 0;
        boolean isReverse = false;
        while(stringIndex<length){
            resultArray[rowIndex][columnIndex] = s.charAt(stringIndex);
            stringIndex++;
            if(rowIndex==numRows){
                columnIndex++;
                isReverse = true;
            }else if(rowIndex==0&&columnIndex!=0){
                columnIndex++;
                isReverse = false;
            }
            if(isReverse){
                rowIndex--;
            }else{
                rowIndex++;
            }
    
        }
        
        String result = "";
        for(int i = 0; i < numRows; i++){
            for(int j = 0; j<columnNum;j++){
                result += resultArray[i][j];
            }
        }
        return result;
    }
}
```

>Your input
"PAYPALISHIRING"
3
Your answer
"PA\u0000H\u0000N\u0000APLSIIGY\u0000I\u0000R\u0000\u0000"
Expected answer
"PAHNAPLSIIGYIR"

```java
char tmp = resultArray[i][j];
                if(tmp!= null){
                   result += tmp;
                }
```

```java
char tmp = resultArray[i][j];
                if(tmp!= ''){
                   result += tmp;
                }
 ```
 
>Your input
"PAYPALISHIRING"
3
Your answer
Line 34: error: empty character literal
Expected answer
"PAHNAPLSIIGYIR"

>Google:java char 数组初始值

```if(tmp!= '0'){```

change the condition according to the hint.
```if(tmp!= '\u0000'){```

```java
class Solution {
    public String convert(String s, int numRows) {
        int length = s.length();
        int maxRowIndex = numRows-1;
        int columnNum = length/maxRowIndex;
        
        char[][] resultArray = new char[numRows][columnNum];
        int stringIndex = 0;
        int rowIndex = 0;
        int columnIndex = 0;
        boolean isReverse = false;
        while(stringIndex<length){
            resultArray[rowIndex][columnIndex] = s.charAt(stringIndex);
            stringIndex++;
            if(rowIndex==maxRowIndex){
                columnIndex++;
                isReverse = true;
            }else if(rowIndex==0&&columnIndex!=0){
                columnIndex++;
                isReverse = false;
            }
            if(isReverse){
                rowIndex--;
            }else{
                rowIndex++;
            }
    
        }
        
        String result = "";
        for(int i = 0; i < numRows; i++){
            for(int j = 0; j<columnNum;j++){
                char tmp = resultArray[i][j];
                if(tmp!= '\u0000'){
                   result += tmp;
                }
            }
        }
        return result;
    }
}
```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 4
	at Solution.convert(Solution.java:13)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:50)
Last executed input:
"PAYPALISHIRING"
4

debug:
>start stringIndex =0 rowIndex=0 columnIndex=0
end rowIndex=1 columnIndex0
start stringIndex =1 rowIndex=1 columnIndex=0
end rowIndex=2 columnIndex0
start stringIndex =2 rowIndex=2 columnIndex=0
end rowIndex=3 columnIndex0
start stringIndex =3 rowIndex=3 columnIndex=0
end rowIndex=2 columnIndex1
start stringIndex =4 rowIndex=2 columnIndex=1
end rowIndex=1 columnIndex1
start stringIndex =5 rowIndex=1 columnIndex=1
end rowIndex=0 columnIndex1
start stringIndex =6 rowIndex=0 columnIndex=1
end rowIndex=1 columnIndex2
start stringIndex =7 rowIndex=1 columnIndex=2
end rowIndex=2 columnIndex2
start stringIndex =8 rowIndex=2 columnIndex=2
end rowIndex=3 columnIndex2
start stringIndex =9 rowIndex=3 columnIndex=2
end rowIndex=2 columnIndex3
start stringIndex =10 rowIndex=2 columnIndex=3
end rowIndex=1 columnIndex3
start stringIndex =11 rowIndex=1 columnIndex=3
end rowIndex=0 columnIndex3
start stringIndex =12 rowIndex=0 columnIndex=3
end rowIndex=1 columnIndex4
start stringIndex =13 rowIndex=1 columnIndex=4
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 4
	at Solution.convert(MainClass.java:14)
    
change the column number.

```int columnNum = length/maxRowIndex+1;```

>Submission Result: Runtime Error 
Debug code in playground
Runtime Error Message:
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Solution.convert(Solution.java:5)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:50)
Last executed input:
""
1

deal with the edge params.

```java
if(length==0){
            return s;
        }
```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Solution.convert(Solution.java:8)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:50)
Last executed input:
"A"
1

```java
     if(length<2){
            return s;
        }
```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Solution.convert(Solution.java:8)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:50)
Last executed input:
"AB"
1

```if(length<3){```

>Submission Result: Runtime Error 
Runtime Error Message:
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Solution.convert(Solution.java:8)
	at __DriverSolution__.__helper__(__Driver__.java:4)
	at __Driver__.main(__Driver__.java:50)
Last executed input:
"ABC"
1

the problem is numRows, not the string length.
switch the restriction to numRows

```java
        if(numRows==1){
            return s;
        }
```
        
```java
class Solution {
    public String convert(String s, int numRows) {
        if(numRows==1){
            return s;
        }
        int length = s.length();
        int maxRowIndex = numRows-1;
        int columnNum = length/maxRowIndex+1;
        
        char[][] resultArray = new char[numRows][columnNum];
        int stringIndex = 0;
        int rowIndex = 0;
        int columnIndex = 0;
        boolean isReverse = false;
        while(stringIndex<length){
            resultArray[rowIndex][columnIndex] = s.charAt(stringIndex);
            stringIndex++;
            if(rowIndex==maxRowIndex){
                columnIndex++;
                isReverse = true;
            }else if(rowIndex==0&&columnIndex!=0){
                columnIndex++;
                isReverse = false;
            }
            if(isReverse){
                rowIndex--;
            }else{
                rowIndex++;
            }
    
        }
        
        String result = "";
        for(int i = 0; i < numRows; i++){
            for(int j = 0; j<columnNum;j++){
                char tmp = resultArray[i][j];
                if(tmp!= '\u0000'){
                   result += tmp;
                }
            }
        }
        return result;
    }
}
```

>Submission Detail
1158 / 1158 test cases passed.
Status: Accepted
Runtime: 64 ms
You are here! 
Your runtime beats 24.15 % of java submissions.
