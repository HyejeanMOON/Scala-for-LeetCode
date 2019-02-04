Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example 1:
```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```
Note:   
In the string, each word is separated by single space and there will not be any extra space in the string.




### 解题思路
根据空格把字符串进行分割。  
然后把每个数组内的字符进行倒置。  
然后进行拼接就可以了。  
#### Scala
```scala
xobject Solution {
    def reverseWords(s: String): String = {
        var result:String = ""
        var sSplit = s.split(" ")
        for(i <- 0 until sSplit.length){
            var temp = sSplit(i).reverse
            result = result + " " + temp
        }
        result = result.trim
        result
    }
}
```

#### Java
```java
class Solution {
    public String reverseWords(String s) {
        String[] temp = s.split(" ");
        int leng = temp.length;
        String res = "";
        for(int i=0; i<leng; i++){
            String t = new StringBuilder(temp[i]).reverse().toString();
            res = res + t + " ";
        }
        res = res.trim();
        return res;   
    }
}
```