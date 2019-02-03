The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Now your job is to find the total Hamming distance between all pairs of the given numbers.

Example:
```
Input: 4, 14, 2

Output: 6

Explanation: In binary representation, the 4 is 0100, 14 is 1110, and 2 is 0010 (just
showing the four bits relevant in this case). So the answer will be:
HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.
Note:
Elements of the given array are in the range of 0 to 10^9
Length of the array will not exceed 10^4.
```


Difficulty:Medium  
Total Accepted:31.9K  
Total Submissions:67.2K  
Related Topics:Bit Manipulation


### 解题思路
这道题是之前那道Hamming Distance的拓展，由于有之前那道题的经验，我们知道需要用异或来求每个位上的情况，那么我们需要来找出某种规律来，比如我们看下面这个例子，4，14，2和1：

4:     0 1 0 0

14:   1 1 1 0

2:     0 0 1 0

1:     0 0 0 1

我们先看最后一列，有三个0和一个1，那么它们之间相互的汉明距离就是3，即1和其他三个0分别的距离累加，然后在看第三列，累加汉明距离为4，因为每个1都会跟两个0产生两个汉明距离，同理第二列也是4，第一列是3。我们仔细观察累计汉明距离和0跟1的个数，我们可以发现其实就是0的个数乘以1的个数，发现了这个重要的规律，那么整道题就迎刃而解了，只要统计出每一位的1的个数即可。
#### Scala
```scala
object Solution {
    def totalHammingDistance(nums: Array[Int]): Int = {
        var res = 0
        var len = nums.length
        for(i <- 0 until 32){
            var count = 0
            for(n <- nums){
                if((n & (1 << i)) == scala.math.pow(2,i)) count+=1
            }
            res += count*(len-count)
        }
        res
    }
}
```

TLE!
#### Scala
```scala
object Solution {
    def totalHammingDistance(nums: Array[Int]): Int = {
        if(nums.length==0) return 0
        var record:Array[Int] = Array()
        var len = nums.length
        for(i <- 0 until len-1){
            for(j <- i+1 until len){
                var temp = nums(i)^nums(j)
                record = record:+temp
            }
        }
        var res = 0
        for(r <- record){
            var temp = r
            while(temp>0){
                if(temp%2==1){
                    res +=1
                }
                temp/=2
            }
        }
        res
        
    }
}
```