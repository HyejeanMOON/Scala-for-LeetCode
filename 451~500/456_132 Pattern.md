Given a sequence of n integers a1, a2, ..., an, a 132 pattern is a subsequence ai, aj, ak such that i < j < k and ai < ak < aj. Design an algorithm that takes a list of n numbers as input and checks whether there is a 132 pattern in the list.

Note: n will be less than 15,000.

Example 1:
```
Input: [1, 2, 3, 4]

Output: False

Explanation: There is no 132 pattern in the sequence.
```
Example 2:
```
Input: [3, 1, 4, 2]

Output: True

Explanation: There is a 132 pattern in the sequence: [1, 4, 2].
```
Example 3:
```
Input: [-1, 3, 2, 0]

Output: True

Explanation: There are three 132 patterns in the sequence: [-1, 3, 2], [-1, 3, 0] and [-1, 2, 0].
```

Difficulty:Medium  
Total Accepted:18.3K  
Total Submissions:66.1K  
Related Topics:Stack

### 解题思路
这道题给我们了一个数组，让我们找到132的模式，就是第一个数小于第二第三个数，且第三个数小于第二个数。那么我们就按顺序来找这三个数，首先我们来找第一个数，这个数需要最小，那么我们如果发现当前数字大于等于后面一个数字，我们就往下继续遍历，直到当前数字小于下一个数字停止。然后我们找第二个数字，这个数字需要最大，那么如果我们发现当前数字小于等于下一个数字就继续遍历，直到当前数字大雨下一个数字停止。最后就找第三个数字，我们验证这个数字是否在之前两个数字的中间，如果没有找到，我们就从第二个数字的后面一个位置继续开始重新找这三个数字。
#### Scala
```scala
object Solution {
    def find132pattern(nums: Array[Int]): Boolean = {
        var n = nums.length
        var i = 0
        var j = 0 
        var k = 0
        while(i<n){
            while(i<n-1 && nums(i)>=nums(i+1)) i+=1
            j = i+1
            while(j<n-1 && nums(j)<=nums(j+1)) j+=1
            k=j+1
            while(k<n){
                if(nums(k)>nums(i) && nums(k)<nums(j)) return true
                k+=1
            }
            i = j+1
        }
        false
    }
}
```