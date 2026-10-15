# Chapter: Stack

> Stacks follow the Last-In-First-Out (LIFO) paradigm, making them essential for parsing nested structures, matching brackets, evaluating expressions, and solving monotonic lookback queries.

**Total Questions in Topic:** 7

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 21 | [Valid Parentheses](#21-valid-parentheses) | **Easy** | `LIFO Matching` | [#20](https://leetcode.com/problems/valid-parentheses/) |
| 22 | [Min Stack](#22-min-stack) | **Medium** | `Auxiliary Min Tracker` | [#155](https://leetcode.com/problems/min-stack/) |
| 23 | [Evaluate Reverse Polish Notation](#23-evaluate-reverse-polish-notation) | **Medium** | `Postfix Expression Evaluation` | [#150](https://leetcode.com/problems/evaluate-reverse-polish-notation/) |
| 24 | [Generate Parentheses](#24-generate-parentheses) | **Medium** | `Backtracking with Stack / State` | [#22](https://leetcode.com/problems/generate-parentheses/) |
| 25 | [Daily Temperatures](#25-daily-temperatures) | **Medium** | `Monotonic Decreasing Stack` | [#739](https://leetcode.com/problems/daily-temperatures/) |
| 26 | [Car Fleet](#26-car-fleet) | **Medium** | `Monotonic Stack / Sort by Position` | [#853](https://leetcode.com/problems/car-fleet/) |
| 27 | [Largest Rectangle in Histogram](#27-largest-rectangle-in-histogram) | **Hard** | `Monotonic Increasing Stack` | [#84](https://leetcode.com/problems/largest-rectangle-in-histogram/) |

---

## <a id="21-valid-parentheses"></a>21. Valid Parentheses

- **Difficulty:** `Easy`
- **Pattern:** `LIFO Matching`
- **LeetCode Reference:** [LeetCode #20](https://leetcode.com/problems/valid-parentheses/)

### 1. Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

#### Examples:
**Example 1:**
```text
Input: s = "()"
Output: true
Explanation: Matching pair of round brackets.
```

**Example 2:**
```text
Input: s = "()[]{}"
Output: true
Explanation: All bracket types open and close in proper order.
```

**Example 3:**
```text
Input: s = "(]"
Output: false
Explanation: Mismatched bracket types.
```

#### Constraints:
- `1 <= s.length <= 10^4`
- `s consists of parentheses only '()[]{}'.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Think of nesting Matryoshka dolls or cafeteria trays: the most recently opened container must be the very first one closed before you can close outer ones.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a stack to hold open brackets.
- Hint 2: Map closing brackets to their matching open counterparts in a hash map: `{')': '(', '}': '{', ']': '['}`.
- Hint 3: When encountering a closing bracket, check if the stack is non-empty and `stack.pop() == mapping[c]`. Return `len(stack) == 0` at the end.

### 4. Detailed Approach Walkthrough
1. Initialize an empty `stack = []`.
2. Create a hash map `closeToOpen = {")": "(", "]": "[", "}": "{"}`.
3. For each character `c` in `s`:
   - If `c` in `closeToOpen`:
     - If `stack` and `stack[-1] == closeToOpen[c]`: `stack.pop()`
     - Else: return `False`
   - Else: `stack.append(c)`
4. Return `True` if `not stack` else `False`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        closeToOpen = {")": "(", "]": "[", "}": "{"}
        
        for c in s:
            if c in closeToOpen:
                if stack and stack[-1] == closeToOpen[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
                
        return True if not stack else False
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass through string `s`.`
- **Space Complexity:** `O(n) - Stack can store up to n characters in the worst case.`

---

## <a id="22-min-stack"></a>22. Min Stack

- **Difficulty:** `Medium`
- **Pattern:** `Auxiliary Min Tracker`
- **LeetCode Reference:** [LeetCode #155](https://leetcode.com/problems/min-stack/)

### 1. Problem Statement
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:
- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

#### Examples:
**Example 1:**
```text
Input: ["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]
Output: [null,null,null,null,-3,null,0,-2]
Explanation: MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

#### Constraints:
- `-2^31 <= val <= 2^31 - 1`
- `Methods pop, top and getMin operations will always be called on non-empty stacks.`
- `At most 3 * 10^4 calls will be made to push, pop, top, and getMin.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Every time you place a plate onto a stack, you write down on its underside the lowest price plate below or equal to it. When you remove plates, you never have to re-evaluate the stack because each remaining plate remembers the minimum at its height.

### 3. Step-by-Step Progressive Hints
- Hint 1: Can we use a secondary stack `minStack` that synchronizes with the main stack?
- Hint 2: Whenever pushing `val`, push `min(val, minStack[-1])` onto `minStack`.
- Hint 3: Whenever popping, pop from both `stack` and `minStack`. `getMin()` simply returns `minStack[-1]` in O(1).

### 4. Detailed Approach Walkthrough
1. Maintain two stacks: `self.stack` (values) and `self.minStack` (minimum value up to that height).
2. `push(val)`: append `val` to `stack`. Append `min(val, minStack[-1] if minStack else val)` to `minStack`.
3. `pop()`: pop from both `stack` and `minStack`.
4. `top()`: return `stack[-1]`.
5. `getMin()`: return `minStack[-1]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.minStack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        val = min(val, self.minStack[-1] if self.minStack else val)
        self.minStack.append(val)

    def pop(self) -> None:
        self.stack.pop()
        self.minStack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minStack[-1]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(1) for all operations (push, pop, top, getMin).`
- **Space Complexity:** `O(n) - We store elements in two parallel stacks.`

---

## <a id="23-evaluate-reverse-polish-notation"></a>23. Evaluate Reverse Polish Notation

- **Difficulty:** `Medium`
- **Pattern:** `Postfix Expression Evaluation`
- **LeetCode Reference:** [LeetCode #150](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

### 1. Problem Statement
You are given an array of strings `tokens` that represents an arithmetic expression in a **Reverse Polish Notation**.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:
- Valid operators are `'+'`, `'-'`, `'*'`, and `'/'`.
- Each operand may be an integer or another expression.
- The division between two integers should truncate toward zero.

#### Examples:
**Example 1:**
```text
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**
```text
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

**Example 3:**
```text
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: Evaluates to 22.
```

#### Constraints:
- `1 <= tokens.length <= 10^4`
- `tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> In an RPN calculator (like vintage Hewlett-Packard calculators), you punch in the numbers first. When you press an operator key, it immediately consumes the two most recent numbers on the stack, computes the result, and pushes the answer back on top.

### 3. Step-by-Step Progressive Hints
- Hint 1: Postfix notation places operators immediately after operands.
- Hint 2: Iterate through tokens. If token is a number, push it onto the stack.
- Hint 3: If token is an operator, pop the two most recent numbers `b = stack.pop()` and `a = stack.pop()`, apply `a op b`, and push the result back. Be careful with integer division truncating toward zero (`int(a / b)`).

### 4. Detailed Approach Walkthrough
1. Initialize `stack = []`.
2. Iterate through each token in `tokens`:
   - If `c == "+"`: `stack.append(stack.pop() + stack.pop())`
   - If `c == "-"`: `b, a = stack.pop(), stack.pop(); stack.append(a - b)`
   - If `c == "*"`: `stack.append(stack.pop() * stack.pop())`
   - If `c == "/"`: `b, a = stack.pop(), stack.pop(); stack.append(int(a / b))` (in Python `int(a / b)` correctly truncates toward zero).
   - Else: `stack.append(int(c))`
3. Return `stack[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def evalRPN(self, tokens: list[str]) -> int:
        stack = []
        for c in tokens:
            if c == "+":
                stack.append(stack.pop() + stack.pop())
            elif c == "-":
                b, a = stack.pop(), stack.pop()
                stack.append(a - b)
            elif c == "*":
                stack.append(stack.pop() * stack.pop())
            elif c == "/":
                b, a = stack.pop(), stack.pop()
                stack.append(int(a / b))
            else:
                stack.append(int(c))
        return stack[0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Linear pass through all tokens.`
- **Space Complexity:** `O(n) - Stack stores operands.`

---

## <a id="24-generate-parentheses"></a>24. Generate Parentheses

- **Difficulty:** `Medium`
- **Pattern:** `Backtracking with Stack / State`
- **LeetCode Reference:** [LeetCode #22](https://leetcode.com/problems/generate-parentheses/)

### 1. Problem Statement
Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

#### Examples:
**Example 1:**
```text
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
Explanation: All 5 valid combinations of 3 pairs of parentheses.
```

**Example 2:**
```text
Input: n = 1
Output: ["()"]
Explanation: Only one pair.
```

#### Constraints:
- `1 <= n <= 8`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a turnstile gate: you can only permit someone to enter (open parenthesis `(`) up to `n` times. You can only permit someone to exit (close parenthesis `)`) if there are currently more people inside than have exited (`closed < open`).

### 3. Step-by-Step Progressive Hints
- Hint 1: Only add an open parenthesis `(` if `open_count < n`.
- Hint 2: Only add a close parenthesis `)` if `closed_count < open_count`.
- Hint 3: When `open_count == closed_count == n`, join the current stack characters and append to the result.

### 4. Detailed Approach Walkthrough
1. Initialize `stack = []` and `res = []`.
2. Define a recursive helper `backtrack(openN, closedN)`:
   - Base case: If `openN == closedN == n`, append `"".join(stack)` to `res` and return.
   - If `openN < n`:
     - `stack.append("(")`
     - `backtrack(openN + 1, closedN)`
     - `stack.pop()`
   - If `closedN < openN`:
     - `stack.append(")")`
     - `backtrack(openN, closedN + 1)`
     - `stack.pop()`
3. Call `backtrack(0, 0)` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def generateParenthesis(self, n: int) -> list[str]:
        stack = []
        res = []
        
        def backtrack(openN, closedN):
            if openN == closedN == n:
                res.append("".join(stack))
                return
                
            if openN < n:
                stack.append("(")
                backtrack(openN + 1, closedN)
                stack.pop()
                
            if closedN < openN:
                stack.append(")")
                backtrack(openN, closedN + 1)
                stack.pop()
                
        backtrack(0, 0)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(4^n / sqrt(n)) - The n-th Catalan number bounds the total combinations.`
- **Space Complexity:** `O(n) - Call stack and character buffer of depth 2n.`

---

## <a id="25-daily-temperatures"></a>25. Daily Temperatures

- **Difficulty:** `Medium`
- **Pattern:** `Monotonic Decreasing Stack`
- **LeetCode Reference:** [LeetCode #739](https://leetcode.com/problems/daily-temperatures/)

### 1. Problem Statement
Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `i-th` day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

#### Examples:
**Example 1:**
```text
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
Explanation: Day 0 (73) warms on Day 1 (74, 1 day). Day 2 (75) warms on Day 6 (76, 4 days).
```

**Example 2:**
```text
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
Explanation: Each day warms up the very next day except the last.
```

#### Constraints:
- `1 <= temperatures.length <= 10^5`
- `30 <= temperatures[i] <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine standing in line. People with decreasing heights wait in a queue. When someone taller arrives, they instantly resolve the wait for all shorter people in front of them in the line.

### 3. Step-by-Step Progressive Hints
- Hint 1: A brute force comparing each day with all future days takes O(n^2).
- Hint 2: We can maintain a monotonic decreasing stack of pairs `[temp, index]`.
- Hint 3: When the current temperature is greater than `stack[-1][0]`, pop the top pair and calculate day difference: `res[prevIndex] = currentIndex - prevIndex`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = [0] * len(temperatures)` and `stack = []` (stores pairs `[temp, index]`).
2. Iterate through index `i` and temperature `t` in `temperatures`:
   - While `stack` is non-empty and `t > stack[-1][0]`:
     - `prevT, prevI = stack.pop()`
     - `res[prevI] = i - prevI`
   - `stack.append([t, i])`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def dailyTemperatures(self, temperatures: list[int]) -> list[int]:
        res = [0] * len(temperatures)
        stack = []  # pair: [temp, index]
        
        for i, t in enumerate(temperatures):
            while stack and t > stack[-1][0]:
                stackT, stackInd = stack.pop()
                res[stackInd] = i - stackInd
            stack.append([t, i])
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Each temperature index is pushed and popped from the stack at most once.`
- **Space Complexity:** `O(n) - Stack stores at most n elements in decreasing order.`

---

## <a id="26-car-fleet"></a>26. Car Fleet

- **Difficulty:** `Medium`
- **Pattern:** `Monotonic Stack / Sort by Position`
- **LeetCode Reference:** [LeetCode #853](https://leetcode.com/problems/car-fleet/)

### 1. Problem Statement
There are `n` cars at given miles away from the starting mile 0, traveling to reach the mile `target`.

You are given two integer arrays `position` and `speed`, both of length `n`.

A car can never pass another car ahead of it, but it can catch up to it and drive at the same speed. A **car fleet** is some non-empty set of cars driving at the same position and speed. A single car is also a car fleet.

Return the **number of car fleets** that will arrive at the destination.

#### Examples:
**Example 1:**
```text
Input: target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]
Output: 3
Explanation: Cars at 10 and 8 meet at 12 (fleet 1). Car at 0 arrives alone (fleet 2). Cars at 5 and 3 meet at 6 and arrive together (fleet 3).
```

**Example 2:**
```text
Input: target = 10, position = [3], speed = [3]
Output: 1
Explanation: A single car is 1 fleet.
```

#### Constraints:
- `n == position.length == speed.length`
- `1 <= n <= 10^5`
- `0 < target <= 10^6`
- `0 <= position[i] < target`
- `All values of position are unique.`
- `0 < speed[i] <= 10^6`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a single-lane highway. If a car behind you is moving faster than you, it will catch up to you and get stuck behind you. Since it cannot pass you, its arrival time will be held back to your arrival time.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort cars by their starting position in descending order (closest to target first).
- Hint 2: For each car, calculate the exact time it takes to reach target: `time = (target - pos) / spd`.
- Hint 3: Push times onto a stack. If a car behind arrives in less than or equal time to the car ahead (`stack[-1] <= stack[-2]`), it merges into the fleet ahead, so pop it!

### 4. Detailed Approach Walkthrough
1. Pair position and speed: `pair = [[p, s] for p, s in zip(position, speed)]`.
2. Sort `pair` in reverse order (descending by starting position).
3. Initialize `stack = []`.
4. For each `p, s` in `pair`:
   - Compute time `(target - p) / s` and append to `stack`.
   - If `len(stack) >= 2` and `stack[-1] <= stack[-2]`:
     - The trailing car catches up to the lead car; pop `stack[-1]`.
5. Return `len(stack)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def carFleet(self, target: int, position: list[int], speed: list[int]) -> int:
        pair = [[p, s] for p, s in zip(position, speed)]
        stack = []
        
        for p, s in sorted(pair)[::-1]:  # Reverse sorted order
            time_to_target = (target - p) / s
            stack.append(time_to_target)
            if len(stack) >= 2 and stack[-1] <= stack[-2]:
                stack.pop()
                
        return len(stack)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n log n) - Dominated by sorting cars by initial position.`
- **Space Complexity:** `O(n) - Stack storing arrival times.`

---

## <a id="27-largest-rectangle-in-histogram"></a>27. Largest Rectangle in Histogram

- **Difficulty:** `Hard`
- **Pattern:** `Monotonic Increasing Stack`
- **LeetCode Reference:** [LeetCode #84](https://leetcode.com/problems/largest-rectangle-in-histogram/)

### 1. Problem Statement
Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return the area of the **largest rectangle** in the histogram.

#### Examples:
**Example 1:**
```text
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The maximum rectangle is formed by heights 5 and 6: area = 5 * 2 = 10.
```

**Example 2:**
```text
Input: heights = [2,4]
Output: 4
Explanation: Height 4 with width 1 or height 2 with width 2 = 4.
```

#### Constraints:
- `1 <= heights.length <= 10^5`
- `0 <= heights[i] <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine laying down long horizontal boards across vertical pillars. A board at height `H` can stretch continuously left and right as long as all pillars underneath are at least height `H`. The moment a shorter pillar is encountered, that board cannot stretch any further.

### 3. Step-by-Step Progressive Hints
- Hint 1: A bar of height `h` can extend to the left and right until it meets a bar strictly shorter than `h`.
- Hint 2: Maintain a monotonic increasing stack of pairs `(start_index, height)`.
- Hint 3: When a shorter bar is encountered, pop taller bars from the stack. The popped bar can extend backward all the way to its stored `start_index`. Update `maxArea = max(maxArea, height * (current_index - start_index))`.

### 4. Detailed Approach Walkthrough
1. Initialize `maxArea = 0` and `stack = []` (stores pairs `(index, height)`).
2. Iterate through each `(i, h)` in `heights`:
   - `start = i`
   - While `stack` and `stack[-1][1] > h`:
     - `index, height = stack.pop()`
     - `maxArea = max(maxArea, height * (i - index))`
     - `start = index` (the current shorter bar can extend backward to where the popped taller bar started!)
   - `stack.append((start, h))`
3. After iterating, pop remaining elements extending to `len(heights)`:
   - For `index, height` in `stack`:
     - `maxArea = max(maxArea, height * (len(heights) - index))`
4. Return `maxArea`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def largestRectangleArea(self, heights: list[int]) -> int:
        maxArea = 0
        stack = []  # pair: (index, height)
        
        for i, h in enumerate(heights):
            start = i
            while stack and stack[-1][1] > h:
                index, height = stack.pop()
                maxArea = max(maxArea, height * (i - index))
                start = index
            stack.append((start, h))
            
        for i, h in stack:
            maxArea = max(maxArea, h * (len(heights) - i))
            
        return maxArea
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Each bar is pushed and popped from the stack at most once.`
- **Space Complexity:** `O(n) - Stack stores at most n bars.`

---
