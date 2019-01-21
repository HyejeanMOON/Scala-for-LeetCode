Given a non-empty array of integers, return the k most frequent elements.

For example,  
Given [1,1,1,2,2,3] and k = 2, return [1,2].

Note:   
- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.  
- Your algorithm's time complexity must be better than O(n log n), where n is the array's size.


### 解题思路
这道题需要用map进行记录。然后对出现的次数进行对比，把已经获得答案，赋予零。让它在下一次的搜索中不会被选出来。
#### Scala
```scala
object Solution {
    def topKFrequent(nums: Array[Int], k: Int): List[Int] = {
        if(nums.isEmpty) return List()
        var record:Map[Int,Int] = Map()
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp+=1
            record+=(n -> temp)           
        }
        var res:List[Int] = List()
        var mxEle = scala.Int.MinValue
        var mxNum = scala.Int.MinValue
        var keys = record.keySet
        for(i <- 0 until k){
            for(key <- keys){
                var temp = record.getOrElse(key,0)          
                if(mxNum<temp){
                  record+=(mxEle -> mxNum)
                  mxEle=key
                  mxNum=temp
                }
            }
            res=res:+mxEle
            record+=(mxEle -> 0)
            mxEle=0
            mxNum=scala.Int.MinValue
        }
        res
    }
}
```