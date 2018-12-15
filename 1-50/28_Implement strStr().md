Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:
```
Input: haystack = "hello", needle = "ll"
Output: 2
```
Example 2:
```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

### 解题思路
如果needle为空返回0，如果needle长度大于haystack则返回-1。
遍历字符串的过程中，如果剩余长度没有needle的字符串长，则没有匹配成功所以return -1。  
遍历的过程中有一个char没有匹配成功，跳出循环。
#### Scala
```
object Solution {
    def strStr(haystack: String, needle: String): Int = {
        var hLeng = haystack.length
        var nLeng = needle.length
        var s = hLeng - nLeng
        if(s < 0){
            return -1
        }else if(s == 0){
            if(haystack.toString == needle.toString){
                return 0
            }else{
                return -1
            }
        }else if(nLeng == 0){
            return 0
        }
        else{
            for(i <- 0 to s){
                var flag = false
                if(haystack.charAt(i).toString == needle.charAt(0).toString){
                    for(j <- 1 until nLeng if !flag){
                        if(haystack.charAt(i+j).toString != needle.charAt(j).toString){
                            flag = true
                        }
                    }
                    if(!flag){
                        return i
                    }
                }
            }
            return -1
        }
    }
}
```