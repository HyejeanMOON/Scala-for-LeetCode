Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:
1. You must do this in-place without making a copy of the array.
1. Minimize the total number of operations.


### 解题思路
冒泡排序，把零排在最后面。


#### scala

```scala
object Solution {
    def moveZeroes(nums: Array[Int]): Unit = {
        var temp = 0
        for(i <- 0 until nums.length-1){
            for(j <- 0 until nums.length-1-i){
                if(nums(j) == 0){
                   temp = nums(j)
                   nums(j) = nums(j+1)
                   nums(j+1) = temp
                }
            }
        }
    }
}
```
#### Java
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int leng = nums.length;
        for(int i=0;i<leng;i++){
            for(int j=0;j<leng-1-i;j++){
                if(nums[j] == 0){
                    int temp = nums[j];
                    nums[j] = nums[j+1];
                    nums[j+1] = temp;
                }
            }
        }
    }
}
```