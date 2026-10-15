# Chapter: Greedy

> Greedy algorithms build up a solution piece by piece, always choosing the immediate local optimum that leads directly to a globally optimal outcome in linear O(n) time.

**Total Questions in Topic:** 8

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 122 | [Maximum Subarray](#122-maximum-subarray) | **Medium** | `Kadane's Algorithm` | [#53](https://leetcode.com/problems/maximum-subarray/) |
| 123 | [Jump Game](#123-jump-game) | **Medium** | `Greedy Goal Post Shifting` | [#55](https://leetcode.com/problems/jump-game/) |
| 124 | [Jump Game II](#124-jump-game-ii) | **Medium** | `Greedy BFS Window Expansion` | [#45](https://leetcode.com/problems/jump-game-ii/) |
| 125 | [Gas Station](#125-gas-station) | **Medium** | `Greedy Reset Linear Scan` | [#134](https://leetcode.com/problems/gas-station/) |
| 126 | [Hand of Straights](#126-hand-of-straights) | **Medium** | `Min-Heap Frequency Greedy Matching` | [#846](https://leetcode.com/problems/hand-of-straights/) |
| 127 | [Merge Triplets to Form Target Triplet](#127-merge-triplets-to-form-target-triplet) | **Medium** | `Greedy Elimination Filter` | [#1899](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/) |
| 128 | [Partition Labels](#128-partition-labels) | **Medium** | `Last Occurrence Greedy Partitioning` | [#763](https://leetcode.com/problems/partition-labels/) |
| 129 | [Valid Parenthesis String](#129-valid-parenthesis-string) | **Medium** | `Greedy Min/Max Open Range` | [#678](https://leetcode.com/problems/valid-parenthesis-string/) |

---

## <a id="122-maximum-subarray"></a>122. Maximum Subarray

- **Difficulty:** `Medium`
- **Pattern:** `Kadane's Algorithm`
- **LeetCode Reference:** [LeetCode #53](https://leetcode.com/problems/maximum-subarray/)

### 1. Problem Statement
Given an integer array `nums`, find the subarray with the **largest sum**, and return its sum.

#### Examples:
**Example 1:**
```text
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: Subarray [4,-1,2,1] has the largest sum 6.
```

#### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Carrying luggage on a hike: if your accumulated bag weight drops below 0 (negative sum), carrying it further only drags down future progress. Dump the bag and start fresh from the current step (`curSum = 0`).

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain `maxSub = nums[0]` and `curSum = 0`.
- Hint 2: If `curSum < 0`, reset `curSum = 0` before adding the next element.

### 4. Detailed Approach Walkthrough
1. `maxSub = nums[0]`, `curSum = 0`.
2. For `n` in `nums`:
   - If `curSum < 0`: `curSum = 0`
   - `curSum += n`
   - `maxSub = max(maxSub, curSum)`
3. Return `maxSub`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxSubArray(self, nums: list[int]) -> int:
        maxSub = nums[0]
        curSum = 0
        
        for n in nums:
            if curSum < 0:
                curSum = 0
            curSum += n
            maxSub = max(maxSub, curSum)
            
        return maxSub
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass through nums.`
- **Space Complexity:** `O(1) - Constant tracking variables.`

---

## <a id="123-jump-game"></a>123. Jump Game

- **Difficulty:** `Medium`
- **Pattern:** `Greedy Goal Post Shifting`
- **LeetCode Reference:** [LeetCode #55](https://leetcode.com/problems/jump-game/)

### 1. Problem Statement
You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` if you can reach the last index, or `false` otherwise.

#### Examples:
**Example 1:**
```text
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**
```text
Input: nums = [3,2,1,0,4]
Output: false
Explanation: Will always arrive at index 3 with jump length 0.
```

#### Constraints:
- `1 <= nums.length <= 10^4`
- `0 <= nums[i] <= 10^5`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Shifting the finish line backwards: start with `goal = last_index`. If position `i` can reach `goal` (`i + nums[i] >= goal`), shift the finish line closer to `goal = i`. If the finish line reaches index 0, the game is winnable.

### 3. Step-by-Step Progressive Hints
- Hint 1: Iterate backwards from `len(nums) - 1` with `goal = len(nums) - 1`.
- Hint 2: If `i + nums[i] >= goal`, update `goal = i`.
- Hint 3: Return `goal == 0`.

### 4. Detailed Approach Walkthrough
1. `goal = len(nums) - 1`.
2. For `i` in range(len(nums) - 1, -1, -1):
   - If `i + nums[i] >= goal`:
     - `goal = i`
3. Return `goal == 0`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def canJump(self, nums: list[int]) -> bool:
        goal = len(nums) - 1
        
        for i in range(len(nums) - 1, -1, -1):
            if i + nums[i] >= goal:
                goal = i
                
        return True if goal == 0 else False
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single backwards pass.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="124-jump-game-ii"></a>124. Jump Game II

- **Difficulty:** `Medium`
- **Pattern:** `Greedy BFS Window Expansion`
- **LeetCode Reference:** [LeetCode #45](https://leetcode.com/problems/jump-game-ii/)

### 1. Problem Statement
You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. Return the **minimum number of jumps** to reach `nums[n - 1]`.

#### Examples:
**Example 1:**
```text
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

#### Constraints:
- `1 <= nums.length <= 10^4`
- `0 <= nums[i] <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> BFS level by level without allocating a queue: maintain the current jump reach window `[l, r]`. In 1 jump, find the absolute farthest point reachable from all indices within `[l, r]`, then set `l = r + 1` and `r = farthest`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain window `l = 0, r = 0, res = 0`.
- Hint 2: While `r < len(nums) - 1`, compute `farthest = max(i + nums[i] for i in range(l, r + 1))`, then `l = r + 1; r = farthest; res += 1`.

### 4. Detailed Approach Walkthrough
1. `res = 0, l = 0, r = 0`.
2. While `r < len(nums) - 1`:
   - `farthest = 0`
   - For `i` in range(l, r + 1):
     - `farthest = max(farthest, i + nums[i])`
   - `l = r + 1`
   - `r = farthest`
   - `res += 1`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def jump(self, nums: list[int]) -> int:
        res = 0
        l = r = 0
        
        while r < len(nums) - 1:
            farthest = 0
            for i in range(l, r + 1):
                farthest = max(farthest, i + nums[i])
            l = r + 1
            r = farthest
            res += 1
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Every index evaluated once in window expansion.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="125-gas-station"></a>125. Gas Station

- **Difficulty:** `Medium`
- **Pattern:** `Greedy Reset Linear Scan`
- **LeetCode Reference:** [LeetCode #134](https://leetcode.com/problems/gas-station/)

### 1. Problem Statement
There are `n` gas stations along a circular route, where the amount of gas at the `i-th` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `i-th` station to its next `(i + 1)-th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return the **starting gas station's index** if you can travel around the circuit once in the clockwise direction, otherwise return `-1`.

#### Examples:
**Example 1:**
```text
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation: Start at station 3 (index 3). Gas = 4. Cost to next = 1. Remaining gas = 3. Successfully loops.
```

#### Constraints:
- `n == gas.length == cost.length`
- `1 <= n <= 10^5`
- `0 <= gas[i], cost[i] <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> If total gas is strictly less than total cost, a complete loop is impossible. Otherwise, a solution is guaranteed to exist: if you run out of gas starting from station `A` while trying to reach station `B`, NO station between `A` and `B` could have succeeded either! Reset start to `B + 1`.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `sum(gas) < sum(cost)`, return -1.
- Hint 2: Iterate through stations maintaining `total += (gas[i] - cost[i])`. If `total < 0`, reset `total = 0` and `res = i + 1`.

### 4. Detailed Approach Walkthrough
1. If `sum(gas) < sum(cost)`: return `-1`.
2. `total = 0, res = 0`.
3. For `i` in range(`len(gas)`):
   - `total += (gas[i] - cost[i])`
   - If `total < 0`:
     - `total = 0`
     - `res = i + 1`
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def canCompleteCircuit(self, gas: list[int], cost: list[int]) -> int:
        if sum(gas) < sum(cost):
            return -1
            
        total = 0
        res = 0
        for i in range(len(gas)):
            total += (gas[i] - cost[i])
            if total < 0:
                total = 0
                res = i + 1
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass over the arrays.`
- **Space Complexity:** `O(1) - Constant tracking variables.`

---

## <a id="126-hand-of-straights"></a>126. Hand of Straights

- **Difficulty:** `Medium`
- **Pattern:** `Min-Heap Frequency Greedy Matching`
- **LeetCode Reference:** [LeetCode #846](https://leetcode.com/problems/hand-of-straights/)

### 1. Problem Statement
Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size `groupSize`, and consists of `groupSize` consecutive cards.

Given an integer array `hand` where `hand[i]` is the value written on the `i-th` card and an integer `groupSize`, return `true` if she can rearrange the cards, or `false` otherwise.

#### Examples:
**Example 1:**
```text
Input: hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
Output: true
Explanation: Groups: [1,2,3], [2,3,4], [6,7,8].
```

#### Constraints:
- `1 <= hand.length <= 10^4`
- `0 <= hand[i] <= 10^9`
- `1 <= groupSize <= hand.length`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Playing cards straight flush: you must always find consecutive cards starting from the absolute smallest card currently in your hand (`minHeap[0]`). If `minHeap[0] + 1` or `+ 2` is missing, you cannot form a valid straight.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `len(hand) % groupSize != 0`, return False.
- Hint 2: Build a frequency map `count = collections.Counter(hand)` and a Min-Heap of unique keys.
- Hint 3: Pop the minimum card `first`. For `i` in range(`first, first + groupSize`), decrement `count[i]`. If count becomes 0, ensure it was popped from heap.

### 4. Detailed Approach Walkthrough
1. If `len(hand) % groupSize != 0`: return `False`.
2. `count = Counter(hand)`, `minH = list(count.keys())`, `heapq.heapify(minH)`.
3. While `minH`:
   - `first = minH[0]`
   - For `i` in range(`first, first + groupSize`):
     - If `i not in count`: return `False`
     - `count[i] -= 1`
     - If `count[i] == 0`:
       - If `i != minH[0]`: return `False` (out-of-order exhaustion)
       - `heapq.heappop(minH)`
4. Return `True`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq
import collections

class Solution:
    def isNStraightHand(self, hand: list[int], groupSize: int) -> bool:
        if len(hand) % groupSize:
            return False
            
        count = collections.Counter(hand)
        minH = list(count.keys())
        heapq.heapify(minH)
        
        while minH:
            first = minH[0]
            for i in range(first, first + groupSize):
                if i not in count:
                    return False
                count[i] -= 1
                if count[i] == 0:
                    if i != minH[0]:
                        return False
                    heapq.heappop(minH)
                    
        return True
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N log N) - Heap operations over N cards.`
- **Space Complexity:** `O(N) - Hash map and min-heap.`

---

## <a id="127-merge-triplets-to-form-target-triplet"></a>127. Merge Triplets to Form Target Triplet

- **Difficulty:** `Medium`
- **Pattern:** `Greedy Elimination Filter`
- **LeetCode Reference:** [LeetCode #1899](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/)

### 1. Problem Statement
A **triplet** is an array of three integers. You are given a 2D integer array `triplets`, where `triplets[i] = [ai, bi, ci]`. You are also given an integer array `target = [x, y, z]`.

To obtain target, you can apply the following operation on `triplets` any number of times: choose two indices `i` and `j` and update `triplets[j] = [max(ai, aj), max(bi, bj), max(ci, cj)]`.

Return `true` if it is possible to obtain `target` as an element of `triplets`, or `false` otherwise.

#### Examples:
**Example 1:**
```text
Input: triplets = [[2,5,3],[1,8,4],[1,7,5]], target = [2,7,5]
Output: true
Explanation: Merge [2,5,3] and [1,7,5] -> [2,7,5].
```

#### Constraints:
- `1 <= triplets.length <= 10^5`
- `triplets[i].length == target.length == 3`
- `1 <= ai, bi, ci, x, y, z <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Filtering candidate materials: if any triplet contains a dimension greater than target (`t[0] > target[0] or t[1] > target[1] or t[2] > target[2]`), including it will ruin the result because `max()` operations can never decrease values. Discard all such invalid triplets and check if remaining triplets can cover all 3 target coordinates.

### 3. Step-by-Step Progressive Hints
- Hint 1: Ignore any triplet where `t[0] > target[0] or t[1] > target[1] or t[2] > target[2]`.
- Hint 2: For valid triplets, maintain a set `good = set()` of matching target indices where `t[i] == target[i]`.
- Hint 3: Return `len(good) == 3`.

### 4. Detailed Approach Walkthrough
1. `good = set()`.
2. For `t` in `triplets`:
   - If `t[0] > target[0] or t[1] > target[1] or t[2] > target[2]`: continue
   - For `i, v` in enumerate(t):
     - If `v == target[i]`: `good.add(i)`
3. Return `len(good) == 3`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def mergeTriplets(self, triplets: list[list[int]], target: list[int]) -> bool:
        good = set()
        
        for t in triplets:
            if t[0] > target[0] or t[1] > target[1] or t[2] > target[2]:
                continue
            for i, v in enumerate(t):
                if v == target[i]:
                    good.add(i)
                    
        return len(good) == 3
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass through triplets.`
- **Space Complexity:** `O(1) - Set stores at most 3 indices.`

---

## <a id="128-partition-labels"></a>128. Partition Labels

- **Difficulty:** `Medium`
- **Pattern:** `Last Occurrence Greedy Partitioning`
- **LeetCode Reference:** [LeetCode #763](https://leetcode.com/problems/partition-labels/)

### 1. Problem Statement
You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return a list of integers representing the size of these parts.

#### Examples:
**Example 1:**
```text
Input: s = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation: Partitions: "ababcbaca", "defegde", "hijhklij".
```

#### Constraints:
- `1 <= s.length <= 500`
- `s consists of lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Grouping chapters in a book: find the final last page where character 'a' appears. Your current partition MUST extend at least to that last page. As you scan forward, if you meet character 'b' whose final appearance is even further right, extend the partition boundary to that new maximum.

### 3. Step-by-Step Progressive Hints
- Hint 1: Record `lastIndex = {c: i for i, c in enumerate(s)}`.
- Hint 2: Iterate through string maintaining `end = max(end, lastIndex[s[i]])` and `size += 1`.
- Hint 3: When `i == end`, append `size` to `res` and reset `size = 0`.

### 4. Detailed Approach Walkthrough
1. `lastIndex = {c: i for i, c in enumerate(s)}`.
2. `res = []`, `size = 0, end = 0`.
3. For `i, c` in enumerate(s):
   - `size += 1`
   - `end = max(end, lastIndex[c])`
   - If `i == end`:
     - `res.append(size)`
     - `size = 0`
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def partitionLabels(self, s: str) -> list[int]:
        lastIndex = {}
        for i, c in enumerate(s):
            lastIndex[c] = i
            
        res = []
        size, end = 0, 0
        for i, c in enumerate(s):
            size += 1
            end = max(end, lastIndex[c])
            if i == end:
                res.append(size)
                size = 0
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Two linear passes over string.`
- **Space Complexity:** `O(1) - Bounded by 26 lowercase English letters.`

---

## <a id="129-valid-parenthesis-string"></a>129. Valid Parenthesis String

- **Difficulty:** `Medium`
- **Pattern:** `Greedy Min/Max Open Range`
- **LeetCode Reference:** [LeetCode #678](https://leetcode.com/problems/valid-parenthesis-string/)

### 1. Problem Statement
Given a string `s` containing only three types of characters: `'('`, `')'` and `'*'`, return `true` if `s` is **valid**.

The following rules define a **valid** string:
- Any left parenthesis `'('` must have a corresponding right parenthesis `')'`.
- Any right parenthesis `')'` must have a corresponding left parenthesis `'('`.
- Left parenthesis `'('` must go before the corresponding right parenthesis `')'`.
- `'*'` could be treated as a single right parenthesis `')'` or a single left parenthesis `'('` or an empty string `""`.

#### Examples:
**Example 1:**
```text
Input: s = "()"
Output: true
Explanation: Valid pair.
```

**Example 2:**
```text
Input: s = "(*)"
Output: true
Explanation: '*' treated as empty string.
```

**Example 3:**
```text
Input: s = "(*))"
Output: true
Explanation: '*' treated as '('.
```

#### Constraints:
- `1 <= s.length <= 100`
- `s[i] is '(', ')' or '*'.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Tracking the possible range of open parentheses `[cmin, cmax]`: `'('` increments both bounds, `')'` decrements both bounds, and `'*'` expands the range (`cmin -= 1`, `cmax += 1`). As long as `cmax` never drops below 0 and final `cmin == 0`, the string is valid.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain `cmin` (minimum possible open count) and `cmax` (maximum possible open count).
- Hint 2: If `cmax < 0`, return False immediately.
- Hint 3: Keep `cmin = max(cmin, 0)`. At the end, return `cmin == 0`.

### 4. Detailed Approach Walkthrough
1. `cmin, cmax = 0, 0`.
2. For `c` in `s`:
   - If `c == "("`: `cmin += 1; cmax += 1`
   - Else if `c == ")"`: `cmin -= 1; cmax -= 1`
   - Else: `cmin -= 1; cmax += 1` (wildcard)
   - If `cmax < 0`: return `False`
   - `if cmin < 0: cmin = 0`
3. Return `cmin == 0`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        cmin, cmax = 0, 0
        
        for c in s:
            if c == "(":
                cmin, cmax = cmin + 1, cmax + 1
            elif c == ")":
                cmin, cmax = cmin - 1, cmax - 1
            else:
                cmin, cmax = cmin - 1, cmax + 1
                
            if cmax < 0:
                return False
            if cmin < 0:
                cmin = 0
                
        return cmin == 0
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass through string.`
- **Space Complexity:** `O(1) - Constant tracking variables.`

---
