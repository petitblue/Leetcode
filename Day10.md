## 232. Implement Queue using Stacks
https://leetcode.com/problems/implement-queue-using-stacks/solutions/?q=python&orderBy=most_relevant
1. use stack2 to append all the stack1's pop elements and stack1 add all the stack2's pop elements, then we can reorder
the elements as a queue in stack1.
```sh
class MyQueue:

    def __init__(self):
        self.stack1 = []
        self.stack2 = []
    #  queue 1 2 3
    # we two stack to implement queue
    # stack is first in  last out
    # so we push an element to s1, and pop it to s2,
    # and s1 append the s2 pop element then we will has s1's order
    
    def push(self, x: int) -> None:
        while self.stack1:
            self.stack2.append(self.stack1.pop())
        self.stack2.append(x)
        while self.stack2:
            self.stack1.append(self.stack2.pop())


    def pop(self) -> int:
        return self.stack1.pop()
        

    def peek(self) -> int:
        return self.stack1[-1]

    def empty(self) -> bool:
        return len(self.stack1) == 0 and len(self.stack2)== 0
        
```

##225. Implement Stack using Queues
https://leetcode.com/problems/implement-stack-using-queues/
use 2 queues
```sh
class MyStack:
    
    def __init__(self):
        from collections import deque
        self.q1 = deque()
        self.q2 = deque()
    # s 1 2 3.  3 first out
    # q    2 1
    # q2  
    def push(self, x: int) -> None:
        while self.q1:
            self.q2.append(self.q1.popleft())
        self.q1.append(x)
        while self.q2:
            self.q1.append(self.q2.popleft())
        
    def pop(self) -> int:
        return self.q1.popleft()

    def top(self) -> int:
        return self.q1[0]

    def empty(self) -> bool:
        return len(self.q1) == 0 and len(self.q2)==0
```

2. use one. queue
```sh

class MyStack:

    def __init__(self):
        from collections import deque 
        self.q = deque()

    def push(self, x: int) -> None:
        self.q.append(x)

    def pop(self) -> int:
        for i in range(0, len(self.q)-1):
            self.q.append(self.q.popleft()). // the q will keep addup the left pop up value, and thus reverse the order
        return self.q.popleft()

    def top(self) -> int:
        return self.q[-1]

    def empty(self) -> bool:
        return len(self.q) ==0
        
   ```
