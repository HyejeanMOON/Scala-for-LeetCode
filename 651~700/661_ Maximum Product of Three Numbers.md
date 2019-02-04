Given an integer array, find three numbers whose product is maximum and output the maximum product.

Example 1:
```
Input: [1,2,3]
Output: 6
```
Example 2:
```
Input: [1,2,3,4]
Output: 24
```
Note:
- The length of the given array will be in range [3,104] and all elements are in the range [-1000, 1000].   
- Multiplication of any three numbers in the input won't exceed the range of 32-bit signed integer.





### 解题思路
这道题博主刚开始看的时候，心想直接排序，然后最后三个数字相乘不就完了，心想不会这么Easy吧，果然被OJ无情打脸，没有考虑到负数和0的情况。这道题给了数组的范围，至少三个，那么如果是三个的话，就无所谓了，直接相乘返回即可，但是如果超过了3个，而且有负数存在的话，情况就可能不一样，我们来考虑几种情况，如果全是负数，三个负数相乘还是负数，为了让负数最大，那么其绝对值就该最小，而负数排序后绝对值小的都在末尾，所以是末尾三个数字相乘，这个跟全是正数的情况一样。那么重点在于前半段是负数，后半段是正数，那么最好的情况肯定是两个最小的负数相乘得到一个正数，然后跟一个最大的正数相乘，这样得到的肯定是最大的数，所以我们让前两个数相乘，再和数组的最后一个数字相乘，就可以得到这种情况下的最大的乘积。实际上我们并不用分情况讨论数组的正负，只要把这两种情况的乘积都算出来，比较二者取较大值，就能涵盖所有的情况，从而得到正确的结果。
#### Scala
```
object Solution {
    def maximumProduct(nums: Array[Int]): Int = {
        var leng = nums.length
        var num = nums.sorted
        var temp = num(0) * num(1) * num(leng-1)
        var result = 0
        if(temp > (num(leng-1)*num(leng-2)*num(leng-3))){
            result = temp
        }else{
            result = num(leng-1) * num(leng-2) * num(leng-3)
        }
        result
    }
}
```