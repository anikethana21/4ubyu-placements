# Chapter: 1-D Dynamic Programming

> 1-D Dynamic Programming breaks complex linear optimization problems into overlapping subproblems, memoizing or tabulating solutions to achieve polynomial runtimes.

**Total Questions in Topic:** 12

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 99 | [Climbing Stairs](#99-climbing-stairs) | **Easy** | `Fibonacci DP (Two Variables)` | [#70](https://leetcode.com/problems/climbing-stairs/) |
| 100 | [Min Cost Climbing Stairs](#100-min-cost-climbing-stairs) | **Easy** | `Bottom-Up Linear DP` | [#746](https://leetcode.com/problems/min-cost-climbing-stairs/) |
| 101 | [House Robber](#101-house-robber) | **Medium** | `Include / Exclude Linear DP` | [#198](https://leetcode.com/problems/house-robber/) |
| 102 | [House Robber II](#102-house-robber-ii) | **Medium** | `Circular Array DP Splitting` | [#213](https://leetcode.com/problems/house-robber-ii/) |
| 103 | [Longest Palindromic Substring](#103-longest-palindromic-substring) | **Medium** | `Expand Around Center` | [#5](https://leetcode.com/problems/longest-palindromic-substring/) |
| 104 | [Palindromic Substrings](#104-palindromic-substrings) | **Medium** | `Expand Around Center (Counting)` | [#647](https://leetcode.com/problems/palindromic-substrings/) |
| 105 | [Decode Ways](#105-decode-ways) | **Medium** | `1-D Dynamic Programming` | [#91](https://leetcode.com/problems/decode-ways/) |
| 106 | [Coin Change](#106-coin-change) | **Medium** | `Unbounded Knapsack DP (Bottom-Up)` | [#322](https://leetcode.com/problems/coin-change/) |
| 107 | [Maximum Product Subarray](#107-maximum-product-subarray) | **Medium** | `Min / Max Tracking DP` | [#152](https://leetcode.com/problems/maximum-product-subarray/) |
| 108 | [Word Break](#108-word-break) | **Medium** | `1-D Substring Matching DP` | [#139](https://leetcode.com/problems/word-break/) |
| 109 | [Longest Increasing Subsequence](#109-longest-increasing-subsequence) | **Medium** | `1-D DP (O(n^2)) or Patience Sorting Binary Search (O(n log n))` | [#300](https://leetcode.com/problems/longest-increasing-subsequence/) |
| 110 | [Partition Equal Subset Sum](#110-partition-equal-subset-sum) | **Medium** | `0/1 Knapsack (Subset Sum Target)` | [#416](https://leetcode.com/problems/partition-equal-subset-sum/) |

---

## <a id="99-climbing-stairs"></a>99. Climbing Stairs

- **Difficulty:** `Easy`
- **Pattern:** `Fibonacci DP (Two Variables)`
- **LeetCode Reference:** [LeetCode #70](https://leetcode.com/problems/climbing-stairs/)

### 1. Problem Statement
You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

#### Examples:
**Example 1:**
```text
Input: n = 2
Output: 2
Explanation: Two ways: 1 step + 1 step, or 2 steps.
```

**Example 2:**
```text
Input: n = 3
Output: 3
Explanation: Three ways: 1+1+1, 1+2, 2+1.
```

#### Constraints:
- `1 <= n <= 45`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> To reach step `n`, you must have come from either step `n-1` (with a 1-step hop) or step `n-2` (with a 2-step hop). Thus, `ways(n) = ways(n-1) + ways(n-2)`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Base cases: `ways(1) = 1`, `ways(2) = 2`.
- Hint 2: Compute iteratively using two variables `one = 1, two = 1` moving backwards.

### 4. Detailed Approach Walkthrough
1. Initialize `one, two = 1, 1`.
2. Loop `n - 1` times:
   - `temp = one`
   - `one = one + two`
   - `two = temp`
3. Return `one`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        one, two = 1, 1
        for i in range(n - 1):
            temp = one
            one = one + two
            two = temp
        return one
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single loop of n steps.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="100-min-cost-climbing-stairs"></a>100. Min Cost Climbing Stairs

- **Difficulty:** `Easy`
- **Pattern:** `Bottom-Up Linear DP`
- **LeetCode Reference:** [LeetCode #746](https://leetcode.com/problems/min-cost-climbing-stairs/)

### 1. Problem Statement
You are given an integer array `cost` where `cost[i]` is the cost of `i-th` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

Return the **minimum cost** to reach the top of the floor.

#### Examples:
**Example 1:**
```text
Input: cost = [10,15,20]
Output: 15
Explanation: Start at index 1 (cost 15), take two steps to reach top.
```

**Example 2:**
```text
Input: cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
Explanation: Optimal path steps on the 1s.
```

#### Constraints:
- `2 <= cost.length <= 1000`
- `0 <= cost[i] <= 999`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Starting from the top floor and working backwards: the minimum cost to climb past step `i` is `cost[i] + min(cost[i+1], cost[i+2])`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Append a 0 cost at the end representing the top floor.
- Hint 2: Iterate backwards: `cost[i] += min(cost[i + 1], cost[i + 2])`.
- Hint 3: Return `min(cost[0], cost[1])`.

### 4. Detailed Approach Walkthrough
1. Append `0` to `cost`.
2. Iterate `i` backwards from `len(cost) - 3` down to 0:
   - `cost[i] += min(cost[i + 1], cost[i + 2])`
3. Return `min(cost[0], cost[1])`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def minCostClimbingStairs(self, cost: list[int]) -> int:
        cost.append(0)
        for i in range(len(cost) - 3, -1, -1):
            cost[i] += min(cost[i + 1], cost[i + 2])
        return min(cost[0], cost[1])
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass in reverse.`
- **Space Complexity:** `O(1) - Modifies array in place.`

---

## <a id="101-house-robber"></a>101. House Robber

- **Difficulty:** `Medium`
- **Pattern:** `Include / Exclude Linear DP`
- **LeetCode Reference:** [LeetCode #198](https://leetcode.com/problems/house-robber/)

### 1. Problem Statement
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. Adjacent houses have security systems connected; it will automatically contact the police if **two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return the **maximum amount of money** you can rob tonight without alerting the police.

#### Examples:
**Example 1:**
```text
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3). Total = 4.
```

**Example 2:**
```text
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob 2 + 9 + 1 = 12.
```

#### Constraints:
- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> At each house `n`, you decide: either rob this house plus your best earnings from 2 houses ago (`n + rob1`), or skip this house and keep your best earnings from the adjacent house (`rob2`).

### 3. Step-by-Step Progressive Hints
- Hint 1: Recurrence relation: `maxRob(i) = max(nums[i] + maxRob(i - 2), maxRob(i - 1))`.
- Hint 2: Only maintain two variables `rob1 = 0, rob2 = 0`.

### 4. Detailed Approach Walkthrough
1. Initialize `rob1 = 0, rob2 = 0`.
2. For each `n` in `nums`:
   - `temp = max(n + rob1, rob2)`
   - `rob1 = rob2`
   - `rob2 = temp`
3. Return `rob2`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def rob(self, nums: list[int]) -> int:
        rob1, rob2 = 0, 0
        for n in nums:
            temp = max(n + rob1, rob2)
            rob1 = rob2
            rob2 = temp
        return rob2
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single linear pass.`
- **Space Complexity:** `O(1) - Two tracking variables.`

---

## <a id="102-house-robber-ii"></a>102. House Robber II

- **Difficulty:** `Medium`
- **Pattern:** `Circular Array DP Splitting`
- **LeetCode Reference:** [LeetCode #213](https://leetcode.com/problems/house-robber-ii/)

### 1. Problem Statement
You are a professional robber planning to rob houses along a street. All houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one.

Return the **maximum amount of money** you can rob tonight without alerting the police.

#### Examples:
**Example 1:**
```text
Input: nums = [2,3,2]
Output: 3
Explanation: Cannot rob house 1 and house 3 together because they are adjacent in a circle.
```

**Example 2:**
```text
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 and 3: 1 + 3 = 4.
```

#### Constraints:
- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Circular street dilemma: robbing House 0 forbids robbing House N-1. Therefore, run standard House Robber I on two separate slices: `nums[1:]` (excluding first house) and `nums[:-1]` (excluding last house), and take the maximum.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `len(nums) == 1`, return `nums[0]`.
- Hint 2: Compute `max(nums[0], helper(nums[1:]), helper(nums[:-1]))` using House Robber I helper.

### 4. Detailed Approach Walkthrough
1. If `len(nums) == 1`, return `nums[0]`.
2. Helper `helper(nums)`: House Robber I linear scan.
3. Return `max(nums[0], helper(nums[1:]), helper(nums[:-1]))`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def rob(self, nums: list[int]) -> int:
        return max(nums[0], self.helper(nums[1:]), self.helper(nums[:-1]))
        
    def helper(self, nums):
        rob1, rob2 = 0, 0
        for n in nums:
            newRob = max(rob1 + n, rob2)
            rob1 = rob2
            rob2 = newRob
        return rob2
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Two linear passes over n elements.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="103-longest-palindromic-substring"></a>103. Longest Palindromic Substring

- **Difficulty:** `Medium`
- **Pattern:** `Expand Around Center`
- **LeetCode Reference:** [LeetCode #5](https://leetcode.com/problems/longest-palindromic-substring/)

### 1. Problem Statement
Given a string `s`, return the **longest palindromic substring** in `s`.

#### Examples:
**Example 1:**
```text
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

**Example 2:**
```text
Input: s = "cbbd"
Output: "bb"
Explanation: "bb" is the longest palindrome.
```

#### Constraints:
- `1 <= s.length <= 1000`
- `s consist of only digits and English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Treat every character (and every space between two characters) as a potential center of symmetry. Expand outward like ripples on water as long as characters match.

### 3. Step-by-Step Progressive Hints
- Hint 1: There are `2n - 1` possible centers for palindromes (odd length centered at `i`, even length centered at `i, i+1`).
- Hint 2: Expand `l` left and `r` right while `s[l] == s[r]` and update longest substring found.

### 4. Detailed Approach Walkthrough
1. `res = "", resLen = 0`.
2. For each index `i` in `s`:
   - **Odd length**: `l = r = i`. While `l >= 0 and r < len(s) and s[l] == s[r]`:
     - If `(r - l + 1) > resLen`: `res = s[l : r + 1]; resLen = r - l + 1`
     - `l -= 1; r += 1`
   - **Even length**: `l = i, r = i + 1`. While `l >= 0 and r < len(s) and s[l] == s[r]`:
     - If `(r - l + 1) > resLen`: `res = s[l : r + 1]; resLen = r - l + 1`
     - `l -= 1; r += 1`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ""
        resLen = 0
        
        for i in range(len(s)):
            # Odd length
            l, r = i, i
            while l >= 0 and r < len(s) and s[l] == s[r]:
                if (r - l + 1) > resLen:
                    res = s[l : r + 1]
                    resLen = r - l + 1
                l -= 1
                r += 1
                
            # Even length
            l, r = i, i + 1
            while l >= 0 and r < len(s) and s[l] == s[r]:
                if (r - l + 1) > resLen:
                    res = s[l : r + 1]
                    resLen = r - l + 1
                l -= 1
                r += 1
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n^2) - n centers, each expanding up to O(n).`
- **Space Complexity:** `O(1) - Constant auxiliary memory.`

---

## <a id="104-palindromic-substrings"></a>104. Palindromic Substrings

- **Difficulty:** `Medium`
- **Pattern:** `Expand Around Center (Counting)`
- **LeetCode Reference:** [LeetCode #647](https://leetcode.com/problems/palindromic-substrings/)

### 1. Problem Statement
Given a string `s`, return the **number of palindromic substrings** in it.

A string is a **palindrome** when it reads the same backward as forward. A **substring** is a contiguous sequence of characters within the string.

#### Examples:
**Example 1:**
```text
Input: s = "abc"
Output: 3
Explanation: Three palindromic substrings: "a", "b", "c".
```

**Example 2:**
```text
Input: s = "aaa"
Output: 6
Explanation: Six palindromic substrings: "a", "a", "a", "aa", "aa", "aaa".
```

#### Constraints:
- `1 <= s.length <= 1000`
- `s consists of lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Expanding outward from every center point: every step `l` and `r` expand while matching contributes exactly +1 to the total palindrome count.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a helper `countPali(s, l, r)` expanding outward and incrementing count while `s[l] == s[r]`.
- Hint 2: Sum counts for all odd centers `countPali(s, i, i)` and even centers `countPali(s, i, i + 1)`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = 0`.
2. Helper `countPali(l, r)`: while `l >= 0 and r < len(s) and s[l] == s[r]`: `res += 1; l -= 1; r += 1`.
3. For `i` in range(`len(s)`): `countPali(i, i)` and `countPali(i, i + 1)`.
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        res = 0
        
        for i in range(len(s)):
            # Odd length
            l = r = i
            while l >= 0 and r < len(s) and s[l] == s[r]:
                res += 1
                l -= 1
                r += 1
                
            # Even length
            l = i
            r = i + 1
            while l >= 0 and r < len(s) and s[l] == s[r]:
                res += 1
                l -= 1
                r += 1
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n^2) - n centers expanding up to O(n).`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="105-decode-ways"></a>105. Decode Ways

- **Difficulty:** `Medium`
- **Pattern:** `1-D Dynamic Programming`
- **LeetCode Reference:** [LeetCode #91](https://leetcode.com/problems/decode-ways/)

### 1. Problem Statement
A message containing letters from A-Z can be encoded into numbers using the mapping: `'A' -> "1", 'B' -> "2", ... 'Z' -> "26"`.

To decode an encoded message, all digits must be grouped then mapped back into letters. For example, `"11106"` can be mapped into `"AAJF"` with `(1 1 10 6)` or `"KJF"` with `(11 10 6)`.

Given a string `s` containing only digits, return the **number of ways** to decode it.

#### Examples:
**Example 1:**
```text
Input: s = "12"
Output: 2
Explanation: "12" could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**
```text
Input: s = "226"
Output: 3
Explanation: "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

**Example 3:**
```text
Input: s = "06"
Output: 0
Explanation: "06" cannot be mapped to "F" because "6" is different from "06".
```

#### Constraints:
- `1 <= s.length <= 100`
- `s contains only digits and may contain leading zero(s).`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Parsing morse code without spaces: at each position, you can decode 1 digit if `s[i] != '0'`, and decode 2 digits if `10 <= int(s[i:i+2]) <= 26`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Base case: `dp[len(s)] = 1`. If `s[i] == '0'`, `dp[i] = 0`.
- Hint 2: Single digit decode: `dp[i] = dp[i + 1]`.
- Hint 3: Two digit decode: if `(i + 1 < len(s))` and `s[i] == '1' or (s[i] == '2' and s[i+1] in '0123456')`, add `dp[i + 2]`.

### 4. Detailed Approach Walkthrough
1. Initialize `dp = {len(s): 1}`.
2. Iterate `i` backwards from `len(s) - 1` down to 0:
   - If `s[i] == "0"`: `dp[i] = 0`
   - Else: `dp[i] = dp[i + 1]`
   - If `(i + 1 < len(s))` and `(s[i] == "1" or (s[i] == "2" and s[i + 1] in "0123456"))`:
     - `dp[i] += dp[i + 2]`
3. Return `dp[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def numDecodings(self, s: str) -> int:
        dp = {len(s): 1}
        
        for i in range(len(s) - 1, -1, -1):
            if s[i] == "0":
                dp[i] = 0
            else:
                dp[i] = dp[i + 1]
                
            if (i + 1 < len(s) and (s[i] == "1" or 
                (s[i] == "2" and s[i + 1] in "0123456"))):
                dp[i] += dp[i + 2]
                
        return dp[0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single backwards pass.`
- **Space Complexity:** `O(n) or O(1) by maintaining only two variables.`

---

## <a id="106-coin-change"></a>106. Coin Change

- **Difficulty:** `Medium`
- **Pattern:** `Unbounded Knapsack DP (Bottom-Up)`
- **LeetCode Reference:** [LeetCode #322](https://leetcode.com/problems/coin-change/)

### 1. Problem Statement
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the **fewest number of coins** that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

#### Examples:
**Example 1:**
```text
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1 (3 coins).
```

**Example 2:**
```text
Input: coins = [2], amount = 3
Output: -1
Explanation: Cannot make 3 using only 2s.
```

**Example 3:**
```text
Input: coins = [1], amount = 0
Output: 0
Explanation: 0 amount requires 0 coins.
```

#### Constraints:
- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 2^31 - 1`
- `0 <= amount <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Building a staircase to height `amount`: for every step `a` from 1 to `amount`, test taking one coin `c` of each denomination. `dp[a] = 1 + min(dp[a - c])`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Initialize `dp = [amount + 1] * (amount + 1)` with `dp[0] = 0`.
- Hint 2: For each amount `a` from 1 to `amount`: for each coin `c` in `coins`: if `a - c >= 0`, `dp[a] = min(dp[a], 1 + dp[a - c])`.
- Hint 3: Return `dp[amount]` if `dp[amount] != amount + 1` else `-1`.

### 4. Detailed Approach Walkthrough
1. Initialize `dp = [amount + 1] * (amount + 1)` and set `dp[0] = 0`.
2. For `a` in range(1, amount + 1):
   - For `c` in `coins`:
     - If `a - c >= 0`:
       - `dp[a] = min(dp[a], 1 + dp[a - c])`
3. Return `dp[amount]` if `dp[amount] != amount + 1` else `-1`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def coinChange(self, coins: list[int], amount: int) -> int:
        dp = [amount + 1] * (amount + 1)
        dp[0] = 0
        
        for a in range(1, amount + 1):
            for c in coins:
                if a - c >= 0:
                    dp[a] = min(dp[a], 1 + dp[a - c])
                    
        return dp[amount] if dp[amount] != amount + 1 else -1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(amount * len(coins)) - Nested loop over amounts and coins.`
- **Space Complexity:** `O(amount) - DP array.`

---

## <a id="107-maximum-product-subarray"></a>107. Maximum Product Subarray

- **Difficulty:** `Medium`
- **Pattern:** `Min / Max Tracking DP`
- **LeetCode Reference:** [LeetCode #152](https://leetcode.com/problems/maximum-product-subarray/)

### 1. Problem Statement
Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the **largest product**, and return the product.

#### Examples:
**Example 1:**
```text
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**
```text
Input: nums = [-2,0,-1]
Output: 0
Explanation: Result cannot be 2, because [-2,-1] is not a contiguous subarray.
```

#### Constraints:
- `1 <= nums.length <= 2 * 10^4`
- `-10 <= nums[i] <= 10`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Multiplying negative numbers flips signs: a negative number times a large negative product flips into a massive POSITIVE product. Therefore, you must track BOTH the running maximum AND running minimum products at each step.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain `curMax` and `curMin` initialized to 1.
- Hint 2: When encountering `n`, compute `temp = curMax * n`, update `curMax = max(n * curMax, n * curMin, n)`, and `curMin = min(temp, n * curMin, n)`.
- Hint 3: Update `res = max(res, curMax)`.

### 4. Detailed Approach Walkthrough
1. `res = max(nums)`, `curMin, curMax = 1, 1`.
2. For `n` in `nums`:
   - `tmp = curMax * n`
   - `curMax = max(n * curMax, n * curMin, n)`
   - `curMin = min(tmp, n * curMin, n)`
   - `res = max(res, curMax)`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxProduct(self, nums: list[int]) -> int:
        res = max(nums)
        curMin, curMax = 1, 1
        
        for n in nums:
            tmp = curMax * n
            curMax = max(n * curMax, n * curMin, n)
            curMin = min(tmp, n * curMin, n)
            res = max(res, curMax)
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single linear pass.`
- **Space Complexity:** `O(1) - Constant tracking variables.`

---

## <a id="108-word-break"></a>108. Word Break

- **Difficulty:** `Medium`
- **Pattern:** `1-D Substring Matching DP`
- **LeetCode Reference:** [LeetCode #139](https://leetcode.com/problems/word-break/)

### 1. Problem Statement
Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

#### Examples:
**Example 1:**
```text
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: "leetcode" can be segmented as "leet code".
```

**Example 2:**
```text
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: "apple pen apple".
```

#### Constraints:
- `1 <= s.length <= 300`
- `1 <= wordDict.length <= 1000`
- `1 <= wordDict[i].length <= 20`
- `s and wordDict[i] consist of only lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Starting from the end of the text and working backwards: `dp[i]` is True if some word `w` matches `s[i : i + len(w)]` and `dp[i + len(w)]` is also True.

### 3. Step-by-Step Progressive Hints
- Hint 1: Initialize `dp = [False] * (len(s) + 1)` and base case `dp[len(s)] = True`.
- Hint 2: Iterate `i` from `len(s) - 1` down to 0: for each `w` in `wordDict`, if `(i + len(w) <= len(s))` and `s[i : i + len(w)] == w`, set `dp[i] = dp[i + len(w)]`.

### 4. Detailed Approach Walkthrough
1. `dp = [False] * (len(s) + 1)`, `dp[len(s)] = True`.
2. For `i` in range(len(s) - 1, -1, -1):
   - For `w` in `wordDict`:
     - If `(i + len(w) <= len(s))` and `s[i : i + len(w)] == w`:
       - `dp[i] = dp[i + len(w)]`
       - If `dp[i]`: break
3. Return `dp[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def wordBreak(self, s: str, wordDict: list[str]) -> bool:
        dp = [False] * (len(s) + 1)
        dp[len(s)] = True
        
        for i in range(len(s) - 1, -1, -1):
            for w in wordDict:
                if (i + len(w)) <= len(s) and s[i : i + len(w)] == w:
                    dp[i] = dp[i + len(w)]
                if dp[i]:
                    break
                    
        return dp[0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M * K) - Where N = len(s), M = len(wordDict), K = average word length.`
- **Space Complexity:** `O(N) - DP array.`

---

## <a id="109-longest-increasing-subsequence"></a>109. Longest Increasing Subsequence

- **Difficulty:** `Medium`
- **Pattern:** `1-D DP (O(n^2)) or Patience Sorting Binary Search (O(n log n))`
- **LeetCode Reference:** [LeetCode #300](https://leetcode.com/problems/longest-increasing-subsequence/)

### 1. Problem Statement
Given an integer array `nums`, return the length of the **longest strictly increasing subsequence**.

#### Examples:
**Example 1:**
```text
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], length = 4.
```

**Example 2:**
```text
Input: nums = [0,1,0,3,2,3]
Output: 4
Explanation: LIS is [0,1,2,3].
```

#### Constraints:
- `1 <= nums.length <= 2500`
- `-10^4 <= nums[i] <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Patience Solitaire game: for each number, if it's larger than all card piles, place it as a new pile. Otherwise, place it on the leftmost pile whose top card is >= current number using binary search.

### 3. Step-by-Step Progressive Hints
- Hint 1: Standard DP: `LIS[i] = 1 + max([LIS[j] for j in range(i+1, n) if nums[i] < nums[j]])` in O(n^2).
- Hint 2: For O(n log n), maintain a dynamic array `sub`. Use `bisect_left` to find insertion point and replace or append.

### 4. Detailed Approach Walkthrough
1. Initialize `LIS = [1] * len(nums)`.
2. Iterate `i` from `len(nums) - 1` down to 0:
   - For `j` in range(`i + 1`, `len(nums)`):
     - If `nums[i] < nums[j]`:
       - `LIS[i] = max(LIS[i], 1 + LIS[j])`
3. Return `max(LIS)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def lengthOfLIS(self, nums: list[int]) -> int:
        LIS = [1] * len(nums)
        
        for i in range(len(nums) - 1, -1, -1):
            for j in range(i + 1, len(nums)):
                if nums[i] < nums[j]:
                    LIS[i] = max(LIS[i], 1 + LIS[j])
                    
        return max(LIS)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n^2) for standard DP, or O(n log n) with binary search (Patience Sorting).`
- **Space Complexity:** `O(n) - LIS DP array.`

---

## <a id="110-partition-equal-subset-sum"></a>110. Partition Equal Subset Sum

- **Difficulty:** `Medium`
- **Pattern:** `0/1 Knapsack (Subset Sum Target)`
- **LeetCode Reference:** [LeetCode #416](https://leetcode.com/problems/partition-equal-subset-sum/)

### 1. Problem Statement
Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or `false` otherwise.

#### Examples:
**Example 1:**
```text
Input: nums = [1,5,11,5]
Output: true
Explanation: Partition into [1, 5, 5] and [11].
```

**Example 2:**
```text
Input: nums = [1,2,3,5]
Output: false
Explanation: Cannot partition into equal sum subsets.
```

#### Constraints:
- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Splitting a treasure pile equally: if total value is odd, it is mathematically impossible to split equally. If even, the problem reduces to finding a subset summing to exactly `target = sum(nums) // 2`.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `sum(nums) % 2 != 0`, return False immediately.
- Hint 2: Use a hash set `dp = {0}` storing all reachable subset sums.
- Hint 3: For each number `n`, update `dp` with `t + n` for all `t` in `dp`. If `target` in `dp`, return True.

### 4. Detailed Approach Walkthrough
1. If `sum(nums) % 2 != 0`: return `False`.
2. `target = sum(nums) // 2`, `dp = set([0])`.
3. Iterate `i` backwards through `nums`:
   - `nextDP = set()`
   - For `t` in `dp`:
     - If `t + nums[i] == target`: return `True`
     - `nextDP.add(t + nums[i])`
     - `nextDP.add(t)`
   - `dp = nextDP`
4. Return `target in dp`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def canPartition(self, nums: list[int]) -> bool:
        if sum(nums) % 2:
            return False
            
        dp = set([0])
        target = sum(nums) // 2
        
        for i in range(len(nums) - 1, -1, -1):
            nextDP = set()
            for t in dp:
                if (t + nums[i]) == target:
                    return True
                nextDP.add(t + nums[i])
                nextDP.add(t)
            dp = nextDP
            
        return True if target in dp else False
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * sum(nums)) - Pseudo-polynomial 0/1 knapsack complexity.`
- **Space Complexity:** `O(sum(nums)) - Set storing reachable subset sums.`

---
