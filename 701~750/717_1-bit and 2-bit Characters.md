We have two special characters. The first character can be represented by one bit 0. The second character can be represented by two bits (10 or 11).

Now given a string represented by several bits. Return whether the last character must be a one-bit character or not. The given string will always end with a zero.

Example 1:
```
Input: 
bits = [1, 0, 0]
Output: True
Explanation: 
The only way to decode it is two-bit character and one-bit character. So the last character is one-bit character.
```
Example 2:
```
Input: 
bits = [1, 1, 1, 0]
Output: False
Explanation: 
The only way to decode it is two-bit character and two-bit character. So the last character is NOT one-bit character.
```
Note:

- 1 <= len(bits) <= 1000.  
-  bits[i] is always 0 or 1.



### 解题思路
遍历数组，当遇到零是跳过一位，当遇到1时跳过两位。判断最后是否留下一位的0。  
判断条件时 i == (leng-1)
#### Scala
```
object Solution {
    def isOneBitCharacter(bits: Array[Int]): Boolean = {
        var leng = bits.length
        var i = 0
        while(i < leng-1){
            if(bits(i) == 0){
                i += 1
            }else{
                i += 2
            }
        }
        var result = i == (leng-1)
        result
    }
}
```