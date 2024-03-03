---
description: 栈实现队列以及队列实现栈
---

# 栈和队列的相互实现

## 栈实现队列

### 思路

需要用2个栈来实现队列，一个栈为输入栈，一个栈为输出栈。

#### push

输入栈压入待添加元素

#### pop/peek

当输出栈不为空时，将输入栈所有元素弹出并压入输出栈。此后，对输出栈进行pop/peek操作即可

#### 判空

输入栈和输出栈同时为空

### 代码实现

```java
class MyQueue {

    Stack<Integer> stack1, stack2;

    public MyQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }
    
    public void push(int x) {
        stack1.push(x);
    }
    
    public int pop() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }
    
    public int peek() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.peek();
    }
    
    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```

## 队列实现栈

### 思路

用一个队列即可实现

#### push

1. 记录当前栈的大小
2. 压入待添加元素
3. 循环将队尾元素弹出并加入队首

#### pop/peek

对队尾元素进行pop/peek操作即可

#### 判空

队列大小为空

### 代码实现

```java
class MyStack {

    Queue<Integer> q;

    public MyStack() {
        q = new LinkedList<>();
    }
    
    public void push(int x) {
        int size = q.size();
        q.offer(x);
        for (int i = 0; i < size; i++) {
            q.offer(q.poll());
        }
    }
    
    public int pop() {
        return q.poll();
    }
    
    public int top() {
        return q.peek();
    }
    
    public boolean empty() {
        return q.size() == 0;
    }
}
```
