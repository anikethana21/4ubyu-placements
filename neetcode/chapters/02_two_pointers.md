# Chapter: Two Pointers

> Two Pointers technique uses two indices to traverse a linear data structure simultaneously, typically converging from opposite ends or moving at different speeds to eliminate redundant nested loops.

**Total Questions in Topic:** 5

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 10 | [Valid Palindrome](#10-valid-palindrome) | **Easy** | `Converging Pointers` | [#125](https://leetcode.com/problems/valid-palindrome/) |
| 11 | [Two Sum II Input Array Is Sorted](#11-two-sum-ii-input-array-is-sorted) | **Medium** | `Two Pointers (Sorted Array)` | [#167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) |
| 12 | [3Sum](#12-3sum) | **Medium** | `Sort + Two Pointers` | [#15](https://leetcode.com/problems/3sum/) |
| 13 | [Container With Most Water](#13-container-with-most-water) | **Medium** | `Greedy Two Pointers` | [#11](https://leetcode.com/problems/container-with-most-water/) |
| 14 | [Trapping Rain Water](#14-trapping-rain-water) | **Hard** | `Two Pointers (Min of Max Heights)` | [#42](https://leetcode.com/problems/trapping-rain-water/) |

---

## <a id="10-valid-palindrome"></a>10. Valid Palindrome

- **Difficulty:** `Easy`
- **Pattern:** `Converging Pointers`
- **LeetCode Reference:** [LeetCode #125](https://leetcode.com/problems/valid-palindrome/)

### 1. Problem Statement
A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

#### Examples:
**Example 1:**
```text
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**
```text
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

**Example 3:**
```text
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumerics, which reads the same forward and backward.
```

#### Constraints:
- `1 <= s.length <= 2 * 10^5`
- `s consists only of printable ASCII characters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Two readers start reading a text simultaneously: one from the very first letter and the other from the last letter, skipping all punctuation and spaces. If they say the exact same character aloud at every step until they meet in the middle, the text is a palindrome.

### 3. Step-by-Step Progressive Hints
- Hint 1: You can ignore spaces, punctuation, and uppercase/lowercase differences.
- Hint 2: Instead of creating a new filtered string (which uses O(n) extra space), use two pointers `l` and `r`.
- Hint 3: Increment `l` past non-alphanumeric chars, decrement `r` past non-alphanumeric chars, and compare lowercase values.

### 4. Detailed Approach Walkthrough
1. Initialize left pointer `l = 0` and right pointer `r = len(s) - 1`.
2. While `l < r`:
   - While `l < r` and `s[l]` is not alphanumeric, `l += 1`.
   - While `r > l` and `s[r]` is not alphanumeric, `r -= 1`.
   - If `s[l].lower() != s[r].lower()`, return `False`.
   - Advance `l += 1` and `r -= 1`.
3. Return `True` if pointers cross without mismatch.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1
        
        while l < r:
            while l < r and not self.isAlphaNum(s[l]):
                l += 1
            while r > l and not self.isAlphaNum(s[r]):
                r -= 1
                
            if s[l].lower() != s[r].lower():
                return False
            l, r = l + 1, r - 1
            
        return True
        
    def isAlphaNum(self, c: str) -> bool:
        return (ord('A') <= ord(c) <= ord('Z') or
                ord('a') <= ord(c) <= ord('z') or
                ord('0') <= ord(c) <= ord('9'))
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single scan over string of length n.`
- **Space Complexity:** `O(1) - Constant space with two pointers in-place.`

---

## <a id="11-two-sum-ii-input-array-is-sorted"></a>11. Two Sum II Input Array Is Sorted

- **Difficulty:** `Medium`
- **Pattern:** `Two Pointers (Sorted Array)`
- **LeetCode Reference:** [LeetCode #167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

### 1. Problem Statement
Given a **1-indexed** array of integers `numbers` that is already **sorted in non-decreasing order**, find two numbers such that they add up to a specific `target` number.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

You may not use the same element twice. Your solution must use only `O(1)` extra space.

#### Examples:
**Example 1:**
```text
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```

**Example 2:**
```text
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: 2 + 4 = 6. index1 = 1, index2 = 3. Return [1, 3].
```

#### Constraints:
- `2 <= numbers.length <= 3 * 10^4`
- `-1000 <= numbers[i] <= 1000`
- `numbers is sorted in non-decreasing order.`
- `-1000 <= target <= 1000`
- `The tests are generated such that there is exactly one solution.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a balanced scale. You pick the lightest item with your left hand and the heaviest with your right. If their sum is too heavy, the only way to lighten it is to pick a lighter item with your right hand. If too light, pick a heavier item with your left hand.

### 3. Step-by-Step Progressive Hints
- Hint 1: The array is sorted. What happens if `numbers[l] + numbers[r] > target`?
- Hint 2: Since numbers are sorted, moving the right pointer left decreases the sum, and moving the left pointer right increases the sum.
- Hint 3: Initialize `l = 0, r = len(numbers) - 1` and converge until the exact sum is found.

### 4. Detailed Approach Walkthrough
1. Initialize left pointer `l = 0` and right pointer `r = len(numbers) - 1`.
2. Calculate `curSum = numbers[l] + numbers[r]`.
3. If `curSum > target`, decrement `r -= 1` to reduce the sum.
4. If `curSum < target`, increment `l += 1` to increase the sum.
5. If `curSum == target`, return `[l + 1, r + 1]` (1-indexed).
6. Exactly one solution is guaranteed.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def twoSum(self, numbers: list[int], target: int) -> list[int]:
        l, r = 0, len(numbers) - 1
        
        while l < r:
            curSum = numbers[l] + numbers[r]
            
            if curSum > target:
                r -= 1
            elif curSum < target:
                l += 1
            else:
                return [l + 1, r + 1]
        return []
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass converging from ends.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="12-3sum"></a>12. 3Sum

- **Difficulty:** `Medium`
- **Pattern:** `Sort + Two Pointers`
- **LeetCode Reference:** [LeetCode #15](https://leetcode.com/problems/3sum/)

### 1. Problem Statement
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

#### Examples:
**Example 1:**
```text
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: Distinct triplets summing to 0 are [-1, 0, 1] and [-1, -1, 2].
```

**Example 2:**
```text
Input: nums = [0,1,1]
Output: []
Explanation: No possible triplet sums to 0.
```

**Example 3:**
```text
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums to 0.
```

#### Constraints:
- `3 <= nums.length <= 3000`
- `-10^5 <= nums[i] <= 10^5`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> You are organizing a 3-person relay team whose combined handicaps must cancel out to 0. First, line up all athletes in order of skill. For each chosen athlete `A`, use Two Sum II with two pointers to find two teammates `B` and `C` such that `B + C = -A`, skipping any duplicate candidates to avoid identical teams.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sorting the array first takes O(n log n) and enables two pointers.
- Hint 2: For each element `nums[i]`, we need to find two other numbers that sum to `-nums[i]`.
- Hint 3: To avoid duplicates, skip `nums[i]` if it is the same as `nums[i-1]`, and skip `nums[l]` / `nums[r]` after finding a valid triplet.

### 4. Detailed Approach Walkthrough
1. Sort `nums` in ascending order.
2. Iterate through index `i` and value `a` in `nums`:
   - If `i > 0` and `a == nums[i - 1]`, continue (skip duplicate base values).
   - If `a > 0`, break early (three positive numbers cannot sum to 0).
   - Set `l = i + 1, r = len(nums) - 1`.
   - While `l < r`:
     - `threeSum = a + nums[l] + nums[r]`
     - If `threeSum > 0`: `r -= 1`
     - If `threeSum < 0`: `l += 1`
     - If `threeSum == 0`: append `[a, nums[l], nums[r]]` to `res`, increment `l += 1`, and advance `l` while `nums[l] == nums[l - 1]` and `l < r`.
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()
        
        for i, a in enumerate(nums):
            if a > 0:
                break
            if i > 0 and a == nums[i - 1]:
                continue
                
            l, r = i + 1, len(nums) - 1
            while l < r:
                threeSum = a + nums[l] + nums[r]
                if threeSum > 0:
                    r -= 1
                elif threeSum < 0:
                    l += 1
                else:
                    res.append([a, nums[l], nums[r]])
                    l += 1
                    r -= 1
                    while nums[l] == nums[l - 1] and l < r:
                        l += 1
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n^2) - Sorting takes O(n log n) and the nested two-pointer loop takes O(n^2).`
- **Space Complexity:** `O(1) or O(n) depending on the sorting implementation.`

---

## <a id="13-container-with-most-water"></a>13. Container With Most Water

- **Difficulty:** `Medium`
- **Pattern:** `Greedy Two Pointers`
- **LeetCode Reference:** [LeetCode #11](https://leetcode.com/problems/container-with-most-water/)

### 1. Problem Statement
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i-th` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the **maximum amount of water** a container can store.

Notice that you may not slant the container.

#### Examples:
**Example 1:**
```text
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: Max area is formed between index 1 (height 8) and index 8 (height 7): min(8, 7) * (8 - 1) = 7 * 7 = 49.
```

**Example 2:**
```text
Input: height = [1,1]
Output: 1
Explanation: min(1, 1) * (1 - 0) = 1.
```

#### Constraints:
- `n == height.length`
- `2 <= n <= 10^5`
- `0 <= height[i] <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine holding two walls of a swimming pool at maximum possible distance apart. The water level is limited by the shorter of the two walls. Moving the taller wall inward only shrinks width without any potential to raise water height. Therefore, the only chance of finding a larger volume is to discard the shorter wall and search inward for a taller replacement.

### 3. Step-by-Step Progressive Hints
- Hint 1: The area is determined by `min(height[l], height[r]) * (r - l)`.
- Hint 2: Start with the maximum possible width: `l = 0` and `r = len(height) - 1`.
- Hint 3: To potentially increase the area when narrowing width, always shift the pointer pointing to the shorter line inward.

### 4. Detailed Approach Walkthrough
1. Initialize `l = 0, r = len(height) - 1, res = 0`.
2. While `l < r`:
   - Calculate `area = (r - l) * min(height[l], height[r])`.
   - Update `res = max(res, area)`.
   - If `height[l] < height[r]`, increment `l += 1`.
   - Else, decrement `r -= 1`.
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxArea(self, height: list[int]) -> int:
        l, r = 0, len(height) - 1
        res = 0
        
        while l < r:
            area = (r - l) * min(height[l], height[r])
            res = max(res, area)
            
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass with two pointers.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="14-trapping-rain-water"></a>14. Trapping Rain Water

- **Difficulty:** `Hard`
- **Pattern:** `Two Pointers (Min of Max Heights)`
- **LeetCode Reference:** [LeetCode #42](https://leetcode.com/problems/trapping-rain-water/)

### 1. Problem Statement
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

#### Examples:
**Example 1:**
```text
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The elevation map traps 6 units of rain water.
```

**Example 2:**
```text
Input: height = [4,2,0,3,2,5]
Output: 9
Explanation: Total trapped water = 9 units.
```

#### Constraints:
- `n == height.length`
- `1 <= n <= 2 * 10^4`
- `0 <= height[i] <= 10^5`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> The water trapped above any single position `i` is strictly limited by the lower of two barriers: the highest wall somewhere to its left, and the highest wall somewhere to its right: `water[i] = max(0, min(maxL, maxR) - height[i])`. With two pointers, you only need to know which side has the smaller maximum barrier to calculate exact trapped water.

### 3. Step-by-Step Progressive Hints
- Hint 1: The water trapped above index `i` is `min(max_left, max_right) - height[i]`.
- Hint 2: You can precompute prefix and suffix max arrays in O(n) space.
- Hint 3: Can we do it in O(1) space? Yes, using two pointers. If `maxLeft < maxRight`, the bottleneck at `l` is strictly `maxLeft`, so we can compute trapped water at `l` immediately and move `l` right.

### 4. Detailed Approach Walkthrough
1. If `not height`, return 0.
2. Set `l = 0, r = len(height) - 1`.
3. Initialize `leftMax = height[l], rightMax = height[r], res = 0`.
4. While `l < r`:
   - If `leftMax < rightMax`:
     - Advance `l += 1`.
     - Update `leftMax = max(leftMax, height[l])`.
     - Add `leftMax - height[l]` to `res`.
   - Else:
     - Decrement `r -= 1`.
     - Update `rightMax = max(rightMax, height[r])`.
     - Add `rightMax - height[r]` to `res`.
5. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def trap(self, height: list[int]) -> int:
        if not height:
            return 0
            
        l, r = 0, len(height) - 1
        leftMax, rightMax = height[l], height[r]
        res = 0
        
        while l < r:
            if leftMax < rightMax:
                l += 1
                leftMax = max(leftMax, height[l])
                res += leftMax - height[l]
            else:
                r -= 1
                rightMax = max(rightMax, height[r])
                res += rightMax - height[r]
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass visiting each elevation bar once.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---
