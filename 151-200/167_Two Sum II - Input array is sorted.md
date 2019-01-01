Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution and you may not use the same element twice.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2

### 解题思路
设置两个循环，一个是作为基准，计算出差值。  
然后再另一个循环中搜索。


#### Scala
```scala
object Solution {
    def twoSum(numbers: Array[Int], target: Int): Array[Int] = {
        var result:Array[Int] = Array()
        for(i <- 0 until numbers.length-1){
            var temp = target - numbers(i)
            for(j <- i+1 until numbers.length){
                if(numbers(j) == temp){
                    result = result :+ (i+1)
                    result = result :+ (j+1)
                }
            }
        }
        result
    }
}
```