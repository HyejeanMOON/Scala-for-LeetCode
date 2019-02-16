We are given two strings, A and B.

A shift on A consists of taking string A and moving the leftmost character to the rightmost position. For example, if A = 'abcde', then it will be 'bcdea' after one shift on A. Return True if and only if A can become B after some number of shifts on A.

Example 1:
```
Input: A = 'abcde', B = 'cdeab'
Output: true
```
Example 2:
```
Input: A = 'abcde', B = 'abced'
Output: false
```
Note:

A and B will have length at most 100.

Difficulty:Easy  
Total Accepted:12K   
Total Submissions:22.3K

### 解题思路
#### Scala
```Scala
object Solution {
    def rotateString(A: String, B: String): Boolean = {
        var temp = A+A+A
        if(A.length!=B.length) return false
        if(temp.contains(B)) return true
        false
    }
}
```
