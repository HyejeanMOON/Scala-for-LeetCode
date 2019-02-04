A zero-indexed array A of length N contains all integers from 0 to N-1. Find and return the longest length of set S, where S[i] = {A[i], A[A[i]], A[A[A[i]]], ... } subjected to the rule below.

Suppose the first element in S starts with the selection of element A[i] of index = i, the next element in S should be A[A[i]], and then A[A[A[i]]]… By that analogy, we stop adding right before a duplicate element occurs in S.

Example 1:
```
Input: A = [5,4,0,3,1,6,2]
Output: 4
Explanation: 
A[0] = 5, A[1] = 4, A[2] = 0, A[3] = 3, A[4] = 1, A[5] = 6, A[6] = 2.

One of the longest S[K]:
S[0] = {A[0], A[5], A[6], A[2]} = {5, 6, 2, 0}
```
Note:  
- N is an integer within the range [1, 20,000].  
- The elements of A are all distinct.  
- Each element of A is an integer within the range [0, N-1].  

Difficulty:Medium  
Total Accepted:21.9K  
Total Submissions:43.9K  
Related Topics:Array


### 解题思路
这道题让我们找嵌套数组的最大个数，给的数组总共有n个数字，范围均在[0, n-1]之间，题目中也把嵌套数组的生成解释的很清楚了，其实就是值变成坐标，得到的数值再变坐标。那么实际上当循环出现的时候，嵌套数组的长度也不能再增加了，而出现的这个相同的数一定是嵌套数组的首元素，博主刚开始没有想清楚这一点，以为出现重复数字的地方可能是嵌套数组中间的某个位置，于是用个set将生成的嵌套数组存入，然后每次查找新生成的数组是否已经存在。而且还以原数组中每个数字当作嵌套数组的起始数字都算一遍，结果当然是TLE了。其实对于遍历过的数字，我们不用再将其当作开头来计算了，而是只对于未遍历过的数字当作嵌套数组的开头数字，不过在进行嵌套运算的时候，并不考虑中间的数字是否已经访问过，而是只要找到和起始位置相同的数字位置，然后更新结果res。
#### Scala
```Scala
object Solution {
    def arrayNesting(nums: Array[Int]): Int = {
        var record = new scala.collection.mutable.ArrayBuffer[Boolean]
        var len = nums.length
        for(i <- 0 until len){
            record = record :+ false
        }
        var count = 1
        var res = 0
        for(i <- 0 until len){
            var cur = i
            count=1
            if(!record(i)){
                while(nums(cur)!=i){
                    record(cur) = true
                    cur = nums(cur)
                    count+=1
                }
            }
            res = scala.math.max(res,count)      
        }
        res
        
    }
}
```