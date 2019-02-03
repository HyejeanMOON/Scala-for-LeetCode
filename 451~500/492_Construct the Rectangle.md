For a web developer, it is very important to know how to design a web page's size. So, given a specific rectangular web page’s area, your job by now is to design a rectangular web page, whose length L and width W satisfy the following requirements:

1. The area of the rectangular web page you designed must equal to the given target area.

2. The width W should not be larger than the length L, which means L >= W.

3. The difference between length L and width W should be as small as possible.
You need to output the length L and the width W of the web page you designed in sequence.
Example:
```
Input: 4
Output: [2, 2]
Explanation: The target area is 4, and all the possible ways to construct it are [1,4], [2,2], [4,1]. 
But according to requirement 2, [1,4] is illegal; according to requirement 3,  [4,1] is not optimal compared to [2,2]. So the length L is 2, and the width W is 2.
```
Note:  
The given area won't exceed 10,000,000 and is a positive integer
The web page's width and length you designed must be positive integers.


Difficulty:Easy  
Total Accepted:32.6K  
Total Submissions:67.7K  

### 解题思路
这道题让我们根据面积来求出矩形的长和宽，要求长和宽的差距尽量的小，那么就是说越接近正方形越好。那么我们肯定是先来判断一下是不是正方行，对面积开方，如果得到的不是整数，说明不是正方形。那么我们取最近的一个整数，看此时能不能整除，如果不行，就自减1，再看能否整除。最坏的情况就是面积是质数，最后减到了1，那么返回结果即可。
#### Scala


```scala
object Solution {
    def constructRectangle(area: Int): Array[Int] = {
        var t = (scala.math.sqrt(area)).toInt
        if(t*t == area) return Array(t,t)
        else{
            while(t>0){
                if(area%t == 0) {
                    if(area/t > t) return Array(area/t,t)
                    else return Array(t,area/t)
                }
                t-= 1
            }
        }
        Array()
        
    }
}
```
#### Scala
```scala
object Solution {
    def constructRectangle(area: Int): Array[Int] = {
        var t = (scala.math.sqrt(area)).toInt
        if(t*t == area) return Array(t,t)
        while(area%t != 0) t-=1
        Array(area/t,t)
    }
}
```