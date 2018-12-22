Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:  
You are not suppose to use the library's sort function for this problem.

Difficulty:Medium  
Total Accepted:218.2K  
Total Submissions:560.8K  
Related Topics:Array, Two Pointer, Sort

### 解题思路
如果是使用api的话，如下方法。
#### Java
```java
class Solution {
    public void sortColors(int[] nums) {
        Arrays.sort(nums);
    }
}
```


---

使用冒泡排序。
```java
class Solution {
    public void sortColors(int[] nums) {
        int len = nums.length;
        for(int i = 0; i < len-1; i++){
            for(int j=i+1; j<len;j++){
                if(nums[i]>nums[j]){
                    int temp = nums[i];
                    nums[i] = nums[j];
                    nums[j] = temp;
                }
            }
        }     
    }
}
```
