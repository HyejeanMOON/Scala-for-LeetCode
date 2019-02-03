Given a list of 24-hour clock time points in "Hour:Minutes" format, find the minimum minutes difference between any two time points in the list.
Example 1:
```
Input: ["23:59","00:00"]
Output: 1
```
Note:  
The number of time points in the given list is at least 2 and won't exceed 20000.
The input time is legal and ranges from 00:00 to 23:59.

Difficulty:Medium  
Total Accepted:17K  
Total Submissions:36.8K  
Related Topics:String

### 解题思路
这道题给了我们一系列无序的时间点，让我们求最短的两个时间点之间的差值。那么最简单直接的办法就是给数组排序，这样时间点小的就在前面了，然后我们分别把小时和分钟提取出来，计算差值，注意唯一的特殊情况就是第一个和末尾的时间点进行比较，第一个时间点需要加上24小时再做差值。
#### Scala
```scala
object Solution {
    def findMinDifference(timePoints: List[String]): Int = {
        var res = scala.Int.MaxValue
        var len = timePoints.length
        var timePoint = timePoints.sorted
        //timePoint.foreach(println)
        for(i <- 0 until len){
            var t1 = timePoint(i).split(":")
            var t2 = timePoint((i+1)%len).split(":")
            var h1 = (t1(0).charAt(0)-'0')*10 + (t1(0).charAt(1)-'0')
            var s1 = (t1(1).charAt(0)-'0')*10 + (t1(1).charAt(1)-'0')
            var h2 = (t2(0).charAt(0)-'0')*10 + (t2(0).charAt(1)-'0')
            var s2 = (t2(1).charAt(0)-'0')*10 + (t2(1).charAt(1)-'0')
            var diff= (h2-h1)*60+(s2-s1)
            println(diff)
            if(i==len-1) diff+=24*60
            res = scala.math.min(res,diff)  
        }
        res
    }
}
```