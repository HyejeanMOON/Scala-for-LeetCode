Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

Note: The algorithm should run in linear time and in O(1) space.

Example 1:
```
Input: [3,2,3]
Output: [3]
```
Example 2:
```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```

Difficulty:Medium  
Total Accepted:72.6K  
Total Submissions:246.8K  
Related Topics:Array

### 解题思路
这道题让我们求出现次数大于n/3的众数，而且限定了时间和空间复杂度，那么就不能排序，也不能使用哈希表，这么苛刻的限制条件只有一种方法能解了，那就是摩尔投票法 Moore Voting，这种方法在之前那道题Majority Element 求众数中也使用了。题目中给了一条很重要的提示，让我们先考虑可能会有多少个众数，经过举了很多例子分析得出，任意一个数组出现次数大于n/3的众数最多有两个，具体的证明我就不会了，我也不是数学专业的。那么有了这个信息，我们使用投票法的核心是找出两个候选众数进行投票，需要两遍遍历，第一遍历找出两个候选众数，第二遍遍历重新投票验证这两个候选众数是否为众数即可，选候选众数方法和前面那篇Majority Element 求众数一样，由于之前那题题目中限定了一定会有众数存在，故而省略了验证候选众数的步骤，这道题却没有这种限定，即满足要求的众数可能不存在，所以要有验证。
### Scala
```scala
object Solution {
    def majorityElement(nums: Array[Int]): List[Int] = {
        var res:List[Int] = List()
        var m=0
        var n=0
        var cm=0
        var cn=0
        for(s <- nums){
            if(s==m) cm+=1
            else if(s==n) cn+=1
            else if(cm==0){
                m=s
                cm=1
            }else if(cn==0){
                n=s
                cn=1
            }else{
                cm-=1
                cn-=1
            }
        }
        cn=0
        cm=0
        for(s <- nums){
            if(m==s) cm+=1
            else if(n==s) cn+=1
        }
        if(cn>nums.length/3) res=res:+n
        if(cm>nums.length/3) res=res:+m
        res
    }
}
```

---

如果不考虑note中的要求的话，直接用map记录就好了。
#### Scala
```scala
object Solution {
    def majorityElement(nums: Array[Int]): List[Int] = {
        if(nums.isEmpty) return List()
        var record:Map[Int,Int] = Map()
        var res:List[Int] = List()
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp+=1
            record+=(n -> temp)
        }
        var key = record.keySet
        for(k <- key){
            if(record.getOrElse(k,0)>nums.length/3) res=res:+k
        }
        res
    }
}
```