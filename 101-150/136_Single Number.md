Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?




### 解题思路
利用哈希表把出现过的Int的个数记录先来，并用遍历key的方法，找出个数是一的key并返回。  
- 对Map的使用还不太熟练，需要加强。
#### Scala
```scala
object Solution {
    def singleNumber(nums: Array[Int]): Int = {
        var res = 0
        var record:Map[Int,Int] = Map()
        for(n <- nums){
            if(record.getOrElse(n,0) >= 0){
                var tempCount = record.getOrElse(n,0) + 1
                record += (n -> tempCount)
            }
        }
        var keys = record.keySet
        //keys.foreach(println)
        for(k <- keys){
            //println(record.get(k))
            if(record.get(k) == Some(1)){
                return k
            }
        }
        res
    }
}
```
#### Java
```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        Map<Integer,Integer> record = new HashMap();
        int leng = nums.length;
        for(int i=0; i < leng; i++){
            if(record.containsKey(nums[i])){
                record.put(nums[i],2);
            }else{
                record.put(nums[i],1);
            }
        }
        Set<Integer> keys = record.keySet();
        for(Integer i:keys){
            if(record.get(i)==1){
                res = i;
                return res;
            }
        }
        return res;
    }
}
```