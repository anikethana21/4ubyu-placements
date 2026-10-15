# Chapter: 2-D Dynamic Programming

> 2-D DP tackles grid traversals, string alignments, and two-state decisions with tabular matrices and memoized states.

**Total Questions in Topic:** 11

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 111 | [Unique Paths](#111-unique-paths) | **Medium** | `2D Grid DP / Combinatorics` | [#62](https://leetcode.com/problems/unique-paths/) |
| 112 | [Longest Common Subsequence](#112-longest-common-subsequence) | **Medium** | `2D String Alignment Matrix` | [#1143](https://leetcode.com/problems/longest-common-subsequence/) |
| 113 | [Best Time to Buy and Sell Stock with Cooldown](#113-best-time-to-buy-and-sell-stock-with-cooldown) | **Medium** | `State Machine DP` | [#309](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/) |
| 114 | [Coin Change II](#114-coin-change-ii) | **Medium** | `Unbounded Knapsack Combinations DP` | [#518](https://leetcode.com/problems/coin-change-ii/) |
| 115 | [Target Sum](#115-target-sum) | **Medium** | `2D DP / Knapsack Memoization` | [#494](https://leetcode.com/problems/target-sum/) |
| 116 | [Interleaving String](#116-interleaving-string) | **Medium** | `2D Grid DP` | [#97](https://leetcode.com/problems/interleaving-string/) |
| 117 | [Longest Increasing Path in a Matrix](#117-longest-increasing-path-in-a-matrix) | **Hard** | `2D Grid DFS with Memoization` | [#329](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/) |
| 118 | [Distinct Subsequences](#118-distinct-subsequences) | **Hard** | `2D String DP (Matching Counts)` | [#115](https://leetcode.com/problems/distinct-subsequences/) |
| 119 | [Edit Distance](#119-edit-distance) | **Medium** | `2D Levenshtein Distance Matrix` | [#72](https://leetcode.com/problems/edit-distance/) |
| 120 | [Burst Balloons](#120-burst-balloons) | **Hard** | `Matrix Chain Multiplication DP (Reverse Thinking)` | [#312](https://leetcode.com/problems/burst-balloons/) |
| 121 | [Regular Expression Matching](#121-regular-expression-matching) | **Hard** | `2D Regex Parsing DP` | [#10](https://leetcode.com/problems/regular-expression-matching/) |

---

## <a id="111-unique-paths"></a>111. Unique Paths

- **Difficulty:** `Medium`
- **Pattern:** `2D Grid DP / Combinatorics`
- **LeetCode Reference:** [LeetCode #62](https://leetcode.com/problems/unique-paths/)

### 1. Problem Statement
There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (`grid[0][0]`). The robot tries to move to the **bottom-right corner** (`grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

#### Examples:
**Example 1:**
```text
Input: m = 3, n = 7
Output: 28
Explanation: 28 distinct paths.
```

**Example 2:**
```text
Input: m = 3, n = 2
Output: 3
Explanation: Paths: Right->Down->Down, Down->Down->Right, Down->Right->Down.
```

#### Constraints:
- `1 <= m, n <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Starting at the bottom-right goal and working backward: the number of paths from cell `(r, c)` is the sum of paths from its right neighbor `(r, c+1)` plus paths from its bottom neighbor `(r+1, c)`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Bottom row is all 1s (can only move right).
- Hint 2: Compress to 1D row: `row[c] = row[c + 1] + row[c]` (sum of right and down).

### 4. Detailed Approach Walkthrough
1. Initialize bottom `row = [1] * n`.
2. Loop `m - 1` times:
   - `newRow = [1] * n`
   - For `j` from `n - 2` down to 0:
     - `newRow[j] = newRow[j + 1] + row[j]`
   - `row = newRow`
3. Return `row[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        row = [1] * n
        
        for i in range(m - 1):
            newRow = [1] * n
            for j in range(n - 2, -1, -1):
                newRow[j] = newRow[j + 1] + row[j]
            row = newRow
            
        return row[0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(m * n) - Grid traversal.`
- **Space Complexity:** `O(n) - Single 1D row memory.`

---

## <a id="112-longest-common-subsequence"></a>112. Longest Common Subsequence

- **Difficulty:** `Medium`
- **Pattern:** `2D String Alignment Matrix`
- **LeetCode Reference:** [LeetCode #1143](https://leetcode.com/problems/longest-common-subsequence/)

### 1. Problem Statement
Given two strings `text1` and `text2`, return the length of their **longest common subsequence**. If there is no common subsequence, return `0`.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

#### Examples:
**Example 1:**
```text
Input: text1 = "abcde", text2 = "ace"
Output: 3
Explanation: LCS is "ace" of length 3.
```

**Example 2:**
```text
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: No common characters.
```

#### Constraints:
- `1 <= text1.length, text2.length <= 1000`
- `text1 and text2 consist of only lowercase English characters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Comparing two text documents (like `git diff`): at index `(i, j)`, if characters match, you get +1 score and advance both diagonally (`1 + dp[i+1][j+1]`). If they mismatch, you branch into the best of advancing `text1` (`dp[i+1][j]`) or advancing `text2` (`dp[i][j+1]`).

### 3. Step-by-Step Progressive Hints
- Hint 1: Build a `(len(text1) + 1) x (len(text2) + 1)` 2D DP matrix initialized to 0.
- Hint 2: Iterate backwards: if `text1[i] == text2[j]`: `dp[i][j] = 1 + dp[i+1][j+1]`; else: `dp[i][j] = max(dp[i+1][j], dp[i][j+1])`.

### 4. Detailed Approach Walkthrough
1. `dp = [[0 for j in range(len(text2) + 1)] for i in range(len(text1) + 1)]`.
2. For `i` from `len(text1) - 1` down to 0:
   - For `j` from `len(text2) - 1` down to 0:
     - If `text1[i] == text2[j]`:
       - `dp[i][j] = 1 + dp[i + 1][j + 1]`
     - Else:
       - `dp[i][j] = max(dp[i + 1][j], dp[i][j + 1])`
3. Return `dp[0][0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[0 for j in range(len(text2) + 1)] for i in range(len(text1) + 1)]
        
        for i in range(len(text1) - 1, -1, -1):
            for j in range(len(text2) - 1, -1, -1):
                if text1[i] == text2[j]:
                    dp[i][j] = 1 + dp[i + 1][j + 1]
                else:
                    dp[i][j] = max(dp[i + 1][j], dp[i][j + 1])
                    
        return dp[0][0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M) - Where N and M are lengths of text1 and text2.`
- **Space Complexity:** `O(N * M) - 2D DP table.`

---

## <a id="113-best-time-to-buy-and-sell-stock-with-cooldown"></a>113. Best Time to Buy and Sell Stock with Cooldown

- **Difficulty:** `Medium`
- **Pattern:** `State Machine DP`
- **LeetCode Reference:** [LeetCode #309](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

### 1. Problem Statement
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i-th` day.

Find the maximum profit you can achieve. You may complete as many transactions as you like with the following restrictions:
- After you sell your stock, you cannot buy stock on the next day (i.e., **cooldown one day**).

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

#### Examples:
**Example 1:**
```text
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: Transactions = [buy, sell, cooldown, buy, sell].
```

#### Constraints:
- `1 <= prices.length <= 5000`
- `0 <= prices[i] <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A 2-state decision tree: State `(i, buying)`. If `buying`: choose between buying stock today `(profit - prices[i])` or resting `(cooldown)`. If `selling`: choose between selling stock today `(profit + prices[i])` and jumping `i + 2` days ahead for mandatory cooldown, or holding.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use memoization `dp = {}` mapping `(i, buying) -> max_profit`.
- Hint 2: When selling, transition to `dfs(i + 2, not buying)`.

### 4. Detailed Approach Walkthrough
1. `dp = {}`.
2. Define `dfs(i, buying)`:
   - If `i >= len(prices)`: return 0
   - If `(i, buying) in dp`: return `dp[(i, buying)]`
   - `cooldown = dfs(i + 1, buying)`
   - If `buying`:
     - `buy = dfs(i + 1, not buying) - prices[i]`
     - `dp[(i, buying)] = max(buy, cooldown)`
   - Else:
     - `sell = dfs(i + 2, not buying) + prices[i]`
     - `dp[(i, buying)] = max(sell, cooldown)`
   - Return `dp[(i, buying)]`
3. Return `dfs(0, True)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        dp = {}  # (i, buying) -> max_profit
        
        def dfs(i, buying):
            if i >= len(prices):
                return 0
            if (i, buying) in dp:
                return dp[(i, buying)]
                
            cooldown = dfs(i + 1, buying)
            if buying:
                buy = dfs(i + 1, not buying) - prices[i]
                dp[(i, buying)] = max(buy, cooldown)
            else:
                sell = dfs(i + 2, not buying) + prices[i]
                dp[(i, buying)] = max(sell, cooldown)
                
            return dp[(i, buying)]
            
        return dfs(0, True)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - 2 * n unique states memoized.`
- **Space Complexity:** `O(n) - Memoization dictionary and call stack.`

---

## <a id="114-coin-change-ii"></a>114. Coin Change II

- **Difficulty:** `Medium`
- **Pattern:** `Unbounded Knapsack Combinations DP`
- **LeetCode Reference:** [LeetCode #518](https://leetcode.com/problems/coin-change-ii/)

### 1. Problem Statement
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the **number of combinations** that make up that amount. If that amount of money cannot be made up by any combination of the coins, return `0`.

You may assume that you have an infinite number of each kind of coin.

#### Examples:
**Example 1:**
```text
Input: amount = 5, coins = [1,2,5]
Output: 4
Explanation: 4 ways: 5, 2+2+1, 2+1+1+1, 1+1+1+1+1.
```

#### Constraints:
- `1 <= coins.length <= 300`
- `1 <= coins[i] <= 5000`
- `0 <= amount <= 5000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Counting unique coin combinations: process coins one by one in outer loop so coins are considered in fixed order, preventing permutations like `1+2` and `2+1` from being double counted.

### 3. Step-by-Step Progressive Hints
- Hint 1: Initialize `dp = [0] * (amount + 1)` with `dp[0] = 1`.
- Hint 2: Loop over each coin first, then update amounts from `coin` to `amount`: `dp[a] += dp[a - coin]`.

### 4. Detailed Approach Walkthrough
1. Initialize `dp = [0] * (amount + 1)` and `dp[0] = 1`.
2. For `coin` in `coins`:
   - For `a` in range(`coin`, `amount + 1`):
     - `dp[a] += dp[a - coin]`
3. Return `dp[amount]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def change(self, amount: int, coins: list[int]) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 1
        
        for coin in coins:
            for a in range(coin, amount + 1):
                dp[a] += dp[a - coin]
                
        return dp[amount]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(amount * len(coins)) - Double loop.`
- **Space Complexity:** `O(amount) - 1D DP table.`

---

## <a id="115-target-sum"></a>115. Target Sum

- **Difficulty:** `Medium`
- **Pattern:** `2D DP / Knapsack Memoization`
- **LeetCode Reference:** [LeetCode #494](https://leetcode.com/problems/target-sum/)

### 1. Problem Statement
You are given an integer array `nums` and an integer `target`.

You want to build an expression out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

Return the number of different **expressions** that you can build, which evaluates to `target`.

#### Examples:
**Example 1:**
```text
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: 5 expressions evaluate to 3.
```

#### Constraints:
- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `-1000 <= target <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A balance scale: at each step, you must place the current weight on the positive pan or the negative pan.

### 3. Step-by-Step Progressive Hints
- Hint 1: State is `(index, total)`. Base case: if `index == len(nums)`, return 1 if `total == target` else 0.
- Hint 2: Memoize `dp[(index, total)] = dfs(index + 1, total + nums[index]) + dfs(index + 1, total - nums[index])`.

### 4. Detailed Approach Walkthrough
1. `dp = {}`.
2. Define `backtrack(i, total)`:
   - If `i == len(nums)`: return 1 if `total == target` else 0
   - If `(i, total) in dp`: return `dp[(i, total)]`
   - `dp[(i, total)] = backtrack(i + 1, total + nums[i]) + backtrack(i + 1, total - nums[i])`
   - Return `dp[(i, total)]`
3. Return `backtrack(0, 0)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findTargetSumWays(self, nums: list[int], target: int) -> int:
        dp = {}
        
        def backtrack(i, total):
            if i == len(nums):
                return 1 if total == target else 0
            if (i, total) in dp:
                return dp[(i, total)]
                
            dp[(i, total)] = (backtrack(i + 1, total + nums[i]) +
                              backtrack(i + 1, total - nums[i]))
            return dp[(i, total)]
            
        return backtrack(0, 0)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * sum(nums)) - N elements across sum range.`
- **Space Complexity:** `O(N * sum(nums)) - DP cache and recursion stack.`

---

## <a id="116-interleaving-string"></a>116. Interleaving String

- **Difficulty:** `Medium`
- **Pattern:** `2D Grid DP`
- **LeetCode Reference:** [LeetCode #97](https://leetcode.com/problems/interleaving-string/)

### 1. Problem Statement
Given strings `s1`, `s2`, and `s3`, find whether `s3` is formed by an **interleaving** of `s1` and `s2`.

#### Examples:
**Example 1:**
```text
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
Explanation: Valid interleave of s1 and s2.
```

#### Constraints:
- `0 <= s1.length, s2.length <= 100`
- `0 <= s3.length <= 200`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Shuffling two decks into a third: at each step, the next card of `s3` must match either the top card of `s1` or `s2`.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `len(s1) + len(s2) != len(s3)`, return False.
- Hint 2: Use 2D DP `dp[i][j]` representing whether `s1[i:]` and `s2[j:]` can form `s3[i+j:]`.

### 4. Detailed Approach Walkthrough
1. If `len(s1) + len(s2) != len(s3)`: return `False`.
2. Initialize `dp = [[False] * (len(s2) + 1) for _ in range(len(s1) + 1)]`, `dp[len(s1)][len(s2)] = True`.
3. Iterate `i` and `j` backwards:
   - If `i < len(s1)` and `s1[i] == s3[i + j]` and `dp[i + 1][j]`: `dp[i][j] = True`
   - If `j < len(s2)` and `s2[j] == s3[i + j]` and `dp[i][j + 1]`: `dp[i][j] = True`
4. Return `dp[0][0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False
            
        dp = [[False] * (len(s2) + 1) for _ in range(len(s1) + 1)]
        dp[len(s1)][len(s2)] = True
        
        for i in range(len(s1), -1, -1):
            for j in range(len(s2), -1, -1):
                if i < len(s1) and s1[i] == s3[i + j] and dp[i + 1][j]:
                    dp[i][j] = True
                if j < len(s2) and s2[j] == s3[i + j] and dp[i][j + 1]:
                    dp[i][j] = True
                    
        return dp[0][0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M) - Grid of size len(s1) * len(s2).`
- **Space Complexity:** `O(N * M) - 2D table.`

---

## <a id="117-longest-increasing-path-in-a-matrix"></a>117. Longest Increasing Path in a Matrix

- **Difficulty:** `Hard`
- **Pattern:** `2D Grid DFS with Memoization`
- **LeetCode Reference:** [LeetCode #329](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

### 1. Problem Statement
Given an `m x n` integers matrix, return the length of the **longest increasing path** in `matrix`.

From each cell, you can either move in four directions: left, right, up, or down. You may **not** move diagonally or move outside the boundary.

#### Examples:
**Example 1:**
```text
Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4
Explanation: Longest increasing path is [1, 2, 6, 9].
```

#### Constraints:
- `m == matrix.length, n == matrix[i].length`
- `1 <= m, n <= 200`
- `0 <= matrix[i][j] <= 2^31 - 1`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Climbing upward in a topographic terrain: since you can strictly only move to higher elevations (`matrix[nr][nc] > matrix[r][c]`), cycles are mathematically impossible (DAG). Memoize the longest uphill path from every coordinate.

### 3. Step-by-Step Progressive Hints
- Hint 1: Since paths must be strictly increasing, the graph is a Directed Acyclic Graph (DAG).
- Hint 2: Memoize `dp[(r, c)] = 1 + max(dfs(nr, nc))` for all valid uphill neighbors.

### 4. Detailed Approach Walkthrough
1. `ROWS, COLS = len(matrix), len(matrix[0])`, `dp = {}`.
2. Define `dfs(r, c, prevVal)`:
   - If out of bounds or `matrix[r][c] <= prevVal`: return 0
   - If `(r, c) in dp`: return `dp[(r, c)]`
   - `res = 1`
   - For `dr, dc` in `[[0,1], [0,-1], [1,0], [-1,0]]`:
     - `res = max(res, 1 + dfs(r + dr, c + dc, matrix[r][c]))`
   - `dp[(r, c)] = res`
   - Return `res`
3. Loop over all `r, c` and return `max(dfs(r, c, -1))`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def longestIncreasingPath(self, matrix: list[list[int]]) -> int:
        ROWS, COLS = len(matrix), len(matrix[0])
        dp = {}  # (r, c) -> LIP
        
        def dfs(r, c, prevVal):
            if (r < 0 or r == ROWS or c < 0 or c == COLS or matrix[r][c] <= prevVal):
                return 0
            if (r, c) in dp:
                return dp[(r, c)]
                
            res = 1
            res = max(res, 1 + dfs(r + 1, c, matrix[r][c]))
            res = max(res, 1 + dfs(r - 1, c, matrix[r][c]))
            res = max(res, 1 + dfs(r, c + 1, matrix[r][c]))
            res = max(res, 1 + dfs(r, c - 1, matrix[r][c]))
            dp[(r, c)] = res
            return res
            
        for r in range(ROWS):
            for c in range(COLS):
                dfs(r, c, -1)
                
        return max(dp.values())
```

### 6. Complexity Analysis
- **Time Complexity:** `O(ROWS * COLS) - Each cell computed once.`
- **Space Complexity:** `O(ROWS * COLS) - Memoization table.`

---

## <a id="118-distinct-subsequences"></a>118. Distinct Subsequences

- **Difficulty:** `Hard`
- **Pattern:** `2D String DP (Matching Counts)`
- **LeetCode Reference:** [LeetCode #115](https://leetcode.com/problems/distinct-subsequences/)

### 1. Problem Statement
Given two strings `s` and `t`, return the **number of distinct subsequences** of `s` which equals `t`.

#### Examples:
**Example 1:**
```text
Input: s = "rabbbit", t = "rabbit"
Output: 3
Explanation: Three different ways to form "rabbit" from "rabbbit".
```

#### Constraints:
- `1 <= s.length, t.length <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Pattern matching with multiple choices: if `s[i] == t[j]`, you can either consume `s[i]` to match `t[j]` (`dfs(i+1, j+1)`), OR skip `s[i]` and look for another match in `s` (`dfs(i+1, j)`).

### 3. Step-by-Step Progressive Hints
- Hint 1: Base cases: if `j == len(t)`, return 1 (matched full t). If `i == len(s)`, return 0.
- Hint 2: If `s[i] == t[j]`: `dp[(i, j)] = dfs(i + 1, j + 1) + dfs(i + 1, j)`. Else: `dp[(i, j)] = dfs(i + 1, j)`.

### 4. Detailed Approach Walkthrough
1. `cache = {}`.
2. Define `dfs(i, j)`:
   - If `j == len(t)`: return 1
   - If `i == len(s)`: return 0
   - If `(i, j) in cache`: return `cache[(i, j)]`
   - If `s[i] == t[j]`:
     - `cache[(i, j)] = dfs(i + 1, j + 1) + dfs(i + 1, j)`
   - Else:
     - `cache[(i, j)] = dfs(i + 1, j)`
   - Return `cache[(i, j)]`
3. Return `dfs(0, 0)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        cache = {}
        
        def dfs(i, j):
            if j == len(t):
                return 1
            if i == len(s):
                return 0
            if (i, j) in cache:
                return cache[(i, j)]
                
            if s[i] == t[j]:
                cache[(i, j)] = dfs(i + 1, j + 1) + dfs(i + 1, j)
            else:
                cache[(i, j)] = dfs(i + 1, j)
                
            return cache[(i, j)]
            
        return dfs(0, 0)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M) - Where N = len(s) and M = len(t).`
- **Space Complexity:** `O(N * M) - Memoization table.`

---

## <a id="119-edit-distance"></a>119. Edit Distance

- **Difficulty:** `Medium`
- **Pattern:** `2D Levenshtein Distance Matrix`
- **LeetCode Reference:** [LeetCode #72](https://leetcode.com/problems/edit-distance/)

### 1. Problem Statement
Given two strings `word1` and `word2`, return the **minimum number of operations** required to convert `word1` to `word2`.

You have the following three operations permitted on a word:
- Insert a character
- Delete a character
- Replace a character

#### Examples:
**Example 1:**
```text
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: horse -> rorse (replace 'h' with 'r') -> rose (remove 'r') -> ros (remove 'e').
```

#### Constraints:
- `0 <= word1.length, word2.length <= 500`
- `word1 and word2 consist of lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Spell-checking: at `(i, j)`, if characters match, cost is 0 (`dp[i+1][j+1]`). Otherwise, take `1 + min(insert: dp[i][j+1], delete: dp[i+1][j], replace: dp[i+1][j+1])`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Base cases on 2D table boundaries: distance to convert empty string to word of length `k` is `k`.
- Hint 2: Bottom-up DP: if `word1[i] == word2[j]`: `dp[i][j] = dp[i+1][j+1]`. Else: `dp[i][j] = 1 + min(dp[i+1][j], dp[i][j+1], dp[i+1][j+1])`.

### 4. Detailed Approach Walkthrough
1. `dp = [[float("inf")] * (len(word2) + 1) for _ in range(len(word1) + 1)]`.
2. Base cases: fill bottom row and rightmost column with remaining lengths.
3. Iterate `i` and `j` backwards:
   - If `word1[i] == word2[j]`: `dp[i][j] = dp[i + 1][j + 1]`
   - Else: `dp[i][j] = 1 + min(dp[i + 1][j], dp[i][j + 1], dp[i + 1][j + 1])`
4. Return `dp[0][0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        dp = [[float("inf")] * (len(word2) + 1) for _ in range(len(word1) + 1)]
        
        for j in range(len(word2) + 1):
            dp[len(word1)][j] = len(word2) - j
        for i in range(len(word1) + 1):
            dp[i][len(word2)] = len(word1) - i
            
        for i in range(len(word1) - 1, -1, -1):
            for j in range(len(word2) - 1, -1, -1):
                if word1[i] == word2[j]:
                    dp[i][j] = dp[i + 1][j + 1]
                else:
                    dp[i][j] = 1 + min(dp[i + 1][j], dp[i][j + 1], dp[i + 1][j + 1])
                    
        return dp[0][0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M) - Table of size len(word1) * len(word2).`
- **Space Complexity:** `O(N * M) - 2D matrix.`

---

## <a id="120-burst-balloons"></a>120. Burst Balloons

- **Difficulty:** `Hard`
- **Pattern:** `Matrix Chain Multiplication DP (Reverse Thinking)`
- **LeetCode Reference:** [LeetCode #312](https://leetcode.com/problems/burst-balloons/)

### 1. Problem Statement
You are given `n` balloons, indexed from `0` to `n - 1`. Each balloon is painted with a number on it represented by an array `nums`. You are asked to burst all the balloons.

If you burst the `i-th` balloon, you will get `nums[i - 1] * nums[i] * nums[i + 1]` coins. If `i - 1` or `i + 1` goes out of bounds of the array, then treat it as if there is a balloon with a `1` painted on it.

Return the **maximum coins** you can collect by bursting the balloons wisely.

#### Examples:
**Example 1:**
```text
Input: nums = [3,1,5,8]
Output: 167
Explanation: Burst order: 1 -> 5 -> 3 -> 8. Coins = 3*1*5 + 3*5*8 + 1*3*8 + 1*8*1 = 167.
```

#### Constraints:
- `n == nums.length`
- `1 <= n <= 300`
- `0 <= nums[i] <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Reverse the thinking: instead of choosing which balloon to burst FIRST (which destroys boundaries and creates subproblems that depend on each other), choose which balloon to burst LAST in range `(l, r)`. The last balloon `i` is multiplied by the fixed outer boundaries `nums[l-1] * nums[i] * nums[r+1]`!

### 3. Step-by-Step Progressive Hints
- Hint 1: Pad `nums = [1] + nums + [1]`.
- Hint 2: For range `(l, r)`, iterate over all possible balloons `i` that will be burst LAST in this range.
- Hint 3: `coins = nums[l-1] * nums[i] * nums[r+1] + dfs(l, i-1) + dfs(i+1, r)`.

### 4. Detailed Approach Walkthrough
1. Pad array: `nums = [1] + [n for n in nums if n > 0] + [1]` (or keep 0s).
2. `dp = {}`.
3. Define `dfs(l, r)`:
   - If `l > r`: return 0
   - If `(l, r) in dp`: return `dp[(l, r)]`
   - `dp[(l, r)] = 0`
   - For `i` from `l` to `r`:
     - `coins = nums[l - 1] * nums[i] * nums[r + 1]`
     - `coins += dfs(l, i - 1) + dfs(i + 1, r)`
     - `dp[(l, r)] = max(dp[(l, r)], coins)`
   - Return `dp[(l, r)]`
4. Return `dfs(1, len(nums) - 2)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxCoins(self, nums: list[int]) -> int:
        nums = [1] + nums + [1]
        dp = {}
        
        def dfs(l, r):
            if l > r:
                return 0
            if (l, r) in dp:
                return dp[(l, r)]
                
            dp[(l, r)] = 0
            for i in range(l, r + 1):
                coins = nums[l - 1] * nums[i] * nums[r + 1]
                coins += dfs(l, i - 1) + dfs(i + 1, r)
                dp[(l, r)] = max(dp[(l, r)], coins)
                
            return dp[(l, r)]
            
        return dfs(1, len(nums) - 2)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n^3) - O(n^2) subproblems, each doing O(n) loop.`
- **Space Complexity:** `O(n^2) - Memoization table.`

---

## <a id="121-regular-expression-matching"></a>121. Regular Expression Matching

- **Difficulty:** `Hard`
- **Pattern:** `2D Regex Parsing DP`
- **LeetCode Reference:** [LeetCode #10](https://leetcode.com/problems/regular-expression-matching/)

### 1. Problem Statement
Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:
- `'.'` Matches any single character.
- `'*'` Matches **zero or more** of the preceding element.

The matching should cover the **entire** input string (not partial).

#### Examples:
**Example 1:**
```text
Input: s = "aa", p = "a*"
Output: true
Explanation: '*' repeats 'a' twice to match "aa".
```

**Example 2:**
```text
Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" matches any sequence of characters.
```

#### Constraints:
- `1 <= s.length <= 20`
- `1 <= p.length <= 20`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A regex parser state machine: `'.'` matches any single letter. `'*'` acts as a repeater allowing you either to skip the preceding character entirely (use 0 times: `dfs(i, j+2)`), or use it once and stay on the `'*'` state if current character matches (`dfs(i+1, j)`).

### 3. Step-by-Step Progressive Hints
- Hint 1: State is `(i, j)`. Base cases: if `i >= len(s)` and `j >= len(p)`, return True. If `j >= len(p)`, return False.
- Hint 2: Check `match = (i < len(s) and (s[i] == p[j] or p[j] == "."))`.
- Hint 3: If `(j + 1 < len(p) and p[j + 1] == "*")`: branch into `dfs(i, j + 2)` (don't use) or `(match and dfs(i + 1, j))` (use once).

### 4. Detailed Approach Walkthrough
1. `cache = {}`.
2. Define `dfs(i, j)`:
   - If `(i, j) in cache`: return `cache[(i, j)]`
   - If `i >= len(s) and j >= len(p)`: return `True`
   - If `j >= len(p)`: return `False`
   - `match = i < len(s) and (s[i] == p[j] or p[j] == ".")`
   - If `(j + 1) < len(p) and p[j + 1] == "*"`:
     - `cache[(i, j)] = (dfs(i, j + 2) or (match and dfs(i + 1, j)))`
     - Return `cache[(i, j)]`
   - If `match`:
     - `cache[(i, j)] = dfs(i + 1, j + 1)`
     - Return `cache[(i, j)]`
   - `cache[(i, j)] = False`
   - Return `False`
3. Return `dfs(0, 0)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        cache = {}
        
        def dfs(i, j):
            if (i, j) in cache:
                return cache[(i, j)]
            if i >= len(s) and j >= len(p):
                return True
            if j >= len(p):
                return False
                
            match = i < len(s) and (s[i] == p[j] or p[j] == ".")
            if (j + 1) < len(p) and p[j + 1] == "*":
                cache[(i, j)] = (dfs(i, j + 2) or          # Don't use *
                                 (match and dfs(i + 1, j))) # Use *
                return cache[(i, j)]
                
            if match:
                cache[(i, j)] = dfs(i + 1, j + 1)
                return cache[(i, j)]
                
            cache[(i, j)] = False
            return False
            
        return dfs(0, 0)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M) - Where N = len(s) and M = len(p).`
- **Space Complexity:** `O(N * M) - Memoization table and call stack.`

---
