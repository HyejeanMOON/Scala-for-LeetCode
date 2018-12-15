Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### 解题思路
双循环搜索，把匹配的数字的位置记录下来，并返回。

#### Scala 
```Scala
object Solution {
    def twoSum(nums: Array[Int], target: Int): Array[Int] = {
        var flag = true
        var returnResult:Array[Int] = Array()
        for(poOuter <- 0 until nums.length if flag){
            for(poInner <- poOuter+1 until nums.length if flag){
                if(target == (nums(poOuter) + nums(poInner))){
                    flag = false
                    returnResult = returnResult :+ poOuter
                    returnResult = returnResult :+ poInner
                } 
            }
        }
        returnResult
    }

}
```
#### Java
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int leng = nums.length;
        for(int i=0; i < leng-1; i++){
            for(int j=i+1; j<leng; j++){
                if(nums[i] + nums[j] == target){
                    int[] res = new int[]{i,j};
                    return res;
                }
            }
        }
        return nums;
    }
}
```

Java
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        HashMap<Integer,Integer> record = new HashMap<Integer,Integer>();
        for(int i=0; i<nums.length; i++){
            if(!record.containsKey(target-nums[i])){
                record.put(nums[i],i);
            }else{
                res[0]=record.get(target-nums[i]);
                res[1]=i;
                break;
            }
        }
        return res;
    }
}
```