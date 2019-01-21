Given two arrays, write a function to compute their intersection.

Example:  
```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].
```
Note:  
Each element in the result should appear as many times as it shows in both arrays.
The result can be in any order.
Follow up:  
- What if the given array is already sorted? How would you optimize your algorithm?
- What if nums1's size is small compared to nums2's size? Which algorithm is better?
- What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### 解题思路
遍历nums1数组并且用map记录元素和出现的数。然后应用于nums2，并自减一，然手记录到数组中返回。
#### Scala
```scala
object Solution {
    def intersect(nums1: Array[Int], nums2: Array[Int]): Array[Int] = {
        var record:Map[Int,Int] = Map()
        var res:Array[Int] = Array()
        for(n <- nums1){
            var temp = record.getOrElse(n,0)
            temp += 1
            record += (n -> temp)
        }
        for(n <- nums2){
            var temp = record.getOrElse(n,0)
            if(temp != 0) {
                temp -= 1
                record += (n -> temp)
                res = res :+ n
            }
        }
        res
    }
}
```