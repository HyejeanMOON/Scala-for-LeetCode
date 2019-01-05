Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

Example 1
```
Input: [3,0,1]
Output: 2
```
Example 2
```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```
Note:  
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?


### 解题思路
用数组内的数字和位置是否一样，不一样的话则不把不一样的位置返回，如果全都一样的话说明最后一位被删掉了，所以返回数组的长度就可以了。
#### Scala
```scala
object Solution {
    def missingNumber(nums: Array[Int]): Int = {
        var temp = nums.sorted
        //temp.foreach(println)
        var leng = temp.length
        var res = leng
        for(i <- 0 until leng){
            if(i != temp(i)){
                return i
            }
        }
        res
    }
}
```

#### Java
```java
class Solution {
    public int missingNumber(int[] nums) {
        Arrays.sort(nums);
        int leng = nums.length;
        for(int i=0; i<leng; i++){
            if(nums[i] != i){
                return i;
            }
        }
        return leng;
    }
}
```