In a string S of lowercase letters, these letters form consecutive groups of the same character.

For example, a string like S = "abbxxxxzyy" has the groups "a", "bb", "xxxx", "z" and "yy".

Call a group large if it has 3 or more characters.  We would like the starting and ending positions of every large group.

The final answer should be in lexicographic order.

 

Example 1:
```
Input: "abbxxxxzzy"
Output: [[3,6]]
Explanation: "xxxx" is the single large group with starting  3 and ending positions 6.
```
Example 2:
```
Input: "abc"
Output: []
Explanation: We have "a","b" and "c" but no large group.
```
Example 3:
```
Input: "abcdddeeeeaabbbcd"
Output: [[3,5],[6,9],[12,14]]
``` 

Note:  1 <= S.length <= 1000

Difficulty:Easy  
Total Accepted:9.5K  
Total Submissions:20.3K  
Related Topics:Array

### 解题思路
#### Scala
```scala
object Solution {
    def largeGroupPositions(S: String): List[List[Int]] = {
        if(S=="") return List()
        var res:List[List[Int]] = List()
        var out:List[Int] = List()
        var temp:Char = '0'
        var count =0
        for(i <- 0 until S.length){
            var s = S.charAt(i)
            if(s!=temp) {
                temp = s
                if(count>=3){
                    out=out:+(i-1)
                    res=res:+out
                }
                count = 1
                out=List()
                out=out:+i
            }else count+=1
        }
        if(count>=3){
            out=out:+(S.length-1)
            res=res:+out
        }
        res
    }
}
```