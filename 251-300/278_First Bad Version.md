You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

### 解题思路
这道题说是有一系列版本，其中有一个版本是坏的，而且后面跟着的全是坏的，给了一个API函数可以用来判定当前版本是否是坏的，让我们尽可能少的调用这个API，找出第一个坏版本。那么这种搜索题最先开始考虑用二分查找法把，效率高嘛。由于这题很有规律，好版本和坏版本一定有个边界，那么我们用二分法来找这个边界，对mid值调用API函数，如果是坏版本，说明边界在左边，则把mid赋值给right，如果是好版本，则说明边界在右边，则把mid+1赋给left，最后返回left即可。需要注意的是，OJ里有个坑，那就是如果left和right都特别大的话，那么left+right可能会溢出，我们的处理方法就是变成left + (right - left) / 2，很好的避免的溢出问题。
#### Java
```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        while(left < right){
            int mid = left + (right-left)/2;
            if(isBadVersion(mid)) right = mid;
            else left = mid+1; 
        }
        return left;
    }
}
```