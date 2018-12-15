Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
```
For example, given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

Difficulty:Medium  
Total Accepted:168.2K  
Total Submissions:532K  
Related Topics:Array, Two Pointer

### 解题思路
这道题的解法使用到了Two Pointer。把其中一个元素作为基准，进行双指针计算。计算的过程中把相差最小的数记下来，且同时把产生最小值的sum也记录下来，最后返回sum就可以了。

铭记一点的是，如果想用双指针算法，那目标数组必须是有序的，否则无法应用。
#### Scala
```scala
object Solution {
    def threeSumClosest(nums: Array[Int], target: Int): Int = {
        var sortedNums = nums.sorted
        var len = nums.length
        var res = 0
        var min = scala.Int.MaxValue
        for(i <- 0 until len){
            var left = i+1
            var right = len-1
            var first = sortedNums(i)
            while(left<right){
                var sum = first+sortedNums(left)+sortedNums(right)
                if(sum > target){
                    min = scala.math.min(min,scala.math.abs(target-sum))
                    if(min==scala.math.abs(target-sum)){
                        res = sum
                    }
                    right -=1
                }else if(sum==target) {
                    return target
                }else {
                    min = scala.math.min(min,scala.math.abs(target-sum))
                    if(min==scala.math.abs(target-sum)){
                        res = sum
                    }
                    left +=1
                }  
            }
        }
        res
    }
}
```