There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

Example 1:
```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```
Example 2:
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

Difficulty:Hard  
Total Accepted:271.1K  
Total Submissions:1.2M  
Related Topics:Array, Binary Search, Divide and Conquer

### 解题思路
这道题比较简单。因为两个数组已经是排好序的，所以只要声明一个数组，比较两个数组大小然后放进record里就可以了。  
然后进行奇偶判断，根据奇偶返回相应的值。  
这里需要注意数据类型的转换。
#### Scala
```scala
object Solution {
    def findMedianSortedArrays(nums1: Array[Int], nums2: Array[Int]): Double = {
        var len1 = nums1.length
        var len2 = nums2.length
        var isOdd = false
        if((len1+len2)%2!=0) isOdd=true
        var record:Array[Int] = Array()
        var cur1 = 0
        var cur2 = 0
        while(cur1!=len1 || cur2!=len2 ){
            if(cur1!=len1 && cur2!=len2){
                if(nums1(cur1)>nums2(cur2)){
                    record = record:+nums2(cur2)
                    cur2+=1
                }else if(nums1(cur1)==nums2(cur2)){
                    record = record :+ nums1(cur1)
                    cur1+=1
                    record = record :+ nums2(cur2)
                    cur2+=1
                }else{
                    record = record :+ nums1(cur1)
                    cur1+=1
                }
            }else if(cur1!=len1){
                record = record :+ nums1(cur1)
                cur1+=1
            }else{
                record = record :+ nums2(cur2)
                cur2+=1
            }
        }
        record.foreach(println)
        println(isOdd)
        var res:Double = 0
        if(isOdd){
            var cur = (len1+len2-1)/2
            res = record(cur)
        }else{
            var cur = (len1+len2)/2
            res = (record(cur).toDouble+record(cur-1).toDouble)/2
        }
        res
    }
}
```