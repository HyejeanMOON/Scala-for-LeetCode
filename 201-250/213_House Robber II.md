You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

Example 1:
```
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
```
Example 2:
```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

Difficulty:Medium  
Total Accepted:83.6K  
Total Submissions:240.8K  
Related Topics:Dynamic Programming

### 解题思路
这道题是之前那道House Robber 打家劫舍的拓展，现在房子排成了一个圆圈，则如果抢了第一家，就不能抢最后一家，因为首尾相连了，所以第一家和最后一家只能抢其中的一家，或者都不抢，那我们这里变通一下，如果我们把第一家和最后一家分别去掉，各算一遍能抢的最大值，然后比较两个值取其中较大的一个即为所求。那我们只需参考之前的House Robber 打家劫舍中的解题方法，然后调用两边取较大值。
#### Scala
```Scala
object Solution {
    def rob(nums: Array[Int]): Int = {
        var len = nums.length
        if(nums.isEmpty) return 0
        var res = 0
        if(len<=3){   
            for(n <- nums) res = scala.math.max(res,n)
        }
        else res = scala.math.max(maxMoney(nums,0,len-1),maxMoney(nums,1,len))
        res
    }
    def maxMoney(nums:Array[Int],left:Int,right:Int):Int={
        if((right-left) <= 1) return nums(left)  
        //因为在上面已经判断小于等于三的情况，所以上一句可以不要。
        var dp = new scala.collection.mutable.ArrayBuffer[Int]()
        for(i <- 0 until right)  dp = dp :+ 0
        dp(left) = nums(left)
        dp(left+1) = scala.math.max(nums(left),nums(left+1))
        for(i <- left+2 until right)  dp(i) = scala.math.max(dp(i-2)+nums(i),dp(i-1))
        dp(right-1)
    }
}
```


```Java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if(len==0) return 0;
        int res = 0;
        if(len<=3){
            for(Integer n:nums){
                res = Math.max(n,res);
            }
        }else{
            res = Math.max(maxMoney(nums,0,len-1),maxMoney(nums,1,len));
        }
        return res;
    }
    
    public int maxMoney(int[] nums,int left, int right){
        int[] dp = new int[right];
        for(int i=0; i<right; i++){
            dp[i] = 0;
        }
        dp[left]=nums[left];
        dp[left+1]=Math.max(nums[left],nums[left+1]);
        for(int i=left+2; i<right; i++){
            dp[i] = Math.max(dp[i-1],dp[i-2]+nums[i]);
        }
        return dp[right-1];
    }
}
```
