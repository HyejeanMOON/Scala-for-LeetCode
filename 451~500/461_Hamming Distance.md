The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

Note:  
0 ≤ x, y < 231.

Example:
```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
```
The above arrows point to positions where the corresponding bits are different.


### 解题思路
#### Scala
```scala
object Solution {
    def hammingDistance(x: Int, y: Int): Int = {
        var res1:String = ""
        var res2:String = ""
        var temp1 = x
        var temp2 = y
        var res = 0
        //换成2进制
        while(temp1 > 0){
            res1 += (temp1 % 2).toString
            temp1 /= 2
        }
        while(temp2 > 0){
            res2 += (temp2 % 2).toString
            temp2 /= 2
        }
        var leng1 = res1.length
        var leng2 = res2.length
        //填补空位，使其位数一样
        if(leng1 > leng2){
            var temp = leng1 - leng2
            for(i <- 0 until temp){
                res2 += 0
            }
        }else if(leng2 > leng1){
            var temp = leng2 - leng1
            for(i <- 0 until temp){
                res1 += 0
            }
        }
        //字符串颠倒，
        res1 = res1.reverse
        res2 = res2.reverse
        //判断字符是否一样。
        for(i <- 0 until res1.length){
            if(res1.charAt(i) != res2.charAt(i)){
                res += 1
            }
        }
        res
        
    }
}
```

#### Java
```java
class Solution {
    public int hammingDistance(int x, int y) {
        int res = 0;
        String xStr = "";
        String yStr = "";
        while(x>0){
            xStr = xStr + x%2;
            x = x/2;
            //System.out.println(x);
        }
        while(y>0){
            yStr = yStr + y%2;
            y = y/2;
        }
        int xLeng = xStr.length();
        int yLeng = yStr.length();
        int t = xLeng - yLeng;
        if(t > 0){
            for(int i=0; i<t; i++){
                yStr = yStr + 0;
            }
        }else{
            for(int i=0; i<(0-t); i++){
                xStr = xStr + 0;
            }
        }
        //String xS = new StringBuffer(xStr).reverse().toString();
        //String yS = new StringBuffer(yStr).reverse().toString();
        int leng = xStr.length();
        for(int i=0; i<leng; i++){
            if(xStr.charAt(i) != yStr.charAt(i)){
                res += 1;
            }
        }
        System.out.println(xStr);
        System.out.println(yStr);
        return res;
    }
}
```