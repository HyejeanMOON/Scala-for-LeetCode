Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to the original place.

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are R (Right), L (Left), U (Up) and D (down). The output should be true or false representing whether the robot makes a circle.

Example 1:
```
Input: "UD"
Output: true
```
Example 2:
```
Input: "LL"
Output: false
```


### 解题思路

#### Scala
```
object Solution {
    def judgeCircle(moves: String): Boolean = {
        var lr = 0
        var ud = 0
        for(s <- moves){
            if(s.toString == "U") ud += 1
            if(s.toString == "D") ud -= 1
            if(s.toString == "L") lr -= 1
            if(s.toString == "R") lr += 1
        }
        var result = false
        if(lr == 0 && ud == 0){
            result = true
        }
        result
    }
}
```