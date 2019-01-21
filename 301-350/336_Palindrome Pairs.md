Given a list of unique words, find all pairs of distinct indices (i, j) in the given list, so that the concatenation of the two words, i.e. words[i] + words[j] is a palindrome.

Example 1:
```
Given words = ["bat", "tab", "cat"]
Return [[0, 1], [1, 0]]
The palindromes are ["battab", "tabbat"]
```
Example 2:
```
Given words = ["abcd", "dcba", "lls", "s", "sssll"]
Return [[0, 1], [1, 0], [3, 2], [2, 4]]
The palindromes are ["dcbaabcd", "abcddcba", "slls", "llssssll"]
```

### 解题思路
 Time Limit Exceeded !
#### Java
```java
class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        Set<List<Integer>> res = new HashSet<List<Integer>>();
        Map<String,Integer> record = new HashMap<String,Integer>();
        List<Integer> lenRecord = new ArrayList<Integer>();
        for(int i=0; i<words.length; i++){
            int w = words[i].length();
            lenRecord.add(w);
            record.put(words[i],i);
        }
        for(int i=0; i<words.length; i++){
            int len = words[i].length();
            for(int j=0; j < lenRecord.size(); j++){
                if(len>=lenRecord.get(j) && i!=j){
                    String lr = words[i]+words[j];
                    String rl = words[j]+words[i];
                    if(isValid(lr)){
                        List<Integer> temp = new ArrayList<Integer>();
                        temp.add(i);
                        temp.add(j);
                        res.add(temp);
                    }
                    if(isValid(rl)) {
                        List<Integer> temp = new ArrayList<Integer>();
                        temp.add(j);
                        temp.add(i);
                        res.add(temp);
                    }
                }
            }
        }
        return new ArrayList(res);
            
    }
    public boolean isValid(String word){
        int left = 0;
        int right = word.length()-1;
        while(left<right){
            char l = word.charAt(left);
            char r = word.charAt(right);
            if(l!=r) return false;
            left += 1;
            right -= 1;
        }
        return true;
    }
}
```
#### Scala
 Time Limit Exceeded !
```scala
object Solution {
    def palindromePairs(words: Array[String]): List[List[Int]] = {
        var res:Set[List[Int]] = Set()
        var record:Map[String,Int] = Map()
        var lengthRecord:List[Int] = List()
        for(i <- 0 until words.length){
            record += (words(i) -> i)
            lengthRecord = lengthRecord :+ words(i).length
        }
        for(i <- 0 until words.length){
            var len = words(i).length
            for(j <- 0 until lengthRecord.length){
                if(len>=lengthRecord(j) && i!=j){
                    var lr:String = words(i)+words(j)
                    var rl:String = words(j)+words(i)
                    if(isValid(lr)) res = res + List(i,j)
                    if(isValid(rl)) res = res + List(j,i)
                }
            }
        }
        res.toList
    }
    def isValid(word:String):Boolean={
        var left = 0
        var right = word.length-1
        while(left<right){
            if(word.charAt(left) != word.charAt(right)) return false
            left += 1
            right -= 1
        }
        true
    }
}
```