Design a HashSet without using any built-in hash table libraries.

To be specific, your design should include these functions:

add(value): Insert a value into the HashSet. 
contains(value) : Return whether the value exists in the HashSet or not.
remove(value): Remove a value in the HashSet. If the value does not exist in the HashSet, do nothing.

Example:
```
MyHashSet hashSet = new MyHashSet();
hashSet.add(1);         
hashSet.add(2);         
hashSet.contains(1);    // returns true
hashSet.contains(3);    // returns false (not found)
hashSet.add(2);          
hashSet.contains(2);    // returns true
hashSet.remove(2);          
hashSet.contains(2);    // returns false (already removed)
```
Note:

All values will be in the range of [0, 1000000].
The number of operations will be in the range of [1, 10000].
Please do not use the built-in HashSet library.

Difficulty:Easy  
Total Accepted:1K  
Total Submissions:6.5K  
Related Topics:Hash Table, Design


### 解题思路
#### Scala
```Scala
class MyHashSet() {

    /** Initialize your data structure here. */
    var record:Map[Int,Int] = Map()

    def add(key: Int) {
        var temp = record.getOrElse(key,0)
        if(temp==0) record+=(key -> 1)
    }

    def remove(key: Int) {
        record+=(key -> 0)
    }

    /** Returns true if this set contains the specified element */
    def contains(key: Int): Boolean = {
        var res = true
        var temp = record.getOrElse(key,0)
        if(temp==0) res = false
        res
    }

}

/**
 * Your MyHashSet object will be instantiated and called as such:
 * var obj = new MyHashSet()
 * obj.add(key)
 * obj.remove(key)
 * var param_3 = obj.contains(key)
 */
```