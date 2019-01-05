Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number, and n does not exceed 1690.

Difficulty:Medium  
Total Accepted:72.7K  
Total Submissions:218.4K  
Related Topics:Math, Dynamic Programming, Heap



### 解题思路
这道题是之前那道Ugly Number 丑陋数的延伸，这里让我们找到第n个丑陋数，还好题目中给了很多提示，基本上相当于告诉我们解法了，根据提示中的信息，我们知道丑陋数序列可以拆分为下面3个子列表：

(1) 1x2,  2x2, 2x2, 3x2, 3x2, 4x2, 5x2...  
(2) 1x3,  1x3, 2x3, 2x3, 2x3, 3x3, 3x3...  
(3) 1x5,  1x5, 1x5, 1x5, 2x5, 2x5, 2x5...  

仔细观察上述三个列表，我们可以发现每个子列表都是一个丑陋数分别乘以2,3,5，而要求的丑陋数就是从已经生成的序列中取出来的，我们每次都从三个列表中取出当前最小的那个加入序列。

这种方法就是dynamic programming。 它把反复出现的问题化简成一系列已经解决的子问题。进而降低复杂度。
#### Scala
```scala
object Solution {
    def nthUglyNumber(n: Int): Int = {
        var record = new scala.collection.mutable.ArrayBuffer[Int]()
        record = record :+ 1
        if(n == 1) return 1
        var f2 = 0
        var f3 = 0
        var f5 = 0
        while(record.size < n){
            var t2 = record(f2)*2
            var t3 = record(f3)*3
            var t5 = record(f5)*5
            var min = scala.math.min(scala.math.min(t3,t2),t5)
            record = record :+ min
            var temp = record.last
            if(temp == t2) f2+=1
            if(temp== t3) f3+=1
            if(temp== t5) f5+=1
        }
        record.last
    }
}
```




-----------

### 解题思路
只要能被2，3，5一直整除的就算是Ugly Number。所以设置一个判断Ugly Number的函数。但是这么做复杂度高，执行的结果是TLE。
#### Scala
TLE!!
```scala
object Solution {
    def nthUglyNumber(n: Int): Int = {
        var count = 1
        var max = scala.Int.MaxValue
        if(n <=6) return n
        for(i <-  2 until max){
            if(isUgly(i)) count+=1
            if(count==n) return i
        }
        0
    }
    def isUgly(n:Int):Boolean={
        var temp = n
        while(temp>1){
            if(temp%2==0) temp/=2
            else if(temp%3==0) temp/=3
            else if(temp%5==0) temp/=5
            else return false
            if(temp==1) return true
        }
        false
    }
}
```