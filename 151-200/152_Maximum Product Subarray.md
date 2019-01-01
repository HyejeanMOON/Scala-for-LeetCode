Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.



Difficulty:Medium  
Total Accepted:133.7K  
Total Submissions:501.4K  

Related Topics ：Array, Dynamic Programming

### 解题思路
这个求最大子数组乘积问题是由最大子数组之和问题演变而来，但是却比求最大子数组之和要复杂，因为在求和的时候，遇到0，不会改变最大值，遇到负数，也只是会减小最大值而已。而在求最大子数组乘积的问题中，遇到0会使整个乘积为0，而遇到负数，则会使最大乘积变成最小乘积，正因为有负数和0的存在，使问题变得复杂了不少。。

比如，我们现在有一个数组[2, 3, -2, 4]，我们可以很容易的找出所有的连续子数组，[2], [3], [-2], [4], [2, 3], [3, -2], [-2, 4], [2, 3, -2], [3, -2, 4], [2, 3, -2, 4], 然后可以很轻松的算出最大的子数组乘积为6，来自子数组[2, 3].

那么我们如何写代码来实现自动找出最大子数组乘积呢，我最先想到的方比较简单粗暴，就是找出所有的子数组，然后算出每一个子数组的乘积，然后比较找出最大的一个，需要两个for循环，第一个for遍历整个数组，第二个for遍历含有当前数字的子数组，就是按以下顺序找出子数组: [2], [2, 3], [2, 3, -2], [2, 3, -2, 4],    [3], [3, -2], [3, -2, 4],    [-2], [-2, 4],    [4], 我在本地测试的一些数组全部通过，于是兴高采烈的拿到OJ上测试，结果丧心病狂的OJ用一个有15000个数字的数组来测试，然后说我程序的运行时间超过了要求值，我一看我的代码，果然如此，时间复杂度O(n2), 得想办法只用一次循环搞定。我想来想去想不出好方法，于是到网上搜各位大神的解决方法。其实这道题最直接的方法就是用DP来做，而且要用两个dp数组，其中f[i]表示子数组[0, i]范围内的最大子数组乘积，g[i]表示子数组[0, i]范围内的最小子数组乘积，初始化时f[0]和g[0]都初始化为nums[0]，其余都初始化为0。那么从数组的第二个数字开始遍历，那么此时的最大值和最小值只会在这三个数字之间产生，即f[i-1]*nums[i]，g[i-1]*nums[i]，和nums[i]。所以我们用三者中的最大值来更新f[i]，用最小值来更新g[i]，然后用f[i]来更新结果res即可。
#### Scala
```scala
object Solution {
    def maxProduct(nums: Array[Int]): Int = {
        var leng = nums.length
        var f = new scala.collection.mutable.ArrayBuffer[Int](leng)
        var g = new scala.collection.mutable.ArrayBuffer[Int](leng)
        var res = nums(0)
        for(i <- 0 until leng){
            f = f :+ 0
            g = g :+ 0
        }
        f(0) = nums(0)
        g(0) = nums(0)
        for(i <- 1 until leng){
            f(i) = scala.math.max(scala.math.max(f(i-1)*nums(i),g(i-1)*nums(i)),nums(i))
            g(i) = scala.math.min(scala.math.min(f(i-1)*nums(i),g(i-1)*nums(i)),nums(i))
            res = scala.math.max(res,f(i))
        }
        res
    }
}
```