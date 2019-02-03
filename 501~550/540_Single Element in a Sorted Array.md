Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.

Example 1:
```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```
Example 2:
```
Input: [3,3,7,7,10,11,11]
Output: 10
```
Note:  
Your solution should run in O(log n) time and O(1) space.

Difficulty:Medium  
Total Accepted:29.5K  
Total Submissions:52.9K  

### 解题思路
这道题的要求是从数组中找出只出现一次的数，需要在O(logn)时间和O(1)的空间完成。所以遍历需要用while，而不是用for。每两个数为一组。如果第一个数和第二数不一样则返回第一个数。遍历到最后只剩最后一个数，那就返回那个数。
#### Scala
```scala
object Solution {
    def singleNonDuplicate(nums: Array[Int]): Int = {
        var len = nums.length
        if(len==1) return nums(0)
        var count = 0
        while(count<len){
            if(count==len-1) return nums(count)
            if(nums(count)!=nums(count+1)) return nums(count)
            count+=2
        }
        count
    }
}
```