Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
empty() -- Return whether the stack is empty.
Example:
```
MyStack stack = new MyStack();

stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false
```
Notes:

You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

Difficulty:Easy  
Total Accepted:99.1K  
Total Submissions:283K  
Related Topics:Stack, Design

### 解题思路
#### Scala
```scala
class MyStack() {

    /** Initialize your data structure here. */
    var que = new scala.collection.mutable.Queue[Int]()

    /** Push element x onto stack. */
    def push(x: Int) {
       que.enqueue(x) 
    }

    /** Removes the element on top of the stack and returns that element. */
    def pop(): Int = {
        var len = que.length
        for(i <- 0 until len-1){
            var temp = que.dequeue
            que.enqueue(temp)
        }
        que.dequeue
    }

    /** Get the top element. */
    def top(): Int = {
        var len = que.length
        for(i <- 0 until len-1){
            var temp = que.dequeue
            que.enqueue(temp)
        }
        var res = que.dequeue
        que.enqueue(res)
        res
    }

    /** Returns whether the stack is empty. */
    def empty(): Boolean = {
        que.isEmpty
    }

}

/**
 * Your MyStack object will be instantiated and called as such:
 * var obj = new MyStack()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.empty()
 */
```