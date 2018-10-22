
## Review
1. Forgot basic methods and principles without IDE's help.
2. Figure out the requirement of the problem, like the output.
3. Consider the algorithm efficiency.
4. Consider more testcases.

---

## Question
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

>Example:
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

----

## Process

### Twice Traversiong

int[] nums
没有nums.size()和nums.length()
只有length

看清题目，run the code时候才发现是要返回indices ，而不是数本身

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i < nums.length-1; i++){
            for(int j = i+1; j < nums.length; j++){
                if(nums[i]+nums[j]==target){
                    return new int[]{i,j};
                }
            }
        }
        return null;
    }
}
```

>29 / 29 test cases passed.
Status: Accepted
Runtime: 40 ms
You are here! 
Your runtime beats 21.72 % of java submissions.

Not satisfied with the efficiency.

---

### Sort First

>看到Discuss中有个帖子的标题提到sort

1. 直接使用list.sort()转换，然而没有这个方法，应该使用```Collections.sort();//默认排序(从小到大)```

2. 不能把基本数据类型转化为列表
>List numList = Arrays.asList(nums);
Line 10: error: bad operand types for binary operator '+'
 
3. 泛型不能用基本类型
List<int> numList = new ArrayList<int>();
Line 3: error: unexpected type

List<Integer> numList = new ArrayList<Integer>();
ok

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        List<Integer> numList = new ArrayList<Integer>();
        for(int tmp:nums){
            numList.add(tmp);
        }
        
        Collections.sort(numList);
        
        int size = numList.size();
        for(int i = 0; i < size-1; i++){
            int j = i+1;
            while(j<size){
                int tmp = numList.get(i) + numList.get(j);
                if(tmp==target){
                    return new int[]{i,j};
                }else if(tmp>target){
                    break;
                }else{
                    j++;
                    continue;
                }   
            }
            
        }
        return null;
    }
}
```

>Submission Result: Wrong Answer 
Input:
[3,2,4]
6
Output:
[0,2]
Expected:
[1,2]

返回的是排序后的序号，而非原始的序号了。

#### 使用map记录原始序号

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        List<Integer> numList = new ArrayList<Integer>();
        Map<Integer,Integer> indexMap = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            numList.add(nums[i]);
            indexMap.put(nums[i],i);
        }
        
        Collections.sort(numList);
        
        int size = numList.size();
        for(int i = 0; i < size-1; i++){
            int j = i+1;
            while(j<size){
                int tmp = numList.get(i) + numList.get(j);
                if(tmp==target){
                    return new int[]{indexMap.get(numList.get(i)),indexMap.get(numList.get(j))};
                }else if(tmp>target){
                    break;
                }else{
                    j++;
                    continue;
                }   
            }
            
        }
        return null;
    }
}
```

>Submission Result: Wrong Answer 
Input:
[3,3]
6
Output:
[1,1]
Expected:
[0,1]

没有考虑相同数值的情况，map的key冲突了。

#### 优化，使用list.indexOf()

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        List<Integer> numList = new ArrayList<Integer>();
        List<Integer> rawNumList = new ArrayList<Integer>();

        Map<Integer,Integer> indexMap = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            numList.add(nums[i]);
            rawNumList.add(nums[i]);
        }
        
        Collections.sort(numList);
        
        int size = numList.size();
        for(int i = 0; i < size-1; i++){
            int j = i+1;
            while(j<size){
                int tmp = numList.get(i) + numList.get(j);
                if(tmp==target){
                    return new int[]{rawNumList.indexOf(numList.get(i)),rawNumList.indexOf(numList.get(j))};
                }else if(tmp>target){
                    break;
                }else{
                    j++;
                    continue;
                }   
            }
            
        }
        return null;
    }
}
```

>Submission Result: Wrong Answer 
Input:
[3,3]
6
Output:
[0,0]
Expected:
[0,1]

list的indexOf取得是第1次出现的序号。

#### 使用lastIndexOf绕开问题

```return new int[]{rawNumList.indexOf(numList.get(i)),rawNumList.lastIndexOf(numList.get(j))};```

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        List<Integer> numList = new ArrayList<Integer>();
        List<Integer> rawNumList = new ArrayList<Integer>();

        Map<Integer,Integer> indexMap = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            numList.add(nums[i]);
            rawNumList.add(nums[i]);
        }
        
        Collections.sort(numList);
        
        int size = numList.size();
        for(int i = 0; i < size-1; i++){
            int j = i+1;
            while(j<size){
                int tmp = numList.get(i) + numList.get(j);
                if(tmp==target){
                    return new int[]{rawNumList.indexOf(numList.get(i)),rawNumList.lastIndexOf(numList.get(j))};
                }else if(tmp>target){
                    break;
                }else{
                    j++;
                    continue;
                }   
            }
            
        }
        return null;
    }
}
```
                   
>29 / 29 test cases passed.
Status: Accepted
Runtime: 12 ms               
You are here! 
Your runtime beats 44.57 % of java submissions.
