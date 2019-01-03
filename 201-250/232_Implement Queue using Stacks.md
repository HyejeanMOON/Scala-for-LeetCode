
Implement the following operations of a queue using stacks.

push(x) -- Push element x to the back of queue.
pop() -- Removes the element from in front of queue.
peek() -- Get the front element.
empty() -- Return whether the queue is empty.
Example:
```
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false
```
Notes:

You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

Difficulty:Easy  
Total Accepted:111.2K  
Total Submissions:287.4K  
Related Topics:Stack, Design


### 解题思路
把stack循环一遍，直到读到最里面的数字。然后把遍历到的数字在放入stack中。
#### Scala
```scala
class MyQueue() {

    /** Initialize your data structure here. */
    var s = new scala.collection.mutable.Stack[Int]()

    /** Push element x to the back of queue. */
    def push(x: Int) {
        s.push(x)
    }

    /** Removes the element from in front of queue and returns that element. */
    def pop(): Int = {
        var re:List[Int] = List()
        for(i <- 0 until s.length){
            re = re :+ s.pop
        }
        var temp = re.reverse
        for(i <- 1 until temp.length){
            s.push(temp(i))
        }
        temp(0)
    }

    /** Get the front element. */
    def peek(): Int = {
        var re:List[Int] = List()
        for(i <- 0 until s.length){
            re = re :+ s.pop
        }
        var temp = re.reverse
        for(i <- 0 until temp.length ){
            s.push(temp(i))
        }
        temp(0)
    }

    /** Returns whether the queue is empty. */
    def empty(): Boolean = {
        s.isEmpty
    }

}

/**
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```


-------

#### Scala
用Queue实现了stack功能。

```scala
class MyQueue() {

    /** Initialize your data structure here. */
    var que = new scala.collection.mutable.Queue[Int]()


    /** Push element x to the back of queue. */
    def push(x: Int) {
        que.enqueue(x)
    }

    /** Removes the element from in front of queue and returns that element. */
    def pop(): Int = {
        for(i <- 0 until que.length-1){
            var temp = que.dequeue
            println(temp+" pop")
            que.enqueue(temp)
        }
        que.dequeue
        
    }

    /** Get the front element. */
    def peek(): Int = {
        for(i <- 0 until que.length-1){
            var temp = que.dequeue
            println(temp+" peek")
            que.enqueue(temp)
        }
        var temp = que.dequeue
        que.enqueue(temp)
        temp
    }

    /** Returns whether the queue is empty. */
    def empty(): Boolean = {
        que.isEmpty
    }

}

/**
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```