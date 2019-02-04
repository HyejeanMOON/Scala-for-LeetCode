Given an integer array with even length, where different numbers in this array represent different kinds of candies. Each number means one candy of the corresponding kind. You need to distribute these candies equally in number to brother and sister. Return the maximum number of kinds of candies the sister could gain.  

Example 1:
```
Input: candies = [1,1,2,2,3,3]
Output: 3
Explanation:
There are three different kinds of candies (1, 2 and 3), and two candies for each kind.
Optimal distribution: The sister has candies [1,2,3] and the brother has candies [1,2,3], too. 
The sister has three different kinds of candies. 
```
Example 2:
```
Input: candies = [1,1,2,3]
Output: 2
Explanation: For example, the sister has candies [2,3] and the brother has candies [1,1]. 
The sister has two different kinds of candies, the brother has only one kind of candies. 
```
Note:

The length of the given array is in range [2, 10,000], and will be even.
The number in given array is in range [-100,000, 100,000].


ifficulty:Easy  
Total Accepted:45.8K  
Total Submissions:78.7K  
Related Topics:Hash Table

### 解题思路
该题要用哈希表。  
首先是要用哈希表进行记录。  
然后分两种情况，  
第一种是如果糖果种类数小于糖果总数的一半，则返回糖果种类数。  
第二种是如果糖果种类数大于糖果总数的一半，则返回糖果总数的一半。
#### Scala
```scala
object Solution {
    def distributeCandies(candies: Array[Int]): Int = {
        var res = 0
        var len = candies.length
        var record:Map[Int,Int] = Map()
        for(c <- candies){
            var temp = record.getOrElse(c,0)
            temp += 1
            record += (c -> temp)
        }
        var keys = record.keySet
        if(keys.toArray.length<=len/2) res=keys.toArray.length
        else if(keys.toArray.length>len/2) res=len/2
        res
    }
}
```