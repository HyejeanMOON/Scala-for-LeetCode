
Given an array of 2n integers, your task is to group these integers into n pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.

Example 1:
```
Input: [1,4,3,2]

Output: 4
Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).
```
Note:
n is a positive integer, which is in the range of [1, 10000].
All the integers in the array will be in the range of [-10000, 10000].

### 解题思路
1. 首先写一个冒泡排序，把数组的顺序排好。
2. 然后把偶数位置的数累加。返回结果。



#### scala

```scala
object Solution {
    def arrayPairSum(nums: Array[Int]): Int = {
        var result:Int = 0
        var temp:Int = 0
        for(i <- 0 until nums.length-1){
            for(j <- 0 until nums.length-i-1){
                if(nums(j) > nums(j+1)){
                    temp = nums(j)
                    nums(j) = nums(j+1)
                    nums(j+1) = temp
                }
            }
        }
     
        var pairs = nums.length/2
        var loop = 1
        while(loop <= pairs){
            result += nums(2*(loop-1))
            loop += 1
            
        }
        
        
        result
    }
}
```
#### Java
```java
class Solution {
    public int arrayPairSum(int[] nums) {
        int leng = nums.length;
        int[] numSorted = nums;
        Arrays.sort(numSorted);
        int res = 0;
        for(int i=0;i<leng/2;i++){
            res = res + numSorted[2*i];
        }
        return res;
    }
}
```