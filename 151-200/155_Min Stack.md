Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
Example:
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

Difficulty:Easy  
Total Accepted:202.5K  
Total Submissions:627.7K  
Related Topics:Stack,Design

### 解题思路
这道最小栈跟原来的栈相比就是多了一个功能，可以返回该栈的最小值。使用两个栈来实现，一个栈来按顺序存储push进来的数据，另一个用来存出现过的最小值。
#### Scala
```scala
class MinStack() {

    /** initialize your data structure here. */
    var s1 = new scala.collection.mutable.Stack[Int]()
    var s2 = new scala.collection.mutable.Stack[Int]()

    def push(x: Int) {
        if(s2.isEmpty || s2.top>=x) s2.push(x)
        s1.push(x)
    }

    def pop() {
        if(s1.top==s2.top) s2.pop
        return s1.pop
    }

    def top(): Int = {
        return s1.top
    }

    def getMin(): Int = {
        return s2.top
    }

}

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```

---
```Java
public class MinStack {
    private Stack<Integer> s1 = new Stack<>();
    private Stack<Integer> s2 = new Stack<>();
    
    /** initialize your data structure here. */
    public MinStack() {}
    
    public void push(int x) {
        s1.push(x);
        if (s2.isEmpty() || s2.peek() >= x) s2.push(x);
    }
    
    public void pop() {
        // Cannot write like the following:
        // if (s2.peek() == s1.peek()) s2.pop();
        // s1.pop();
        int x = s1.pop();
        if (s2.peek() == x) s2.pop();
    }
    
    public int top() {
        return s1.peek();
    }
    
    public int getMin() {
        return s2.peek();
    }
}
```