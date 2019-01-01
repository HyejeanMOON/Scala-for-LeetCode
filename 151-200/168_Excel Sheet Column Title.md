Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```


### 解题思路
#### Scala
```scala
object Solution {
    def convertToTitle(n: Int): String = {
        var res = ""
        var temp = n
        while(temp != 0){
            if((temp % 26) == 0){
                res = res + 'Z'
                temp -= 26
            }else{
                res += (temp % 26 - 1 + 'A').toChar
                temp -= temp % 26
            }
            temp /= 26
        }
        res = res.reverse
        res
    }
}
```