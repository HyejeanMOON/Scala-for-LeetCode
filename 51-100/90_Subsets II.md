Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:
```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

Difficulty:Medium  
Total Accepted:148.4K    
Total Submissions:384.3K  
Related Topics: Array, Backtracking

### 解题思路
这道子集合之二是之前那道 Subsets 子集合 的延伸，这次输入数组允许有重复项，其他条件都不变，只需要在之前那道题解法的基础上稍加改动便可以做出来，我们先来看非递归解法，拿题目中的例子[1 2 2]来分析，根据之前 Subsets 子集合 里的分析可知，当处理到第一个2时，此时的子集合为[], [1], [2], [1, 2]，而这时再处理第二个2时，如果在[]和[1]后直接加2会产生重复，所以只能在上一个循环生成的后两个子集合后面加2，发现了这一点，题目就可以做了，我们用last来记录上一个处理的数字，然后判定当前的数字和上面的是否相同，若不同，则循环还是从0到当前子集的个数，若相同，则新子集个数减去之前循环时子集的个数当做起点来循环，这样就不会产生重复了。
#### Scala
```scala
object Solution {
    def subsetsWithDup(nums: Array[Int]): List[List[Int]] = {
        if(nums.isEmpty) return List()
        var num = nums.sorted
        var res:List[List[Int]] = List()
        res = res :+ List()
        var last = scala.Int.MinValue
        var size = 0
        for(i <- 0 until num.length){
            if(last!=num(i)){
                last = num(i)
                size = res.size
            }
            var newSize = res.size
            for(j <- newSize-size until newSize){
                var temp = res(j) :+ num(i)
                res = res :+ temp
            }
        }
        res
    }
}
```