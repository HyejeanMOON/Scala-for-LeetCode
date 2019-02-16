Implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.

 

Example 1:
```
Input: "Hello"
Output: "hello"
```
Example 2:
```
Input: "here"
Output: "here"
```
Example 3:
```
Input: "LOVELY"
Output: "lovely"
```

Difficulty:Easy  
Total Accepted:6.5K  
Total Submissions:8.6K  
Related Topics:String

### 解题思路
#### Scala
```Scala
object Solution {
    def toLowerCase(str: String): String = {
        var res = ""
        for(s <- str){
            if(s.isUpper) res+=s.toString.toLowerCase
            else res+=s
        }
        res
    }
}
```