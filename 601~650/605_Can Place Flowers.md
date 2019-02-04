Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.

Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.

Example 1:
```
Input: flowerbed = [1,0,0,0,1], n = 1
Output: True
```
Example 2:
```
Input: flowerbed = [1,0,0,0,1], n = 2
Output: False
```
Note:  
The input array won't violate no-adjacent-flowers rule.  
The input array size is in the range of [1, 20000].  
n is a non-negative integer which won't exceed the input array size.

### 解题思路
首先判断flowerbed是否长度是一且数据为0，  
在结算左手边是否有零并计算个数，此时能种植的数为canCount = lefCount/2。  
然后在计算右手边是否有零并计算个数，能种植的数为canCount = right/2。  
最后再计算中间部分。中间部分的能种植的数,  
偶数时 canCount = zero / 2 - 1  
奇数时 canCount = (zero-1) / 2

#### Scala
```scala
object Solution {
    def canPlaceFlowers(flowerbed: Array[Int], n: Int): Boolean = {
        var result = false
        var isEnd = false
        var zeroCount = 0
        var canCount = 0
        var leftCount = 0
        var rightCount = 0
        var flag = true
        var leng = flowerbed.length
        if(leng == 1 && flowerbed(0) == 0 ){
            canCount += 1
            isEnd = true
        }
        if(leng ==1 && flowerbed(0) != 0 ) {
            
            isEnd = true
        }
        if(flowerbed(0) == 0 && !isEnd){
            leftCount += 1
            for(f <- 1 until flowerbed.length if flag){
                if(flowerbed(f) == 0){
                    leftCount += 1
                    
                }else{
                    flag = false
                }
            }
            
            if(leftCount == leng){
                canCount = canCount + (leftCount+1)/2
                isEnd = true
            }else{
                canCount = canCount + leftCount/2
            }   
            if(leftCount!=0 ){
                leftCount -= 1
            }
        }
        flag = true
        
        if(flowerbed(leng-1) == 0 && !isEnd){
            rightCount += 1
            for(f <- 1 to leng-leftCount if flag){
                
                if(flowerbed(leng-1-f) == 0){
                    rightCount += 1
                }else{
                    flag = false
                }
            }
            println(rightCount)
            canCount = canCount + rightCount/2
        }
        
        if(!isEnd){
            for(f <- leftCount until leng-rightCount){
                if(flowerbed(f) == 0){
                    
                    zeroCount += 1
                    
                }else{
                    if(zeroCount > 2){
                        if(zeroCount % 2 == 1){
                            canCount = canCount + (zeroCount-1)/2
                        }else{
                            canCount = canCount + (zeroCount-2)/2
                        }
                    }
                    zeroCount = 0
                }
            }
        }
        //println(canCount)
        if(canCount >= n){
            result = true
        }else{
            result = false
        }
        result
    }
}
```

#### Java
```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int leng = flowerbed.length;
        if(leng == 1){
            if(flowerbed[0] == 0 && n <= 1) return true;
            else if(flowerbed[0] == 1 && n ==0) return true; 
            else return false;
        }
        int countLeft = 0;
        int countRight = 0;
        for(int i=0; i< leng; i++){
            if(flowerbed[i] == 0){
                countLeft += 1;
            }else{
                break;
            }
        }
        //为解决全是零的情况。
        if(countLeft == leng) return (countLeft+1)/2 >= n ;
        for(int i=leng-1; i>=0; i-- ){
            if(flowerbed[i] == 0){
                countRight += 1;
            }else{
                break;
            }
        }
        int res = countLeft/2 + countRight/2;
        int countZero = 0;
        for(int i=countLeft; i<leng-countRight; i++){
            if(flowerbed[i] == 0){
                countZero += 1;
            }else{
                res += (countZero-1)/2;
                countZero = 0;
            }
        }
        System.out.println(res);
        return res >= n;
    }
}
```