Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

Difficulty:Easy  
Total Accepted:231.8K  
Total Submissions:584K  
Related Topics:Array, Math

### 解题思路
将一个数字的每个位上的数字分别存到一个一维向量中，最高位在最开头，我们需要给这个数字加一，即在末尾数字加一，如果末尾数字是9，那么则会有进位问题，而如果前面位上的数字仍为9，则需要继续向前进位。具体算法如下：首先判断最后一位是否为9，若不是，直接加一返回，若是，则该位赋0，再继续查前一位，同样的方法，知道查完第一位。如果第一位原本为9，加一后会产生新的一位，那么最后要做的是，查运算完的第一位是否为0，如果是，则在最前头加一个1。
#### Scala
```scala
object Solution {
    def plusOne(digits: Array[Int]): Array[Int] = {
        var temp = new scala.collection.mutable.ArrayBuffer[Int]()
        var len = digits.length
        var res:Array[Int] = Array()
        var result:Array[Int] = Array()
        for(i <- 0 until len){
            temp = temp :+ digits(i)
        }
        for(i <- 0 until len){
            if(temp(len-i-1)==9) temp(len-i-1) = 0
            else {
                temp(len-i-1) += 1
                return temp.toArray
            } 
        }
        if(temp.head==0) temp.insert(0,1)
        temp.toArray
    }
}
```