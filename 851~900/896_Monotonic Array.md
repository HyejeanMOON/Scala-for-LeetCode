
An array is monotonic if it is either monotone increasing or monotone decreasing.

An array A is monotone increasing if for all i <= j, A[i] <= A[j].  An array A is monotone decreasing if for all i <= j, A[i] >= A[j].

Return true if and only if the given array A is monotonic.

 

Example 1:
```
Input: [1,2,2,3]
Output: true
```
Example 2:
```
Input: [6,5,4,4]
Output: true
```
Example 3:
```
Input: [1,3,2]
Output: false
```
Example 4:
```
Input: [1,2,4,5]
Output: true
```
Example 5:
```
Input: [1,1,1]
Output: true
```

Note:

- 1 <= A.length <= 50000
- -100000 <= A[i] <= 100000

Difficulty:Easy  
Total Accepted:8.3K  
Total Submissions:14.8K  
Related Topics:Array

### 解题思路
#### Scala
```Scala
object Solution {
    def isMonotonic(A: Array[Int]): Boolean = {
        var res = true
        var len = A.length
        for(i <- 0 until len-1){
            if(A(i)-A(i+1)<0) res=false
        }
        if(res) return res
        res=true
        for(i <- 0 until len-1){
            if(A(i)-A(i+1)>0) res=false
        }
        res
    }
}
```