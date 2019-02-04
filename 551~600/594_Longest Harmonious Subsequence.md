We define a harmonious array is an array where the difference between its maximum value and its minimum value is exactly 1.

Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.

Example 1:
```
Input: [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].
```
Note: The length of the input array will not exceed 20,000.

Difficulty:Easy  
Total Accepted:21.2K  
Total Submissions:51.6K  
Related Topics:Hash Table

### 解题思路
用map记录出现的次数就可以解决。总体来说很简单。
#### Scala
```scala
object Solution {
    def findLHS(nums: Array[Int]): Int = {
        var res:Array[Int] = Array()
        var record:Map[Int,Int] = Map()
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp += 1
            record += (n -> temp)
        }
        var key = record.keySet.toArray.sorted
        var mx = 0
        for(i <- 1 until key.length){
            if(key(i)-key(i-1)==1){
                var v1 = record.getOrElse(key(i-1),0)
                var v2 = record.getOrElse(key(i),0)
                var count = v1+v2
                if(mx<count) mx = count
            }
        }
        mx
        
    }
}
```