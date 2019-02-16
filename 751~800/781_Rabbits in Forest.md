
In a forest, each rabbit has some color. Some subset of rabbits (possibly all of them) tell you how many other rabbits have the same color as them. Those answers are placed in an array.

Return the minimum number of rabbits that could be in the forest.

Examples:
```
Input: answers = [1, 1, 2]
Output: 5
Explanation:
The two rabbits that answered "1" could both be the same color, say red.
The rabbit than answered "2" can't be red or the answers would be inconsistent.
Say the rabbit that answered "2" was blue.
Then there should be 2 other blue rabbits in the forest that didn't answer into the array.
The smallest possible number of rabbits in the forest is therefore 5: 3 that answered plus 2 that didn't.

Input: answers = [10, 10, 10]
Output: 11

Input: answers = []
Output: 0
```
Note:

answers will have length at most 1000.
Each answers[i] will be an integer in the range [0, 999].

Difficulty:Medium  
Total Accepted:4.8K  
Total Submissions:9.8K  
Related Topics:Hash Table, Math

### 解题思路
根据题意， 首先要建立一个哈希表，记录每个数字出现的次数。   
如果key的值大于等于value，则需加key+1，  
如果key的值小于value，则求出相除值和余值，相应的想加。  
key等于0是一个特殊情况，表示该颜色只有我一个人，所以只要相加value值就可以了。
#### Scala
```scala
object Solution {
    def numRabbits(answers: Array[Int]): Int = {
        if(answers.isEmpty) return 0
        var len = answers.length
        var record:Map[Int,Int] = Map()
        for(a <- answers){
            var temp = record.getOrElse(a,0)
            temp += 1
            record += (a -> temp)
        }
        var keys = record.keySet
        var sum = 0
        for(key <- keys){
            var v = record.getOrElse(key,0)
            if(key==0) sum += v
            //else if((key+1==v)) sum += key+1
            else if(v<=key+1) sum += key+1
            else {
                var v1 = v/(key+1)
                var v2 = v%(key+1)
                if(v2==0){
                    sum += v1*(key+1)
                }else{
                    sum += (v1+1)*(key+1)
                }
            }
        }
        sum
    }
}
```