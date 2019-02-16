Given an array of integers nums, write a method that returns the "pivot" index of this array.

We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.

If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.

Example 1:
```
Input: 
nums = [1, 7, 3, 6, 5, 6]
Output: 3
Explanation: 
The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.
Also, 3 is the first index where this occurs.
```
Example 2:
```
Input: 
nums = [1, 2, 3]
Output: -1
Explanation: 
There is no index that satisfies the conditions in the problem statement.
```
Note:

The length of nums will be in the range [0, 10000].
Each element nums[i] will be an integer in the range [-1000, 1000].

Difficulty:Easy  
Total Accepted:17.3K  
Total Submissions:43.8K  
Related Topics:Array

### 解题思路
这道题给了我们一个数组，让我们求一个中枢点，使得该位置左右两边的子数组之和相等。这道题难度不大，直接按题意去搜索就行了，因为中枢点可能出现的位置就是数组上的位置，所以我们搜索一遍就可以找出来，我们先求出数组的总和，然后维护一个当前数组之和curSum，然后对于遍历到的位置，用总和减去当前数字，看得到的结果是否是curSum的两倍，是的话，那么当前位置就是中枢点，返回即可；否则就将当前数字加到curSum中继续遍历，遍历结束后还没返回，说明没有中枢点，返回-1即可。
#### Scala
```scala
object Solution {
    def pivotIndex(nums: Array[Int]): Int = {
        var sum = 0
        var curSum=0
        for(n <- nums){
            sum += n
        }
        for(i <- 0 until nums.length){
            if((sum-nums(i))==2*curSum){
                return i
            }else{
                curSum += nums(i)
            }
        }
        -1
    }
}
```