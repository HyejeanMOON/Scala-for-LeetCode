Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair (i, j), where i and j are both numbers in the array and their absolute difference is k.

Example 1:
```
Input: [3, 1, 4, 1, 5], k = 2
Output: 2
Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).
Although we have two 1s in the input, we should only return the number of unique pairs.
```
Example 2:
```
Input:[1, 2, 3, 4, 5], k = 1
Output: 4
Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
```
Example 3:
```
Input: [1, 3, 1, 5, 4], k = 0
Output: 1
Explanation: There is one 0-diff pair in the array, (1, 1).
```
Note:  
The pairs (i, j) and (j, i) count as the same pair.
The length of the array won't exceed 10,000.
All the integers in the given input belong to the range: [-1e7, 1e7].

Difficulty:Easy  
Total Accepted:37.8K  
Total Submissions:134.2K  
Related Topics:Array, Two Pointers

### 解题思路
这道题用哈希表做的话思路非常清晰且简单。  
要分两种情况，一种是k==0，另一种是k！=0的情况。  
如果是0的情况就是把value大于1的key进行计数就可以了。  
如果是大于0的情况的话，就是对keys进行遍历找出满足情况的，进行计数就可以了。
#### Scala
```scala
object Solution {
    def findPairs(nums: Array[Int], k: Int): Int = {
        var res = 0
        var record:Map[Int,Int] = Map()
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp += 1
            record += (n -> temp)
        }
        var key = record.keySet
        if(k==0){
            for(k <- key){
                var temp = record.getOrElse(k,0)
                if(temp>1) res+=1
            }
        }else{
            var keys = key.toArray.sorted
            for(i <- 0 until keys.length-1){
                for(j <- i+1 until keys.length){
                    if(keys(j)-keys(i)==k) res+=1
                }
            }
        }
        res
    }
}
```