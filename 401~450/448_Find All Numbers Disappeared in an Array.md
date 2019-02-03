Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```
### 解题思路
这道题让我们找出数组中所有消失的数，跟之前那道Find the Duplicate Number极其类似，那道题让找出所有重复的数字，这道题让找不存在的数，这类问题的一个重要条件就是1 ≤ a[i] ≤ n (n = size of array)，不然很难在O(1)空间和O(n)时间内完成。三种解法也跟之前题目的解法极其类似。首先来看第一种解法，这种解法的思路路是，对于每个数字nums[i]，如果其对应的nums[nums[i] - 1]是正数，我们就赋值为其相反数，如果已经是负数了，就不变了，那么最后我们只要把留下的整数对应的位置加入结果res中即可。  
用同样的方法在scala中，然而超时。
#### Java
```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<Integer>();
        for(int i=0; i < nums.length; i++){
            int index = Math.abs(nums[i])-1;
            if(nums[index]>0) nums[index] = 0-nums[index];
        }
        for(int j=0; j<nums.length; j++){
            if(nums[j] > 0) res.add(j+1);
        }
        return res;
    }
}
```