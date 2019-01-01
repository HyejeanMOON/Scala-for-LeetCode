A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.

Difficulty:Medium  
Total Accepted:148.2K  
Total Submissions:381.4K  
Related Topics:Array, Binary Search

### 解题思路
该题的思路是寻找最大数，但要求是那个数比相邻两个数大。特例是len=1的时候直接return 0， 然后就是先找0和len-1的情况，最后就开始搜索中间部分。
#### Scala
```scala
object Solution {
    def findPeakElement(nums: Array[Int]): Int = {
        var len = nums.length
        var res = 0
        var max = scala.Int.MinValue
        if(len==1) return 0
        for(i <- 0 until len){
            if(i==0){
                if(nums(0)>nums(1)){
                    res = 0
                    max = nums(0)
                }
            }else if(i==(len-1)){
                if(nums(len-1)>nums(len-2)){
                    if(max<nums(len-1)){
                        res = len-1
                        max = nums(len-1)
                    }
                }
            }else{
                if(nums(i)>nums(i-1) && nums(i)>nums(i+1)){
                    if(max<nums(i)){
                        res = i
                        max = nums(i)
                    }
                }
            }
        }
        res
    }
}
```