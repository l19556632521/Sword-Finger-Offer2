## [剑指 Offer 30. 包含min函数的栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/description/)

[思路](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/description/#)



## 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

**示例:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

 

**提示：**

1. 各函数的调用总次数不超过 20000 次

 

注意：本题与主站 155 题相同：https://leetcode-cn.com/problems/min-stack/



## 解题思路

主要是这个随时返回栈中最小元素这个问题，该怎么想到，可以借助另一个栈来存储阶段性最小值元素



## 正确题解



```java
class MinStack {
    //记录栈中的所有元素
    Stack<Integer> stack = new Stack<>();
    //记录阶段性的最小元素
    Stack<Integer> minStack = new Stack<>();

    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
    }
    
    public void push(int x) {
        stack.push(x);
        //阶段最小值栈为空或者当前值小于阶段最小栈顶元素
        if(minStack.isEmpty() || x <= minStack.peek()) {
            //同时存入最小栈
            minStack.push(x);
        } else {
            //插入元素大于栈顶元素
            minStack.push(minStack.peek());
        }
    }
    
    public void pop() {
        //直接弹出两个栈的栈顶元素
        stack.pop();
        minStack.pop();
    }
    
    public int top() {
        //返回栈顶元素
        return stack.peek();
    }
    
    public int min() {
        //minStack栈顶为当前栈中最小元素
        return minStack.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.min();
 */
```







## 其他题解（简化版）

阶段最小值栈中存储的只是每一次比较的最小值，不是存入所有元素

所以在取出的时候也要判断原栈弹出的元素是否等于最小栈栈顶元素，是则同步删最小栈栈顶元素

````java
class MinStack {
    Stack<Integer> stack = new Stack<>();
    //只放最小元素
    Stack<Integer> minStack = new Stack<>();

    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
    }
    
    public void push(int x) {
        stack.push(x);
        //如果最小值栈不为空且插入插入元素小于最小栈顶元素
        if(minStack.isEmpty() || x <= minStack.peek()) {
            minStack.push(x);
        }
    }
    
    public void pop() {
        //如果要弹出的元素和最小栈栈顶元素相等
        if(stack.peek().equals(minStack.peek())) {
            //弹出最下栈栈顶元素
            minStack.pop();
        }
        stack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int min() {
        //直接返回最小栈顶元素
        return minStack.peek();
    }
}
````

