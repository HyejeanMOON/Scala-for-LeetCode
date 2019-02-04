Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

Example 1:
```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
Output: ["Shogun"]
Explanation: The only restaurant they both like is "Shogun".
```
Example 2:
```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
Output: ["Shogun"]
Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).
```
Note:  
The length of both lists will be in the range of [1, 1000].
The length of strings in both lists will be in the range of [1, 30].
The index is starting from 0 to the list length minus 1.
No duplicates in both lists.

### 解题思路
遍历数组，用图记录。
#### Scala
```scala
object Solution {
    def findRestaurant(list1: Array[String], list2: Array[String]): Array[String] = {
        var leng1 = list1.length
        var leng2 = list2.length
        var res = leng1+leng2
        var record:Map[String,Int] = Map()
        var tempResult = ""
        for(i <- 0 until leng1){
            record += (list1(i) -> i)
        }
        var result:Array[String] = Array()
        for(j <- 0 until leng2){
            var temp = record.getOrElse(list2(j),-1)
            var flag = true
            if(temp+j < res && temp != -1){
                res = temp + j
                tempResult = list2(j)
                result = Array()
                result = result :+ tempResult
                flag = false
            }
            if(temp+j == res && temp != -1 && flag){
                //println(list2(j))
                result = result :+ list2(j)
            }
        }
        result 
    }
}
```