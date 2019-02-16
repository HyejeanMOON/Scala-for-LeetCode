Given an array A of positive lengths, return the largest perimeter of a triangle with non-zero area, formed from 3 of these lengths.

If it is impossible to form any triangle of non-zero area, return 0.

EASY

Example 1:
```
Input: [2,1,2]
Output: 5
```
Example 2:
```
Input: [1,2,1]
Output: 0
```
Example 3:
```
Input: [3,2,3,4]
Output: 10
```
Example 4:
```
Input: [3,6,2,3]
Output: 8
```

Note:
```
3 <= A.length <= 10000
1 <= A[i] <= 10^6
```

#### 说明
连着的三个数组成的三角形，三边之和最大。
#### Java
```java
class Solution {
    public int largestPerimeter(int[] A) {
        Arrays.sort(A);
        int ci = A.length - 1;
        while (ci > 1) {
            int c = A[ci];
            int a = A[ci  - 1];
            int b = A[ci - 2];
            if (a + b > c) return a + b + c;
            ci--;
        }
        return 0;
    }
}
```