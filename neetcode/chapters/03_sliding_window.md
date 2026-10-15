# Chapter: Sliding Window

> Sliding Window maintains a contiguous subsegment of an array or string that dynamically expands and contracts to optimize continuous subarray/substring problems in O(n) linear time.

**Total Questions in Topic:** 6

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 15 | [Best Time to Buy and Sell Stock](#15-best-time-to-buy-and-sell-stock) | **Easy** | `Sliding Window / Two Pointers` | [#121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) |
| 16 | [Longest Substring Without Repeating Characters](#16-longest-substring-without-repeating-characters) | **Medium** | `Dynamic Sliding Window + Set` | [#3](https://leetcode.com/problems/longest-substring-without-repeating-characters/) |
| 17 | [Longest Repeating Character Replacement](#17-longest-repeating-character-replacement) | **Medium** | `Sliding Window + Frequency Tracking` | [#424](https://leetcode.com/problems/longest-repeating-character-replacement/) |
| 18 | [Permutation in String](#18-permutation-in-string) | **Medium** | `Fixed-Size Sliding Window + Match Counter` | [#567](https://leetcode.com/problems/permutation-in-string/) |
| 19 | [Minimum Window Substring](#19-minimum-window-substring) | **Hard** | `Dynamic Sliding Window + Condition Met` | [#76](https://leetcode.com/problems/minimum-window-substring/) |
| 20 | [Sliding Window Maximum](#20-sliding-window-maximum) | **Hard** | `Monotonic Decreasing Deque` | [#239](https://leetcode.com/problems/sliding-window-maximum/) |

---

## <a id="15-best-time-to-buy-and-sell-stock"></a>15. Best Time to Buy and Sell Stock

- **Difficulty:** `Easy`
- **Pattern:** `Sliding Window / Two Pointers`
- **LeetCode Reference:** [LeetCode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

### 1. Problem Statement
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i-th` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return `0`.

#### Examples:
**Example 1:**
```text
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6 - 1 = 5.
```

**Example 2:**
```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and max profit = 0.
```

#### Constraints:
- `1 <= prices.length <= 10^5`
- `0 <= prices[i] <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine tracking historical commodity prices. As you walk forward through the calendar, you always remember the cheapest bargain day you've seen so far. Every day you compare today's selling price against that lowest historical dip.

### 3. Step-by-Step Progressive Hints
- Hint 1: You can only sell on a day AFTER you buy.
- Hint 2: Track the lowest buying price seen so far as you iterate through the list.
- Hint 3: At each day `prices[r]`, calculate `profit = prices[r] - min_price` and update `max_profit`.

### 4. Detailed Approach Walkthrough
1. Initialize `l = 0` (buy day) and `r = 1` (sell day), `maxP = 0`.
2. While `r < len(prices)`:
   - If `prices[l] < prices[r]` (profitable transaction), calculate `profit = prices[r] - prices[l]` and update `maxP = max(maxP, profit)`.
   - If `prices[r] <= prices[l]` (found a lower buy price), update `l = r`.
   - Increment `r += 1`.
3. Return `maxP`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        l, r = 0, 1  # l=buy, r=sell
        maxP = 0
        
        while r < len(prices):
            if prices[l] < prices[r]:
                profit = prices[r] - prices[l]
                maxP = max(maxP, profit)
            else:
                l = r
            r += 1
            
        return maxP
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass through the prices array.`
- **Space Complexity:** `O(1) - Constant extra space.`

---

## <a id="16-longest-substring-without-repeating-characters"></a>16. Longest Substring Without Repeating Characters

- **Difficulty:** `Medium`
- **Pattern:** `Dynamic Sliding Window + Set`
- **LeetCode Reference:** [LeetCode #3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### 1. Problem Statement
Given a string `s`, find the length of the **longest substring** without repeating characters.

#### Examples:
**Example 1:**
```text
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**
```text
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**
```text
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with length 3.
```

#### Constraints:
- `0 <= s.length <= 5 * 10^4`
- `s consists of English letters, digits, symbols and spaces.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine an expanding zoom lens over the text. As you extend the right border of the lens, if a duplicate letter appears inside the frame, you shrink the left border of the lens until that duplicate letter is ejected from the view.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a sliding window with left pointer `l` and right pointer `r`.
- Hint 2: Use a hash set `charSet` to keep track of unique characters in the current window `s[l..r]`.
- Hint 3: If `s[r]` is already in `charSet`, remove `s[l]` and increment `l` until `s[r]` is no longer in `charSet`.

### 4. Detailed Approach Walkthrough
1. Initialize `charSet = set()`, `l = 0`, `res = 0`.
2. Iterate `r` from `0` to `len(s) - 1`:
   - While `s[r]` is in `charSet`:
     - Remove `s[l]` from `charSet`
     - `l += 1`
   - Add `s[r]` to `charSet`.
   - Update `res = max(res, r - l + 1)`.
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        charSet = set()
        l = 0
        res = 0
        
        for r in range(len(s)):
            while s[r] in charSet:
                charSet.remove(s[l])
                l += 1
            charSet.add(s[r])
            res = max(res, r - l + 1)
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Each character is inserted and removed from the set at most once.`
- **Space Complexity:** `O(min(n, m)) - Where m is the size of the character set (e.g. 128 for ASCII).`

---

## <a id="17-longest-repeating-character-replacement"></a>17. Longest Repeating Character Replacement

- **Difficulty:** `Medium`
- **Pattern:** `Sliding Window + Frequency Tracking`
- **LeetCode Reference:** [LeetCode #424](https://leetcode.com/problems/longest-repeating-character-replacement/)

### 1. Problem Statement
You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

#### Examples:
**Example 1:**
```text
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa to get "AAAA" or "BBBB".
```

**Example 2:**
```text
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the middle 'A' to form "AABBBBA" -> substring "BBBB" has length 4.
```

#### Constraints:
- `1 <= s.length <= 10^5`
- `s consists of only uppercase English letters.`
- `0 <= k <= s.length`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> In any window of size `W`, if the most popular character appears `maxF` times, the number of replacements needed to make the entire window identical is `W - maxF`. As long as `(window_length - maxF) <= k`, the window is valid.

### 3. Step-by-Step Progressive Hints
- Hint 1: A window of length `(r - l + 1)` is valid if `(r - l + 1) - max_frequency <= k`.
- Hint 2: Use a frequency hash map and track `maxF = max(count.values())`.
- Hint 3: If `(r - l + 1) - maxF > k`, increment `l` and decrement `count[s[l]]`.

### 4. Detailed Approach Walkthrough
1. Initialize `count = {}`, `res = 0`, `l = 0`, `maxf = 0`.
2. Iterate `r` across `s`:
   - `count[s[r]] = 1 + count.get(s[r], 0)`
   - `maxf = max(maxf, count[s[r]])`
   - While `(r - l + 1) - maxf > k`:
     - `count[s[l]] -= 1`
     - `l += 1`
   - `res = max(res, r - l + 1)`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = {}
        res = 0
        l = 0
        maxf = 0
        
        for r in range(len(s)):
            count[s[r]] = 1 + count.get(s[r], 0)
            maxf = max(maxf, count[s[r]])
            
            while (r - l + 1) - maxf > k:
                count[s[l]] -= 1
                l += 1
                
            res = max(res, r - l + 1)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass over string `s`.`
- **Space Complexity:** `O(26) = O(1) - Only 26 uppercase English letters stored in the hash map.`

---

## <a id="18-permutation-in-string"></a>18. Permutation in String

- **Difficulty:** `Medium`
- **Pattern:** `Fixed-Size Sliding Window + Match Counter`
- **LeetCode Reference:** [LeetCode #567](https://leetcode.com/problems/permutation-in-string/)

### 1. Problem Statement
Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

#### Examples:
**Example 1:**
```text
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**
```text
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
Explanation: No permutation of "ab" exists as a contiguous substring in s2.
```

#### Constraints:
- `1 <= s1.length, s2.length <= 10^4`
- `s1 and s2 consist of lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A permutation is just an anagram of fixed length `len(s1)`. Slide a stencil of length `len(s1)` across `s2`. Instead of rechecking all 26 letter counts at each step, maintain a `matches` counter indicating how many of the 26 characters have identical counts in both the stencil and `s1`.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `len(s1) > len(s2)`, return False immediately.
- Hint 2: A window of size `len(s1)` moves across `s2`. We need `s1_count == s2_window_count`.
- Hint 3: Maintain a `matches` variable (0 to 26). When sliding the window, update counts for the incoming and outgoing characters and adjust `matches` accordingly in O(1).

### 4. Detailed Approach Walkthrough
1. If `len(s1) > len(s2)`, return `False`.
2. Initialize two 26-element arrays `s1Count` and `s2Count`.
3. Populate counts for the first `len(s1)` characters of both strings.
4. Count initial `matches` (how many indices `0..25` have `s1Count[i] == s2Count[i]`).
5. Slide the window from `len(s1)` to `len(s2)`:
   - If `matches == 26`, return `True`.
   - Add character at `r`, update `s2Count` and `matches`.
   - Remove character at `l`, update `s2Count` and `matches`.
   - Increment `l += 1`.
6. Return `matches == 26`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        if len(s1) > len(s2):
            return False
            
        s1Count, s2Count = [0] * 26, [0] * 26
        for i in range(len(s1)):
            s1Count[ord(s1[i]) - ord('a')] += 1
            s2Count[ord(s2[i]) - ord('a')] += 1
            
        matches = 0
        for i in range(26):
            matches += (1 if s1Count[i] == s2Count[i] else 0)
            
        l = 0
        for r in range(len(s1), len(s2)):
            if matches == 26:
                return True
                
            # Add character at right
            index = ord(s2[r]) - ord('a')
            s2Count[index] += 1
            if s1Count[index] == s2Count[index]:
                matches += 1
            elif s1Count[index] + 1 == s2Count[index]:
                matches -= 1
                
            # Remove character at left
            index = ord(s2[l]) - ord('a')
            s2Count[index] -= 1
            if s1Count[index] == s2Count[index]:
                matches += 1
            elif s1Count[index] - 1 == s2Count[index]:
                matches -= 1
            l += 1
            
        return matches == 26
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Where n is the length of s2.`
- **Space Complexity:** `O(1) - Fixed 26-element arrays.`

---

## <a id="19-minimum-window-substring"></a>19. Minimum Window Substring

- **Difficulty:** `Hard`
- **Pattern:** `Dynamic Sliding Window + Condition Met`
- **LeetCode Reference:** [LeetCode #76](https://leetcode.com/problems/minimum-window-substring/)

### 1. Problem Statement
Given two strings `s` and `t` of lengths `m` and `n` respectively, return the **minimum window substring** of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

#### Examples:
**Example 1:**
```text
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

**Example 2:**
```text
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
```

**Example 3:**
```text
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window, which is impossible.
```

#### Constraints:
- `m == s.length, n == t.length`
- `1 <= m, n <= 10^5`
- `s and t consist of uppercase and lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine shopping for an exact recipe ingredients checklist `t`. You move your shopping cart down aisle `s` adding items. As soon as your cart satisfies all required ingredients (`have == need`), you try discarding unnecessary items from the back of your cart (`l`) to make the package as compact and cheap as possible.

### 3. Step-by-Step Progressive Hints
- Hint 1: Build a frequency map `countT` of string `t`.
- Hint 2: Track `have` (number of unique chars satisfying required count) and `need = len(countT)`.
- Hint 3: Expand `r` until `have == need`. Then shrink `l` while updating minimum window length until the condition breaks.

### 4. Detailed Approach Walkthrough
1. If `t == ""`, return `""`.
2. Populate `countT` with char counts of `t`, and set `need = len(countT)`.
3. Initialize `window = {}`, `have = 0`, `res = [-1, -1]`, `resLen = float('inf')`, `l = 0`.
4. Expand `r` from 0 to `len(s) - 1`:
   - Add `c = s[r]` to `window`.
   - If `c` in `countT` and `window[c] == countT[c]`: `have += 1`.
   - While `have == need`:
     - If `(r - l + 1) < resLen`: record `res = [l, r]` and `resLen = r - l + 1`.
     - Pop `s[l]` from `window`. If `s[l]` in `countT` and `window[s[l]] < countT[s[l]]`: `have -= 1`.
     - Increment `l += 1`.
5. Return `s[res[0] : res[1] + 1]` if `resLen != float('inf')` else `""`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if t == "":
            return ""
            
        countT, window = {}, {}
        for c in t:
            countT[c] = 1 + countT.get(c, 0)
            
        have, need = 0, len(countT)
        res, resLen = [-1, -1], float("inf")
        l = 0
        
        for r in range(len(s)):
            c = s[r]
            window[c] = 1 + window.get(c, 0)
            
            if c in countT and window[c] == countT[c]:
                have += 1
                
            while have == need:
                # Update our result
                if (r - l + 1) < resLen:
                    res = [l, r]
                    resLen = (r - l + 1)
                # Pop from the left of our window
                window[s[l]] -= 1
                if s[l] in countT and window[s[l]] < countT[s[l]]:
                    have -= 1
                l += 1
                
        l, r = res
        return s[l : r + 1] if resLen != float("inf") else ""
```

### 6. Complexity Analysis
- **Time Complexity:** `O(m + n) - Where m = len(s) and n = len(t). Each character in s is visited at most twice.`
- **Space Complexity:** `O(m + n) - For storing character count dictionaries.`

---

## <a id="20-sliding-window-maximum"></a>20. Sliding Window Maximum

- **Difficulty:** `Hard`
- **Pattern:** `Monotonic Decreasing Deque`
- **LeetCode Reference:** [LeetCode #239](https://leetcode.com/problems/sliding-window-maximum/)

### 1. Problem Statement
You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return the **max sliding window**.

#### Examples:
**Example 1:**
```text
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: Window position -> Max: [1 3 -1] -> 3; [3 -1 -3] -> 3; [-1 -3 5] -> 5; [-3 5 3] -> 5; [5 3 6] -> 6; [3 6 7] -> 7.
```

**Example 2:**
```text
Input: nums = [1], k = 1
Output: [1]
Explanation: Single window produces [1].
```

#### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a sports team recruitment window of size `k`. If a new recruit arrives who is younger AND more skilled than older players currently sitting on the bench, those older, less-skilled players will NEVER be the top player in any future window. You can immediately cut them from the queue.

### 3. Step-by-Step Progressive Hints
- Hint 1: A max-heap gives O(n log k). Can we achieve O(n) using a Double-Ended Queue (`collections.deque`)?
- Hint 2: Maintain a monotonically decreasing deque of *indices*. The front of the deque `q[0]` always holds the index of the maximum element.
- Hint 3: When adding `nums[r]`, pop from the back of `q` while `nums[q[-1]] < nums[r]`. Also pop from the front if `q[0] < l`.

### 4. Detailed Approach Walkthrough
1. Initialize `output = []`, `q = collections.deque()` (stores indices), and `l = 0`.
2. Iterate `r` from 0 to `len(nums) - 1`:
   - While `q` is non-empty and `nums[q[-1]] < nums[r]`: `q.pop()` (maintain monotonic decreasing order).
   - `q.append(r)`.
   - If `l > q[0]`: `q.popleft()` (remove elements outside window boundary).
   - If `(r + 1) >= k`: append `nums[q[0]]` to `output` and increment `l += 1`.
3. Return `output`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def maxSlidingWindow(self, nums: list[int], k: int) -> list[int]:
        output = []
        q = collections.deque()  # stores indices
        l = r = 0
        
        while r < len(nums):
            # Pop smaller values from the back
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)
            
            # Remove left index from window if it's out of bounds
            if l > q[0]:
                q.popleft()
                
            # Record window maximum when window reaches size k
            if (r + 1) >= k:
                output.append(nums[q[0]])
                l += 1
            r += 1
            
        return output
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Each element is added and removed from the deque at most once.`
- **Space Complexity:** `O(k) - The deque stores at most k indices.`

---
