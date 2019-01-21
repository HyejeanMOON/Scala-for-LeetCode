Given two arrays, write a function to compute their intersection.

Example:  
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

Note:  
Each element in the result must be unique.
The result can be in any order.

### 解题思路
遍历数组，用map记录。然后以nums2为key，如果值大于0则记录。然后把值更新为0，防止被重复记录。
#### Scala
```scala
object Solution {
    def intersection(nums1: Array[Int], nums2: Array[Int]): Array[Int] = {
        var res:Array[Int] = Array()
        var leng1 = nums1.length
        var leng2 = nums2.length
        if(leng1 == 0 || leng2 == 0) return res
        var record:Map[Int,Int] = Map()
        for(i <- 0 until leng1){
            var temp = record.getOrElse(nums1(i),0)
            temp += 1
            record += (nums1(i) -> temp)
        }
        for(n <- nums2){
            var temp = record.getOrElse(n,0)
            if(temp > 0) res = res :+ n
            record += (n -> 0)
        }
        res = res.sorted
        res
    }
}
```