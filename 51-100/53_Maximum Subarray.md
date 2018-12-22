Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

Difficulty:Easy  
Total Accepted:293.6K  
Total Submissions:729.6K  
Related Topics : Array, Divide and Conquer, Dynamic Programming

### 解题思路
### 方法一： 
比较笨的方式用双循环，复杂度O(N2)。 每次相加都在判断是否是最大值。
#### Scala
```scala
object Solution {
    def maxSubArray(nums: Array[Int]): Int = {
        var max = scala.Int.MinValue
        if(nums.length==1) return nums(0)
        for(i <- 0 until nums.length){
            var temp = nums(i)
            max = scala.math.max(temp,max)
            for(j <- i+1 until nums.length){
                temp  += nums(j)
                max = scala.math.max(temp,max)
            }
        }
        max
    }
}
```
#### 方法二
定义两个变量res和curSum，其中res保存最终要返回的结果，即最大的子数组之和，curSum初始值为0，每遍历一个数字num，比较curSum + num和num中的较大值存入curSum，然后再把res和curSum中的较大值存入res，以此类推直到遍历完整个数组，可得到最大子数组的值存在res中。 复杂度为O（N）。
#### Scala
```scala
object Solution {
    def maxSubArray(nums: Array[Int]): Int = {
        var res = scala.Int.MinValue
        var curSum = 0
        for(n <- nums){
            curSum = scala.math.max(curSum+n,n)
            res = scala.math.max(curSum,res)
        }
        res
    }
}
```
#### Java
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = Integer.MIN_VALUE;
        int curSum = 0;
        for(Integer n:nums){
            curSum = Math.max(curSum+n,n);
            res = Math.max(res,curSum);
        }
        return res;
    }
}
```

### 方法三：
题目还要求我们用分治法Divide and Conquer Approach来解，这个分治法的思想就类似于二分搜索法，我们需要把数组一分为二，分别找出左边和右边的最大子数组之和，然后还要从中间开始向左右分别扫描，求出的最大值分别和左右两边得出的最大值相比较取最大的那一个。
#### Java
```java
public class Solution {
    public int maxSubArray(int[] nums) {
        if (nums.length == 0) return 0;
        return helper(nums, 0, nums.length - 1);
    }
    public int helper(int[] nums, int left, int right) {
        if (left >= right) return nums[left];
        int mid = left + (right - left) / 2;
        int lmax = helper(nums, left, mid - 1);
        int rmax = helper(nums, mid + 1, right);
        int mmax = nums[mid], t = mmax;
        for (int i = mid - 1; i >= left; --i) {
            t += nums[i];
            mmax = Math.max(mmax, t);
        }
        t = mmax;
        for (int i = mid + 1; i <= right; ++i) {
            t += nums[i];
            mmax = Math.max(mmax, t);
        }
        return Math.max(mmax, Math.max(lmax, rmax));
    }
}
```
