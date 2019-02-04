There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. The bricks have the same height but different width. You want to draw a vertical line from the top to the bottom and cross the least bricks.

The brick wall is represented by a list of rows. Each row is a list of integers representing the width of each brick in this row from left to right.

If your line go through the edge of a brick, then the brick is not considered as crossed. You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.

You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.

Example:
```
Input: 
[[1,2,2,1],
 [3,1,2],
 [1,3,2],
 [2,4],
 [3,1,2],
 [1,3,1,1]]
Output: 2
Explanation: 
```

Note:  
The width sum of bricks in different rows are the same and won't exceed INT_MAX.
The number of bricks in each row is in range [1,10,000]. The height of wall is in range [1,10,000]. Total number of bricks of the wall won't exceed 20,000.

Difficulty:Medium  
Total Accepted:22.6K  
Total Submissions:48.6K  
Related Topics:Hash Table

### 解题思路
用哈希表记录每层断点的频率。然后选出频率最大的那个。  
需要注意的是key中的max值需要刨除。因为那是墙的最右端。
#### Scala
```scala
object Solution {
    def leastBricks(wall: List[List[Int]]): Int = {
        var len = wall.length
        var record:Map[Int,Int] = Map()
        for(w <- wall){
            var sum = 0
            for(i <- 0 until w.length){
                sum += w(i)
                var temp = record.getOrElse(sum,0)
                temp += 1
                record += (sum -> temp)
            }
        }
        var mx = 0
        var keys = record.keySet
        for(key <- keys){
            if(key!=keys.max){
                var temp = record.getOrElse(key,0)
                mx = scala.math.max(temp,mx)
            }
            
        }
        len-mx
    }
}
```