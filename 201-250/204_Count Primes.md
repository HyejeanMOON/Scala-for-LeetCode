Count the number of prime numbers less than a non-negative number, n.

Example:
```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```


Difficulty:Easy   
Total Accepted:158.5K  
Total Submissions:596.2K  
Related Topics:Hash Table, Math

### 解题思路
这道题给定一个非负数n，让我们求小于n的质数的个数，题目中给了充足的提示，解题方法就在第二个提示埃拉托斯特尼筛法Sieve of Eratosthenes中，这个算法的过程如下图所示，我们从2开始遍历到根号n，先找到第一个质数2，然后将其所有的倍数全部标记出来，然后到下一个质数3，标记其所有倍数，一次类推，直到根号n，此时数组中未被标记的数字就是质数。我们需要一个n-1长度的bool型数组来记录每个数字是否被标记，长度为n-1的原因是题目说是小于n的质数个数，并不包括n。 然后我们用两个for循环来实现埃拉托斯特尼筛法，难度并不是很大。
#### Java
```java
class Solution {
    public int countPrimes(int n) {
        if(n==0||n==1) return 0;
        Boolean[] num = new Boolean[n];
        for(int i=0; i<n-1;i++){
            num[i] = true;
        }
        num[0] = false;
        int res = 0;
        int limit = (int)Math.sqrt(n);
        for(int i=2; i<=limit;i++){
            if(num[i-1]){
                for(int j=i*i; j<n; j=j+i){
                    num[j-1] = false;
                }
            }
        }
        for(int j=0; j<n-1;j++){
            if(num[j]) res++;
        }
        return res;
    }
}
```