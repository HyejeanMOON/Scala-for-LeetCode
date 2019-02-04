Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

Example 1:
```
Input: [1, 2, 2, 3, 1]
Output: 2
Explanation: 
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.
```
Example 2:
```
Input: [1,2,2,3,1,4,2]
Output: 6
```
Note:  
nums.length will be between 1 and 50,000.   
nums[i] will be an integer between 0 and 49,999.



#### Scala
首先用map记录每个数字出来的次数。然后用indexOf和lastIndexOf的api计算第一次和最后一次出现的位置。然后用last-first+1就可以了。
```Scala
object Solution {
    def findShortestSubArray(nums: Array[Int]): Int = {
        var record:Map[Int,Int] = Map()
        for(n <- nums){
            var temp = record.getOrElse(n,0)
            temp += 1
            record += (n -> temp)
        }
        var keys = record.keySet
        var maxValue = 0
        var recordNum:Array[Int] = Array()
        for(k <- keys){
            var temp = record.getOrElse(k,0)
            if(temp > maxValue){
                maxValue = temp
                recordNum = Array()
                recordNum = recordNum :+ k
            }
            if(temp == maxValue){
                recordNum = recordNum :+ k
            }
        }
        var res = nums.length
        for(r <- recordNum){
            var first = nums.indexOf(r)
            var last = nums.lastIndexOf(r)
            var temp = last - first + 1
            if(temp < res){
                res = temp
            }
        }     
        res
    }
}
```