Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

### 解题思路
这是到求众数的问题，有很多种解法，其中我感觉比较好的有两种，一种是用哈希表，这种方法需要O(n)的时间和空间，另一种是用一种叫摩尔投票法 Moore Voting，需要O(n)的时间和O(1)的空间，比前一种方法更好。这种投票法先将第一个数字假设为众数，然后把计数器设为1，比较下一个数和此数是否相等，若相等则计数器加一，反之减一。然后看此时计数器的值，若为零，则将当前值设为候选众数。以此类推直到遍历完整个数组，当前候选众数即为该数组的众数。不仔细弄懂摩尔投票法的精髓的话，过一阵子还是会忘记的，首先要明确的是这个叼炸天的方法是有前提的，就是数组中一定要有众数的存在才能使用，下面我们来看本算法的思路，这是一种先假设候选者，然后再进行验证的算法。我们现将数组中的第一个数假设为众数，然后进行统计其出现的次数，如果遇到同样的数，则计数器自增1，否则计数器自减1，如果计数器减到了0，则更换当前数字为候选者。这是一个很巧妙的设定，也是本算法的精髓所在，为啥遇到不同的要计数器减1呢，为啥减到0了又要更换候选者呢？首先是有那个强大的前提存在，一定会有一个出现超过半数的数字存在，那么如果计数器减到0了话，说明目前不是候选者数字的个数已经跟候选者的出现个数相同了，那么这个候选者已经很weak，不一定能出现超过半数，我们选择更换当前的候选者。那有可能你会有疑问，那万一后面又大量的出现了之前的候选者怎么办，不需要担心，如果之前的候选者在后面大量出现的话，其又会重新变为候选者，直到最终验证成为正确的众数，佩服算法的提出者啊。
### Scala
```scala
object Solution {
    def majorityElement(nums: Array[Int]): Int = {
        var res = 0
        var cnt = 0
        for(n <- nums){
            if(cnt==0){
                res=n
                cnt+=1
            }else if(n==res) {
                cnt+=1
            }
            else cnt-=1
            println("res " + res)
            println("cnt " + cnt)
            println()
        }
        res
    }
}
```


---

遍历数组，并用map记录。
#### Scala
```scala
object Solution {
    def majorityElement(nums: Array[Int]): Int = {
        var leng = nums.length
        if(leng == 0) return 0
        var record:Map[Int,Int] = Map()
        for(i <- 0 until leng){
            var temp = record.getOrElse(nums(i),0)
            temp += 1
            record += (nums(i) -> temp)
        }
        var keys = record.keySet
        for(k <- keys){
            if(record.getOrElse(k,0) > leng/2){
                return k
            }
        }
        0
    }
}
```