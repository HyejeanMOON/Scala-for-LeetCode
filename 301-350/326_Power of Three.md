Given an integer, write a function to determine if it is a power of three.

Follow up:
Could you do it without using any loop / recursion?

Difficulty:Easy  
Total Accepted:123.6K  
Total Submissions:303.4K  
Related Topics:Math

### 解题思路
#### Scala
```scala
object Solution {
    def isPowerOfThree(n: Int): Boolean = {
        if(n<=0) return false
        if(n==1) return true
        var temp = n
        while(temp>1){
            var t = temp % 3
            if(t!=0) return false
            temp /= 3
        }
        true
    }
}
```

### 方法二
题目中的Follow up让我们不用循环，那么有一个投机取巧的方法，由于输入是int，正数范围是0-231，在此范围中允许的最大的3的次方数为319=1162261467，那么我们只要看这个数能否被n整除即可。
#### Scala
```scala
object Solution {
    def isPowerOfThree(n: Int): Boolean = {
        return (n>0 && 1162261467%n ==0)
    }
}
```


### 方法三
最后还有一种巧妙的方法，利用对数的换底公式来做，高中学过的换底公式为logab = logcb / logca，那么如果n是3的倍数，则log3n一定是整数，我们利用换底公式可以写为log3n = log10n / log103，注意这里一定要用10为底数，不能用自然数或者2为底数，否则当n=243时会出错，原因请看这个帖子。现在问题就变成了判断log10n / log103是否为整数，在c++中判断数字a是否为整数，我们可以用 a - int(a) == 0 来判断 方法三。
```c
class Solution {
public:
    bool isPowerOfThree(int n) {
        return (n > 0 && int(log10(n) / log10(3)) - log10(n) / log10(3) == 0);
    }
};
```
