# Chapter: Backtracking

> Backtracking systematically explores solution decision trees, making choices, recursing, and reverting state (backtracking) when reaching dead ends or completed candidate paths.

**Total Questions in Topic:** 9

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 71 | [Subsets](#71-subsets) | **Medium** | `Include / Exclude Decision Tree` | [#78](https://leetcode.com/problems/subsets/) |
| 72 | [Combination Sum](#72-combination-sum) | **Medium** | `Unbounded Knapsack Backtracking` | [#39](https://leetcode.com/problems/combination-sum/) |
| 73 | [Permutations](#73-permutations) | **Medium** | `Recursive Element Insertion / Swapping` | [#46](https://leetcode.com/problems/permutations/) |
| 74 | [Subsets II](#74-subsets-ii) | **Medium** | `Backtracking with Duplicate Skipping` | [#90](https://leetcode.com/problems/subsets-ii/) |
| 75 | [Combination Sum II](#75-combination-sum-ii) | **Medium** | `Sorted Backtracking with Duplicate Pruning` | [#40](https://leetcode.com/problems/combination-sum-ii/) |
| 76 | [Word Search](#76-word-search) | **Medium** | `2D Grid Backtracking DFS` | [#79](https://leetcode.com/problems/word-search/) |
| 77 | [Palindrome Partitioning](#77-palindrome-partitioning) | **Medium** | `Backtracking Partition Search` | [#131](https://leetcode.com/problems/palindrome-partitioning/) |
| 78 | [Letter Combinations of a Phone Number](#78-letter-combinations-of-a-phone-number) | **Medium** | `Combinatorial Backtracking` | [#17](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) |
| 79 | [N-Queens](#79-n-queens) | **Hard** | `Row-by-Row Constraint Propagation` | [#51](https://leetcode.com/problems/n-queens/) |

---

## <a id="71-subsets"></a>71. Subsets

- **Difficulty:** `Medium`
- **Pattern:** `Include / Exclude Decision Tree`
- **LeetCode Reference:** [LeetCode #78](https://leetcode.com/problems/subsets/)

### 1. Problem Statement
Given an integer array `nums` of **unique** elements, return all possible subsets (the power set).

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

#### Examples:
**Example 1:**
```text
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
Explanation: 2^3 = 8 total unique subsets.
```

**Example 2:**
```text
Input: nums = [0]
Output: [[],[0]]
Explanation: Power set of single element.
```

#### Constraints:
- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- `All the numbers of nums are unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A binary switchboard: for every number `nums[i]`, you have a binary choice: either flip the switch ON (include `nums[i]` in the current subset) or OFF (exclude `nums[i]`).

### 3. Step-by-Step Progressive Hints
- Hint 1: At index `i`, branch into two recursive calls: one including `nums[i]` and one excluding it.
- Hint 2: Base case is `i >= len(nums)`, where we append a copy of `subset` to `res`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = []` and `subset = []`.
2. Define `dfs(i)`:
   - Base case: If `i >= len(nums)`: `res.append(subset.copy()); return`
   - Decision 1 (Include `nums[i]`): `subset.append(nums[i])`; `dfs(i + 1)`
   - Decision 2 (Exclude `nums[i]`): `subset.pop()`; `dfs(i + 1)`
3. Call `dfs(0)` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def subsets(self, nums: list[int]) -> list[list[int]]:
        res = []
        subset = []
        
        def dfs(i):
            if i >= len(nums):
                res.append(subset.copy())
                return
                
            # Decision to include nums[i]
            subset.append(nums[i])
            dfs(i + 1)
            
            # Decision NOT to include nums[i]
            subset.pop()
            dfs(i + 1)
            
        dfs(0)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n * 2^n) - Total of 2^n subsets generated, each taking O(n) to copy.`
- **Space Complexity:** `O(n) - Recursion depth bounded by n.`

---

## <a id="72-combination-sum"></a>72. Combination Sum

- **Difficulty:** `Medium`
- **Pattern:** `Unbounded Knapsack Backtracking`
- **LeetCode Reference:** [LeetCode #39](https://leetcode.com/problems/combination-sum/)

### 1. Problem Statement
Given an array of **distinct** integers `candidates` and a target integer `target`, return a list of all **unique combinations** of `candidates` where the chosen numbers sum to `target`. You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

#### Examples:
**Example 1:**
```text
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation: 2+2+3 = 7 and 7 = 7.
```

**Example 2:**
```text
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
Explanation: Combinations summing to 8.
```

#### Constraints:
- `1 <= candidates.length <= 30`
- `2 <= candidates[i] <= 40`
- `All elements of candidates are distinct.`
- `1 <= target <= 40`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> An ATM dispensing exact change: you can choose to dispense another $2 bill (staying on candidate $2), or decide you are done with $2 bills and move on to $3 bills.

### 3. Step-by-Step Progressive Hints
- Hint 1: At index `i`, we can either choose `candidates[i]` (and stay at index `i` to allow reuse) or skip `candidates[i]` (and advance to `i + 1`).
- Hint 2: If `total == target`, record combination. If `total > target` or `i >= len(candidates)`, backtrack.

### 4. Detailed Approach Walkthrough
1. Initialize `res = []`.
2. Define `dfs(i, cur, total)`:
   - If `total == target`: `res.append(cur.copy()); return`
   - If `i >= len(candidates)` or `total > target`: return
   - Include `candidates[i]`: `cur.append(candidates[i])`; `dfs(i, cur, total + candidates[i])`; `cur.pop()`
   - Exclude `candidates[i]`: `dfs(i + 1, cur, total)`
3. Call `dfs(0, [], 0)` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def combinationSum(self, candidates: list[int], target: int) -> list[list[int]]:
        res = []
        
        def dfs(i, cur, total):
            if total == target:
                res.append(cur.copy())
                return
            if i >= len(candidates) or total > target:
                return
                
            # Choose candidates[i]
            cur.append(candidates[i])
            dfs(i, cur, total + candidates[i])
            cur.pop()
            
            # Skip candidates[i]
            dfs(i + 1, cur, total)
            
        dfs(0, [], 0)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(2^(target / min_val)) - Bounded by recursion tree height `target / min(candidates)`.`
- **Space Complexity:** `O(target / min_val) - Recursion call stack depth.`

---

## <a id="73-permutations"></a>73. Permutations

- **Difficulty:** `Medium`
- **Pattern:** `Recursive Element Insertion / Swapping`
- **LeetCode Reference:** [LeetCode #46](https://leetcode.com/problems/permutations/)

### 1. Problem Statement
Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in **any order**.

#### Examples:
**Example 1:**
```text
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
Explanation: All 3! = 6 permutations.
```

#### Constraints:
- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- `All the integers of nums are unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Placing letters into empty mailbox slots: for the first slot you have `n` choices, for the second `n-1` choices, until all letters are slotted.

### 3. Step-by-Step Progressive Hints
- Hint 1: Base case: if `len(nums) == 1`, return `[nums.copy()]`.
- Hint 2: Pop `n = nums.pop(0)`, recursively find all permutations of the remaining elements, and insert `n` into every possible position of each sub-permutation.

### 4. Detailed Approach Walkthrough
1. Base case: If `len(nums) == 0`, return `[[]]`.
2. `perms = self.permute(nums[1:])`.
3. `res = []`.
4. For `p` in `perms`:
   - For `i` in range(`len(p) + 1`):
     - `p_copy = p.copy()`
     - `p_copy.insert(i, nums[0])`
     - `res.append(p_copy)`
5. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def permute(self, nums: list[int]) -> list[list[int]]:
        res = []
        
        if len(nums) == 1:
            return [nums.copy()]
            
        for i in range(len(nums)):
            n = nums.pop(0)
            perms = self.permute(nums)
            
            for p in perms:
                p.append(n)
            res.extend(perms)
            nums.append(n)
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n! * n) - Total of n! permutations, each taking O(n) to construct.`
- **Space Complexity:** `O(n!) - To store all permutations.`

---

## <a id="74-subsets-ii"></a>74. Subsets II

- **Difficulty:** `Medium`
- **Pattern:** `Backtracking with Duplicate Skipping`
- **LeetCode Reference:** [LeetCode #90](https://leetcode.com/problems/subsets-ii/)

### 1. Problem Statement
Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set).

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

#### Examples:
**Example 1:**
```text
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
Explanation: Duplicates [1,2] and [2] are not repeated.
```

#### Constraints:
- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Sorting identical twins in line: if you decide not to invite the first twin `2`, you must also skip all other identical twin `2`s at this decision level to avoid generating duplicate guest lists.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort `nums` first so duplicates are adjacent.
- Hint 2: When skipping `nums[i]`, advance `i` while `i + 1 < len(nums) and nums[i] == nums[i + 1]`.

### 4. Detailed Approach Walkthrough
1. Sort `nums`.
2. Define `dfs(i, subset)`:
   - If `i == len(nums)`: `res.append(subset.copy()); return`
   - Include `nums[i]`: `subset.append(nums[i])`; `dfs(i + 1, subset)`; `subset.pop()`
   - Skip all duplicates of `nums[i]`: while `i + 1 < len(nums)` and `nums[i] == nums[i + 1]`: `i += 1`
   - Exclude: `dfs(i + 1, subset)`
3. Call `dfs(0, [])` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def subsetsWithDup(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()
        
        def backtrack(i, subset):
            if i == len(nums):
                res.append(subset.copy())
                return
                
            # All subsets that include nums[i]
            subset.append(nums[i])
            backtrack(i + 1, subset)
            subset.pop()
            
            # All subsets that don't include nums[i]
            while i + 1 < len(nums) and nums[i] == nums[i + 1]:
                i += 1
            backtrack(i + 1, subset)
            
        backtrack(0, [])
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n * 2^n) - Upper bound of power set generation.`
- **Space Complexity:** `O(n) - Call stack depth.`

---

## <a id="75-combination-sum-ii"></a>75. Combination Sum II

- **Difficulty:** `Medium`
- **Pattern:** `Sorted Backtracking with Duplicate Pruning`
- **LeetCode Reference:** [LeetCode #40](https://leetcode.com/problems/combination-sum-ii/)

### 1. Problem Statement
Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

Note: The solution set must not contain duplicate combinations.

#### Examples:
**Example 1:**
```text
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: [[1,1,6],[1,2,5],[1,7],[2,6]]
Explanation: Unique combinations summing to 8.
```

#### Constraints:
- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Choosing ingredients for a recipe from a basket with duplicate items: you sort items first, and if you reject an onion at the current selection step, you skip all remaining duplicate onions in that round.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort `candidates`.
- Hint 2: In the loop `for i in range(pos, len(candidates))`, if `i > pos and candidates[i] == candidates[i - 1]`, `continue`.
- Hint 3: If `candidates[i] > target`, break early (prune search space).

### 4. Detailed Approach Walkthrough
1. Sort `candidates`.
2. Initialize `res = []`.
3. Define `backtrack(cur, pos, target)`:
   - If `target == 0`: `res.append(cur.copy()); return`
   - If `target <= 0`: return
   - `prev = -1`
   - For `i` from `pos` to `len(candidates) - 1`:
     - If `candidates[i] == prev`: continue
     - If `candidates[i] > target`: break
     - `cur.append(candidates[i])`
     - `backtrack(cur, i + 1, target - candidates[i])`
     - `cur.pop()`
     - `prev = candidates[i]`
4. Call `backtrack([], 0, target)` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def combinationSum2(self, candidates: list[int], target: int) -> list[list[int]]:
        candidates.sort()
        res = []
        
        def backtrack(cur, pos, target):
            if target == 0:
                res.append(cur.copy())
                return
            if target <= 0:
                return
                
            prev = -1
            for i in range(pos, len(candidates)):
                if candidates[i] == prev:
                    continue
                if candidates[i] > target:
                    break
                cur.append(candidates[i])
                backtrack(cur, i + 1, target - candidates[i])
                cur.pop()
                prev = candidates[i]
                
        backtrack([], 0, target)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(2^n) - In the worst case.`
- **Space Complexity:** `O(n) - Maximum recursive stack depth.`

---

## <a id="76-word-search"></a>76. Word Search

- **Difficulty:** `Medium`
- **Pattern:** `2D Grid Backtracking DFS`
- **LeetCode Reference:** [LeetCode #79](https://leetcode.com/problems/word-search/)

### 1. Problem Statement
Given an `m x n` grid of characters `board` and a string `word`, return `true` if `word` exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

#### Examples:
**Example 1:**
```text
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
Explanation: Path A -> B -> C -> C -> E -> D exists on board.
```

**Example 2:**
```text
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
Explanation: Cannot reuse cell 'B'.
```

#### Constraints:
- `m == board.length, n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board and word consist of only lowercase and uppercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Walking through a labyrinth matching letters step-by-step: at each step, temporarily mark the stone with chalk (`path.add((r, c))`) so you don't step on it again, explore 4 neighboring directions, and erase the chalk mark (`path.remove((r, c))`) when backtracking.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `word[i] != board[r][c]` or `(r, c)` in path, return False.
- Hint 2: Base case: if `i == len(word)`, return True.
- Hint 3: Explore 4 directions `(r+1,c), (r-1,c), (r,c+1), (r,c-1)` and clean up `path.remove((r, c))`.

### 4. Detailed Approach Walkthrough
1. `ROWS, COLS = len(board), len(board[0])`, `path = set()`.
2. Define `dfs(r, c, i)`:
   - If `i == len(word)`: return `True`
   - If `r < 0 or c < 0 or r >= ROWS or c >= COLS or board[r][c] != word[i] or (r, c) in path`: return `False`
   - `path.add((r, c))`
   - `res = (dfs(r + 1, c, i + 1) or dfs(r - 1, c, i + 1) or dfs(r, c + 1, i + 1) or dfs(r, c - 1, i + 1))`
   - `path.remove((r, c))`
   - Return `res`
3. Loop over all `r, c`: if `dfs(r, c, 0)`: return `True`.
4. Return `False`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def exist(self, board: list[list[str]], word: str) -> bool:
        ROWS, COLS = len(board), len(board[0])
        path = set()
        
        def dfs(r, c, i):
            if i == len(word):
                return True
            if (r < 0 or c < 0 or 
                r >= ROWS or c >= COLS or 
                board[r][c] != word[i] or 
                (r, c) in path):
                return False
                
            path.add((r, c))
            res = (dfs(r + 1, c, i + 1) or
                   dfs(r - 1, c, i + 1) or
                   dfs(r, c + 1, i + 1) or
                   dfs(r, c - 1, i + 1))
            path.remove((r, c))
            return res
            
        for r in range(ROWS):
            for c in range(COLS):
                if dfs(r, c, 0):
                    return True
        return False
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M * 4^L) - Where N*M is grid size and L is word length.`
- **Space Complexity:** `O(L) - Recursion stack depth equals length of word.`

---

## <a id="77-palindrome-partitioning"></a>77. Palindrome Partitioning

- **Difficulty:** `Medium`
- **Pattern:** `Backtracking Partition Search`
- **LeetCode Reference:** [LeetCode #131](https://leetcode.com/problems/palindrome-partitioning/)

### 1. Problem Statement
Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**.

Return *all possible palindrome partitioning of* `s`.

#### Examples:
**Example 1:**
```text
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
Explanation: Valid palindrome partitionings.
```

**Example 2:**
```text
Input: s = "a"
Output: [["a"]]
Explanation: Single character.
```

#### Constraints:
- `1 <= s.length <= 16`
- `s contains only lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Cutting a loaf of bread into slices: you can make a cut at index `j` only if the resulting slice `s[i:j+1]` is a palindrome. Then repeat cutting the remaining loaf.

### 3. Step-by-Step Progressive Hints
- Hint 1: At index `i`, try every end index `j` from `i` to `len(s) - 1`.
- Hint 2: If `s[i:j+1]` is a palindrome (`self.isPali(s, i, j)`), append it to `part`, recurse `dfs(j + 1)`, and backtrack `part.pop()`.
- Hint 3: Base case: if `i >= len(s)`, record a copy of `part`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = []` and `part = []`.
2. Define `dfs(i)`:
   - If `i >= len(s)`: `res.append(part.copy()); return`
   - For `j` from `i` to `len(s) - 1`:
     - If `self.isPali(s, i, j)`:
       - `part.append(s[i : j + 1])`
       - `dfs(j + 1)`
       - `part.pop()`
3. Helper `isPali(s, l, r)`: checks if `s[l..r]` is a palindrome with two pointers.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def partition(self, s: str) -> list[list[str]]:
        res = []
        part = []
        
        def dfs(i):
            if i >= len(s):
                res.append(part.copy())
                return
            for j in range(i, len(s)):
                if self.isPali(s, i, j):
                    part.append(s[i : j + 1])
                    dfs(j + 1)
                    part.pop()
                    
        dfs(0)
        return res
        
    def isPali(self, s, l, r):
        while l < r:
            if s[l] != s[r]:
                return False
            l, r = l + 1, r - 1
        return True
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n * 2^n) - Total of 2^(n-1) possible partition points, O(n) palindrome check.`
- **Space Complexity:** `O(n) - Maximum recursion call depth.`

---

## <a id="78-letter-combinations-of-a-phone-number"></a>78. Letter Combinations of a Phone Number

- **Difficulty:** `Medium`
- **Pattern:** `Combinatorial Backtracking`
- **LeetCode Reference:** [LeetCode #17](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

### 1. Problem Statement
Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters:
- `2: abc, 3: def, 4: ghi, 5: jkl, 6: mno, 7: pqrs, 8: tuv, 9: wxyz`

#### Examples:
**Example 1:**
```text
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
Explanation: All 9 letter pairings.
```

**Example 2:**
```text
Input: digits = ""
Output: []
Explanation: Empty input produces empty list.
```

#### Constraints:
- `0 <= digits.length <= 4`
- `digits[i] is a digit in the range ['2', '9'].`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Dialing on an old T9 keypad: for each digit button pressed, you explore branches for every letter imprinted on that button.

### 3. Step-by-Step Progressive Hints
- Hint 1: Map digits to letters using a hash map `{"2": "abc", "3": "def", ...}`.
- Hint 2: Recursive state: `backtrack(i, curStr)`. If `len(curStr) == len(digits)`, append `curStr` to `res`.
- Hint 3: Iterate through characters of `digitToChar[digits[i]]` and recurse `backtrack(i + 1, curStr + c)`.

### 4. Detailed Approach Walkthrough
1. If `not digits`: return `[]`.
2. Map digits: `digitToChar = {"2": "abc", "3": "def", "4": "ghi", "5": "jkl", "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"}`.
3. Initialize `res = []`.
4. Define `backtrack(i, curStr)`:
   - If `len(curStr) == len(digits)`: `res.append(curStr); return`
   - For `c` in `digitToChar[digits[i]]`: `backtrack(i + 1, curStr + c)`
5. Call `backtrack(0, "")` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def letterCombinations(self, digits: str) -> list[str]:
        res = []
        digitToChar = {
            "2": "abc", "3": "def", "4": "ghi", "5": "jkl",
            "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"
        }
        
        def backtrack(i, curStr):
            if len(curStr) == len(digits):
                res.append(curStr)
                return
            for c in digitToChar[digits[i]]:
                backtrack(i + 1, curStr + c)
                
        if digits:
            backtrack(0, "")
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n * 4^n) - Where n is length of digits string.`
- **Space Complexity:** `O(n) - Maximum depth of recursion.`

---

## <a id="79-n-queens"></a>79. N-Queens

- **Difficulty:** `Hard`
- **Pattern:** `Row-by-Row Constraint Propagation`
- **LeetCode Reference:** [LeetCode #51](https://leetcode.com/problems/n-queens/)

### 1. Problem Statement
The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return *all distinct solutions to the **n-queens puzzle***. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

#### Examples:
**Example 1:**
```text
Input: n = 4
Output: [[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]]
Explanation: Two distinct valid configurations.
```

**Example 2:**
```text
Input: n = 1
Output: [["Q"]]
Explanation: Single queen on 1x1 board.
```

#### Constraints:
- `1 <= n <= 9`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Placing one queen per row: a queen attacks horizontally (prevented by placing exactly one queen per row), vertically (tracked by `cols` set), positive diagonally `(r + c)` (tracked by `posDiag` set), and negative diagonally `(r - c)` (tracked by `negDiag` set).

### 3. Step-by-Step Progressive Hints
- Hint 1: Place queens row by row (`r = 0..n-1`).
- Hint 2: Use three sets: `cols`, `posDiag = r + c`, `negDiag = r - c` for O(1) conflict validation.
- Hint 3: When placing a queen at `(r, c)`, add to all 3 sets. Recurse to `r + 1`, then remove from all 3 sets upon backtracking.

### 4. Detailed Approach Walkthrough
1. Initialize `col = set()`, `posDiag = set()`, `negDiag = set()`, `res = []`.
2. Create board: `board = [["."] * n for _ in range(n)]`.
3. Define `backtrack(r)`:
   - If `r == n`: append `["".join(row) for row in board]` to `res`; return
   - For `c` in range(`n`):
     - If `c in col or (r + c) in posDiag or (r - c) in negDiag`: continue
     - Place queen: `col.add(c); posDiag.add(r + c); negDiag.add(r - c); board[r][c] = "Q"`
     - `backtrack(r + 1)`
     - Remove queen: `col.remove(c); posDiag.remove(r + c); negDiag.remove(r - c); board[r][c] = "."`
4. Call `backtrack(0)` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def solveNQueens(self, n: int) -> list[list[str]]:
        col = set()
        posDiag = set()  # (r + c)
        negDiag = set()  # (r - c)
        
        res = []
        board = [["."] * n for _ in range(n)]
        
        def backtrack(r):
            if r == n:
                copy = ["".join(row) for row in board]
                res.append(copy)
                return
                
            for c in range(n):
                if c in col or (r + c) in posDiag or (r - c) in negDiag:
                    continue
                    
                col.add(c)
                posDiag.add(r + c)
                negDiag.add(r - c)
                board[r][c] = "Q"
                
                backtrack(r + 1)
                
                col.remove(c)
                posDiag.remove(r + c)
                negDiag.remove(r - c)
                board[r][c] = "."
                
        backtrack(0)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n!) - Placing queens row by row reduces available columns factorial-style.`
- **Space Complexity:** `O(n^2) - To store board state and recursion tree of depth n.`

---
