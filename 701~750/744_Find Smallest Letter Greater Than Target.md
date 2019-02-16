Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = ['a', 'b'], the answer is 'a'.

Examples:
```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```
Note:  
letters has a length in range [2, 10000].
letters consists of lowercase letters, and contains at least 2 unique letters.
target is a lowercase letter.

Difficulty:Easy  
Total Accepted:13K  
Total Submissions:29.1K  
Related Topics:Binary Search

### 解题思路
把特殊情况单独分解出来就可以了。
#### Scala
```scala
object Solution {
    def nextGreatestLetter(letters: Array[Char], target: Char): Char = {
        var len = letters.length
        if(letters(0).toInt > target.toInt  || letters(len-1).toInt <= target.toInt) return letters(0)
        for(i <- 1 until len){
            if(letters(i-1).toInt<=target.toInt && letters(i).toInt>target.toInt) return letters(i)
        }
        letters(0)
    }
}
```
### 解法二
可以用二分法。因为给定的数组是已经排好序的。
#### Scala
```scala
object Solution {
    def nextGreatestLetter(letters: Array[Char], target: Char): Char = {
        var len = letters.length
        if(target.toInt>=letters(len-1)) return letters(0)
        var left = 0
        var right = len
        while(left<right){
            var mid = left + (right-left)/2
            if(target.toInt>=letters(mid)) left = mid+1
            else right = mid
        }
        letters(right)
    }
}
```