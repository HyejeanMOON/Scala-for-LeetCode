We are given two sentences A and B.  (A sentence is a string of space separated words.  Each word consists only of lowercase letters.)

A word is uncommon if it appears exactly once in one of the sentences, and does not appear in the other sentence.

Return a list of all uncommon words. 

You may return the list in any order.

 

Example 1:
```
Input: A = "this apple is sweet", B = "this apple is sour"
Output: ["sweet","sour"]
```
Example 2:
```
Input: A = "apple apple", B = "banana"
Output: ["banana"]
```

Note:

- 0 <= A.length <= 200
- 0 <= B.length <= 200
- A and B both contain only spaces and lowercase letters.


Difficulty:Easy  
Total Accepted:2.3K  
Total Submissions:3.7K  
Related Topics:Hash Table

### 解题思路
#### Scala
```Scala
object Solution {
    def uncommonFromSentences(A: String, B: String): Array[String] = {
        var record:Map[String,Int] = Map()
        var a = A.split(" ")
        var b = B.split(" ")
        for(aa <- a){
            var temp = record.getOrElse(aa,0)
            temp+=1
            record+=(aa -> temp)
        }
        for(bb <- b){
            var temp = record.getOrElse(bb,0)
            temp+=1
            record+=(bb -> temp)
        }
        var keys = record.keySet
        var res:Array[String] = Array()
        for(key <- keys){
            var temp = record.getOrElse(key,0)
            if(temp==1) res=res:+key
        }
        res
    }
}
```