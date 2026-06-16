# Implement Queue using Stacks

## Problem Statement

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

**Implement the `MyQueue` class:**
- `void push(int x)` — Pushes element `x` to the back of the queue.
- `int pop()` — Removes the element from the front of the queue and returns it.
- `int peek()` — Returns the element at the front of the queue.
- `boolean empty()` — Returns `true` if the queue is empty, `false` otherwise.

**Notes:**
- You must use only standard stack operations: push to top, peek/pop from top, size, and isEmpty.
- You may simulate a stack using a list or deque as long as you only use stack's standard operations.

---

## Approach: Two Stacks (Lazy Transfer / Amortized O(1))

Use two stacks:
- **inputStack** — receives all `push` operations (new elements go on top, i.e., at the "back").
- **outputStack** — serves `pop` and `peek` operations (front of queue is at its top).

The key insight is that reversing a stack gives FIFO order. When `outputStack` is empty and we need the front element, we pour everything from `inputStack` into `outputStack` — this reversal makes the oldest element end up on top.

**Transfer is lazy:** we only move elements when `outputStack` is empty, so each element is transferred at most once across its lifetime, giving **amortized O(1)** per operation.

### Complexity
| Operation | Time | Space |
|-----------|------|-------|
| `push`    | O(1) | O(n)  |
| `pop`     | O(1) amortized | — |
| `peek`    | O(1) amortized | — |
| `empty`   | O(1) | — |

---

## Code (Java)

```java
class MyQueue {
    private Deque<Integer> inputStack = new ArrayDeque();
    private Deque<Integer> outputStack = new ArrayDeque();

    public MyQueue() {
        
    }
    
    public void push(int x) {
        inputStack.push(x);
    }
    
    public int pop() {
        transferElements();
        return outputStack.pop();
    }
    
    public int peek() {
        transferElements();
        return outputStack.peek();
    }
    
    public boolean empty() {
        return inputStack.isEmpty() && outputStack.isEmpty();
    }

    private void transferElements(){
        if(outputStack.isEmpty()){
            while(!inputStack.isEmpty()){
                outputStack.push(inputStack.pop());
            }
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

---

## Walkthrough Example

```
push(1) → inputStack: [1]        outputStack: []
push(2) → inputStack: [2, 1]     outputStack: []
peek()  → transfer: inputStack: [], outputStack: [1, 2]  → returns 1
pop()   → outputStack already has elements → pop returns 1
          outputStack: [2]
empty() → false
```
