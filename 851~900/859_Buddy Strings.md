Given two strings A and B of lowercase letters, return true if and only if we can swap two letters in A so that the result equals B.

 

Example 1:
```
Input: A = "ab", B = "ba"
Output: true
```
Example 2:
```
Input: A = "ab", B = "ab"
Output: false
```
Example 3:
```
Input: A = "aa", B = "aa"
Output: true
```
Example 4:
```
Input: A = "aaaaaaabc", B = "aaaaaaacb"
Output: true
```
Example 5:
```
Input: A = "", B = "aa"
Output: false
```

Note:

- 0 <= A.length <= 20000
- 0 <= B.length <= 20000
- A and B consist only of lowercase letters.


Difficulty:Easy  
Total Accepted:6.3K  
Total Submissions:24K  
Related Topics:String

### 解题思路
该题的要求是必须在A中交换两个char，使其和B一样。  
这样就有两种情况。  
一种是，有两个char它们之间只是位置不一样。  
另一种是A和B完全一样，这种情况只要在A中有两个以上的Char就可以认为是true。（也是使用map的原因）
#### Scala
```scala
object Solution {
    def buddyStrings(A: String, B: String): Boolean = {
        var lenA = A.length
        var lenB = B.length
        var record:List[Char] = List()
        var map:Map[Char,Int] = Map()
        if(lenA!=lenB) return false
        for(i <- 0 until lenA){
            var a = A.charAt(i)
            var b = B.charAt(i)
            if(a!=b) {
                record=record:+a
                record=record:+b
            }else{
                var temp = map.getOrElse(a,0)
                temp+=1
                map+=(a -> temp)
            }
            if(record.length>4) return false
        }
        if(A.equals(B)){
            var v = map.values
            for(vv <- v){
                if(vv>=2) return true
            }
        }
        if(record.length==2) return false
        else if(record.length==4) {
            if(record(0)==record(3) && record(1)==record(2)) return true
            else false
        }
        false
    }
}
```


Java
```java
**Easy,
String.**

Given two strings A and B of lowercase letters, return true if and only if we can swap two letters in A so that the result equals B.

 

Example 1:
```
Input: A = "ab", B = "ba"
Output: true
```
Example 2:
```
Input: A = "ab", B = "ab"
Output: false
```
Example 3:
```
Input: A = "aa", B = "aa"
Output: true
```
Example 4:
```
Input: A = "aaaaaaabc", B = "aaaaaaacb"
Output: true
```
Example 5:
```
Input: A = "", B = "aa"
Output: false
```

Note:
```
0 <= A.length <= 20000
0 <= B.length <= 20000
A and B consist only of lowercase letters.
```

#### 解法

这里用的是比较笨的方法。
如果A和B有不同的就记录下来，如果不同处超过2则false，
如果记录下来的A和B不同之处相同则true。
这里还需要注意两个string是否相同，如果相同又需要分两种情况。
一是里面有相同的字符，
另一个是没有的情况。

java
```java
class Solution {
    public boolean buddyStrings(String A, String B) {
        int lenA = A.length();
        int lenB = B.length();
        if(lenA!=lenB) return false;
        if(A.equals(B)){
            Map record = new HashMap();
            for(int i=0; i<lenA; i++){
                if(record.get(A.charAt(i))==null) record.put(A.charAt(i),1);
                else return true;
            }
            return false;
        }
        char[] recordA = new char[2];
        char[] recordB = new char[2];
        int position=0;
        int count = 2;
        while(position<lenA && count >0){
            if(A.charAt(position)==B.charAt(position)) position++;
            else {
                recordA[count-1] = A.charAt(position);
                recordB[count-1] = B.charAt(position);
                position++;
                count--;
            }
        }
        if(position!=lenA) return false;
        Arrays.sort(recordA);
        Arrays.sort(recordB);
        for(int i=0; i<2; i++){
            if(recordA[i]!=recordB[i]) return false;
        }
        return true;
    }
}
```
```