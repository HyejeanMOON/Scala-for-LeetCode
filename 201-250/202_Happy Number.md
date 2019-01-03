Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number

12 + 92 = 82  
82 + 22 = 68  
62 + 82 = 100  
12 + 02 + 02 = 1  




### 解题思路
该题目的关键是会获得一个数中每位的数的方法。需要记住。
#### Scala
```scala
object Solution {
    def isHappy(n: Int): Boolean = {
        var res = false
        var sum = 0
        var record:Map[Int,String] = Map()
        var temp = n
        while(sum != 1){
            sum = 0
            while(temp != 0){
                sum += (temp % 10) * (temp % 10)
                temp /= 10
                
            }
            println(sum)
            if(record.getOrElse(sum,"NO") == "NO"){
                record += (sum -> "YES")
            }else{
                return false
            }
            temp = sum
        }
        res = true
        res
    }
}
```
#### Java
```java
class Solution {
    public boolean isHappy(int n) {
        boolean res = true;
        if(n==1){
            return true;
        }
        if(n==0){
            return false;
        }
        int temp = n;
        java.util.HashSet<Integer> list = new java.util.HashSet<Integer>();
        list.add(n);
        while(temp!=1){
            int sum = 0;
            while(temp>0){
                int t = temp%10;
                sum = sum + t*t;
                //System.out.println(sum);
                temp /= 10;
            }
            for(Integer i:list){
                if(i==sum){
                    return false;
                }
            }
            list.add(sum);  
            temp = sum;
        }
        return res;
    }
}
```