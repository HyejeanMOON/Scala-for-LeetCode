Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

Example 1:
```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
```
The second 1's next greater number needs to search circularly, which is also 2.
Note: The length of given array won't exceed 10000.

Difficulty:Medium  
Total Accepted:28K  
Total Submissions:58.3K  
Related Topics:Stack

### 解题思路
我们可以使用栈来进行优化上面的算法，我们遍历两倍的数组，然后还是坐标i对n取余，取出数字，如果此时栈不为空，且栈顶元素小于当前数字，说明当前数字就是栈顶元素的右边第一个较大数，那么建立二者的映射，并且去除当前栈顶元素，最后如果i小于n，则把i压入栈。因为res的长度必须是n，超过n的部分我们只是为了给之前栈中的数字找较大值，所以不能压入栈。  
** 还没有完全理解。
#### Scala
```scala
object Solution {
    def nextGreaterElements(nums: Array[Int]): Array[Int] = {
        var len = nums.length
        var res = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 until len){
            res = res :+ -1
        }      
        var st = new scala.collection.mutable.Stack[Int]()
        for(i <- 0 until 2*len){
            var num = nums(i%len)
            while(!st.isEmpty && nums(st.top)<num){
                res(st.top)= num
                println(i)
                println(num)
                println()
                st.pop
            }
            if(i<len) st.push(i)
        }
        res.toArray
    }
}
```