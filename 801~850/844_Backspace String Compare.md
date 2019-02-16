Given two strings S and T, return if they are equal when both are typed into empty text editors. # means a backspace character.

Example 1:
```
Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
```
Example 2:
```
Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
```
Example 3:
```
Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
```
Example 4:
```
Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
```
Note:

- 1 <= S.length <= 200
- 1 <= T.length <= 200
S and T only contain lowercase letters and '#' characters.  

Follow up:

Can you solve it in O(N) time and O(1) space?
 
Difficulty:Easy  
Total Accepted:8.9K  
Total Submissions:19.5K  
Related Topics:Two Pointers, Stack

### 解题思路
#### Scala
```scala
object Solution {
    def backspaceCompare(S: String, T: String): Boolean = {
        var res1 = back(S)
        var res2 = back(T)
        if(res1==res2) return true
        false
    }
    def back(S:String):String={
        var stack = new scala.collection.mutable.Stack[Char]
        for(s <- S){
            if(s.toString!="#") stack.push(s)
            else {
                if(!stack.isEmpty) stack.pop
            }
        }
        stack.toString
    }
}
```
