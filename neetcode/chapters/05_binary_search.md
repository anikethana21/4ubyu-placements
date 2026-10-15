# Chapter: Binary Search

> Binary Search operates by repeatedly halving the search space in sorted data or monotonic answer spaces, delivering fast logarithmic O(log n) time complexity.

**Total Questions in Topic:** 7

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 28 | [Binary Search](#28-binary-search) | **Easy** | `Standard Binary Search` | [#704](https://leetcode.com/problems/binary-search/) |
| 29 | [Search a 2D Matrix](#29-search-a-2d-matrix) | **Medium** | `2D Binary Search / Row-Column Elimination` | [#74](https://leetcode.com/problems/search-a-2d-matrix/) |
| 30 | [Koko Eating Bananas](#30-koko-eating-bananas) | **Medium** | `Binary Search on Solution Space` | [#875](https://leetcode.com/problems/koko-eating-bananas/) |
| 31 | [Find Minimum in Rotated Sorted Array](#31-find-minimum-in-rotated-sorted-array) | **Medium** | `Rotated Binary Search (Pivot Finding)` | [#153](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) |
| 32 | [Search in Rotated Sorted Array](#32-search-in-rotated-sorted-array) | **Medium** | `Rotated Binary Search (Half Selection)` | [#33](https://leetcode.com/problems/search-in-rotated-sorted-array/) |
| 33 | [Time Based Key-Value Store](#33-time-based-key-value-store) | **Medium** | `Binary Search on Timestamps` | [#981](https://leetcode.com/problems/time-based-key-value-store/) |
| 34 | [Median of Two Sorted Arrays](#34-median-of-two-sorted-arrays) | **Hard** | `Binary Search (Array Partitioning)` | [#4](https://leetcode.com/problems/median-of-two-sorted-arrays/) |

---

## <a id="28-binary-search"></a>28. Binary Search

- **Difficulty:** `Easy`
- **Pattern:** `Standard Binary Search`
- **LeetCode Reference:** [LeetCode #704](https://leetcode.com/problems/binary-search/)

### 1. Problem Statement
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

#### Examples:
**Example 1:**
```text
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4.
```

**Example 2:**
```text
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1.
```

#### Constraints:
- `1 <= nums.length <= 10^4`
- `-10^4 < nums[i], target < 10^4`
- `All the integers in nums are unique.`
- `nums is sorted in ascending order.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine looking for a word in a printed physical dictionary. You open directly to the middle page. If your word alphabetically comes before that page's words, you discard the entire right half of the book and repeat on the left half.

### 3. Step-by-Step Progressive Hints
- Hint 1: Initialize two pointers `l = 0` and `r = len(nums) - 1`.
- Hint 2: Compute midpoint `m = l + ((r - l) // 2)` to avoid integer overflow.
- Hint 3: If `nums[m] > target`, eliminate the right half (`r = m - 1`). If `nums[m] < target`, eliminate the left half (`l = m + 1`). If equal, return `m`.

### 4. Detailed Approach Walkthrough
1. Set `l = 0, r = len(nums) - 1`.
2. While `l <= r`:
   - Compute `m = l + ((r - l) // 2)`.
   - If `nums[m] > target`: `r = m - 1`.
   - Else if `nums[m] < target`: `l = m + 1`.
   - Else: return `m`.
3. Return `-1` if target is not found.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        l, r = 0, len(nums) - 1
        
        while l <= r:
            m = l + ((r - l) // 2)
            if nums[m] > target:
                r = m - 1
            elif nums[m] < target:
                l = m + 1
            else:
                return m
        return -1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log n) - Search space is halved in every iteration.`
- **Space Complexity:** `O(1) - Iterative pointers use constant memory.`

---

## <a id="29-search-a-2d-matrix"></a>29. Search a 2D Matrix

- **Difficulty:** `Medium`
- **Pattern:** `2D Binary Search / Row-Column Elimination`
- **LeetCode Reference:** [LeetCode #74](https://leetcode.com/problems/search-a-2d-matrix/)

### 1. Problem Statement
You are given an `m x n` integer matrix `matrix` with the following two properties:
1. Each row is sorted in non-decreasing order.
2. The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if `target` is in `matrix` or `false` otherwise.

You must write a solution in `O(log(m * n))` time complexity.

#### Examples:
**Example 1:**
```text
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
Explanation: 3 is present in the first row.
```

**Example 2:**
```text
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
Explanation: 13 is not present in the matrix.
```

#### Constraints:
- `m == matrix.length, n == matrix[i].length`
- `1 <= m, n <= 100`
- `-10^4 <= matrix[i][j], target <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> The entire 2D matrix is actually just a single continuous 1D sorted array of length `m * n` that has been wrapped into rows. You can either perform binary search across rows then columns, or treat index `k` as cell `(k // n, k % n)`.

### 3. Step-by-Step Progressive Hints
- Hint 1: First, run binary search across row boundaries to find the single row where `matrix[row][0] <= target <= matrix[row][-1]`.
- Hint 2: Once the correct row is identified, run standard binary search on that row.
- Hint 3: Total complexity will be `O(log m + log n) = O(log(m * n))`.

### 4. Detailed Approach Walkthrough
1. Set `top = 0, bot = len(matrix) - 1, COLS = len(matrix[0])`.
2. Binary search to find target row:
   - `row = (top + bot) // 2`
   - If `target > matrix[row][-1]`: `top = row + 1`
   - Else if `target < matrix[row][0]`: `bot = row - 1`
   - Else: break (target must be in this row).
3. If `top > bot`, return `False`.
4. Standard binary search within `matrix[row]`:
   - Set `l = 0, r = COLS - 1`.
   - Halve search space until found or `l > r`.
5. Return result.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def searchMatrix(self, matrix: list[list[int]], target: int) -> bool:
        ROWS, COLS = len(matrix), len(matrix[0])
        
        top, bot = 0, ROWS - 1
        while top <= bot:
            row = (top + bot) // 2
            if target > matrix[row][-1]:
                top = row + 1
            elif target < matrix[row][0]:
                bot = row - 1
            else:
                break
                
        if not (top <= bot):
            return False
            
        row = (top + bot) // 2
        l, r = 0, COLS - 1
        while l <= r:
            m = (l + r) // 2
            if target > matrix[row][m]:
                l = m + 1
            elif target < matrix[row][m]:
                r = m - 1
            else:
                return True
        return False
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log(m * n)) = O(log m + log n) - Binary searching rows and columns.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="30-koko-eating-bananas"></a>30. Koko Eating Bananas

- **Difficulty:** `Medium`
- **Pattern:** `Binary Search on Solution Space`
- **LeetCode Reference:** [LeetCode #875](https://leetcode.com/problems/koko-eating-bananas/)

### 1. Problem Statement
Koko loves to eat bananas. There are `n` piles of bananas, the `i-th` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the **minimum integer** `k` such that she can eat all the bananas within `h` hours.

#### Examples:
**Example 1:**
```text
Input: piles = [3,6,7,11], h = 8
Output: 4
Explanation: At speed 4: pile 3 takes 1h, pile 6 takes 2h, pile 7 takes 2h, pile 11 takes 3h. Total = 8 hours.
```

**Example 2:**
```text
Input: piles = [30,11,23,4,20], h = 5
Output: 30
Explanation: Since h == len(piles), Koko must eat each pile in 1h, requiring speed = max(piles) = 30.
```

**Example 3:**
```text
Input: piles = [30,11,23,4,20], h = 6
Output: 23
Explanation: At speed 23, total hours = 1 + 1 + 1 + 1 + 2 = 6 <= 6.
```

#### Constraints:
- `1 <= piles.length <= 10^4`
- `piles.length <= h <= 10^9`
- `1 <= piles[i] <= 10^9`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> The speed dial ranges from 1 banana/hr to `max(piles)` bananas/hr. As speed increases, total eating time monotonically decreases. Since time vs speed is monotonic, we can binary search the speed dial to find the lowest speed that finishes within `h` hours.

### 3. Step-by-Step Progressive Hints
- Hint 1: The minimum possible speed is 1, and the maximum necessary speed is `max(piles)`.
- Hint 2: For any speed `k`, the hours needed for pile `p` is `ceil(p / k)` (or `math.ceil(p / k)` / `(p + k - 1) // k`).
- Hint 3: If total hours <= `h`, speed `k` is valid; try slower speeds (`r = k - 1`). If total hours > `h`, `k` is too slow; try faster speeds (`l = k + 1`).

### 4. Detailed Approach Walkthrough
1. Set `l = 1, r = max(piles), res = r`.
2. While `l <= r`:
   - `k = (l + r) // 2`
   - Calculate `hours = sum(math.ceil(p / k) for p in piles)`.
   - If `hours <= h`:
     - `res = min(res, k)`
     - `r = k - 1` (search for a slower valid speed)
   - Else:
     - `l = k + 1` (need a faster speed)
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
import math

class Solution:
    def minEatingSpeed(self, piles: list[int], h: int) -> int:
        l, r = 1, max(piles)
        res = r
        
        while l <= r:
            k = (l + r) // 2
            hours = 0
            for p in piles:
                hours += math.ceil(p / k)
                
            if hours <= h:
                res = min(res, k)
                r = k - 1
            else:
                l = k + 1
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * log(max(piles))) - Where N is number of piles and log(max(piles)) is the binary search range.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="31-find-minimum-in-rotated-sorted-array"></a>31. Find Minimum in Rotated Sorted Array

- **Difficulty:** `Medium`
- **Pattern:** `Rotated Binary Search (Pivot Finding)`
- **LeetCode Reference:** [LeetCode #153](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

### 1. Problem Statement
Suppose an array of length `n` sorted in ascending order is **rotated** between `1` and `n` times.

Given the sorted rotated array `nums` of **unique** elements, return the **minimum element** of this array.

You must write an algorithm that runs in `O(log n)` time.

#### Examples:
**Example 1:**
```text
Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.
```

**Example 2:**
```text
Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: Original array was [0,1,2,4,5,6,7] rotated 4 times.
```

**Example 3:**
```text
Input: nums = [11,13,15,17]
Output: 11
Explanation: Rotated 4 times (fully sorted), min is 11.
```

#### Constraints:
- `n == nums.length`
- `1 <= n <= 5000`
- `-5000 <= nums[i] <= 5000`
- `All the integers of nums are unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A rotated sorted array consists of two upward ramps separated by a cliff drop. The minimum value is the base of the cliff. By comparing the midpoint to the rightmost value `nums[m] > nums[r]`, we can determine whether the cliff lies to our right or left.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `nums[l] < nums[r]`, the current subarray `[l..r]` is already fully sorted, so `nums[l]` is the minimum.
- Hint 2: Compare `nums[m]` with `nums[r]`. If `nums[m] > nums[r]`, the pivot (minimum) must be strictly to the right (`l = m + 1`).
- Hint 3: Otherwise, `nums[m] <= nums[r]`, so the minimum is at `m` or to the left (`r = m`).

### 4. Detailed Approach Walkthrough
1. Initialize `res = nums[0], l = 0, r = len(nums) - 1`.
2. While `l <= r`:
   - If `nums[l] < nums[r]`: `res = min(res, nums[l]); break`
   - `m = (l + r) // 2`
   - `res = min(res, nums[m])`
   - If `nums[m] >= nums[l]`: `l = m + 1` (left side is sorted, search right)
   - Else: `r = m - 1` (search left)
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findMin(self, nums: list[int]) -> int:
        res = nums[0]
        l, r = 0, len(nums) - 1
        
        while l <= r:
            if nums[l] < nums[r]:
                res = min(res, nums[l])
                break
                
            m = (l + r) // 2
            res = min(res, nums[m])
            if nums[m] >= nums[l]:
                l = m + 1
            else:
                r = m - 1
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log n) - Search space is halved each step.`
- **Space Complexity:** `O(1) - Constant extra space.`

---

## <a id="32-search-in-rotated-sorted-array"></a>32. Search in Rotated Sorted Array

- **Difficulty:** `Medium`
- **Pattern:** `Rotated Binary Search (Half Selection)`
- **LeetCode Reference:** [LeetCode #33](https://leetcode.com/problems/search-in-rotated-sorted-array/)

### 1. Problem Statement
There is an integer array `nums` sorted in ascending order (with **distinct** values) that is possibly rotated at an unknown pivot index.

Given the array `nums` after the possible rotation and an integer `target`, return the index of `target` if it is in `nums`, or `-1` if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

#### Examples:
**Example 1:**
```text
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
Explanation: 0 is located at index 4.
```

**Example 2:**
```text
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
Explanation: 3 is not in the array.
```

#### Constraints:
- `1 <= nums.length <= 5000`
- `-10^4 <= nums[i], target <= 10^4`
- `All values of nums are unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> At any midpoint `m` in a rotated sorted array, AT LEAST one of the two halves (`[l..m]` or `[m..r]`) is guaranteed to be completely normally sorted. Determine which half is sorted, check if `target` falls inside its range, and eliminate the other half.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `nums[l] <= nums[m]`, the left portion is sorted.
- Hint 2: In the left sorted portion, if `target > nums[m]` or `target < nums[l]`, search right (`l = m + 1`); else search left (`r = m - 1`).
- Hint 3: In the right sorted portion, if `target < nums[m]` or `target > nums[r]`, search left (`r = m - 1`); else search right (`l = m + 1`).

### 4. Detailed Approach Walkthrough
1. Set `l = 0, r = len(nums) - 1`.
2. While `l <= r`:
   - `m = (l + r) // 2`
   - If `target == nums[m]`: return `m`
   - If left portion is sorted (`nums[l] <= nums[m]`):
     - If `target > nums[m]` or `target < nums[l]`: `l = m + 1`
     - Else: `r = m - 1`
   - Else (right portion is sorted):
     - If `target < nums[m]` or `target > nums[r]`: `r = m - 1`
     - Else: `l = m + 1`
3. Return `-1`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        l, r = 0, len(nums) - 1
        
        while l <= r:
            m = (l + r) // 2
            if target == nums[m]:
                return m
                
            # Left sorted portion
            if nums[l] <= nums[m]:
                if target > nums[m] or target < nums[l]:
                    l = m + 1
                else:
                    r = m - 1
            # Right sorted portion
            else:
                if target < nums[m] or target > nums[r]:
                    r = m - 1
                else:
                    l = m + 1
                    
        return -1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log n) - Search space is halved each step.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="33-time-based-key-value-store"></a>33. Time Based Key-Value Store

- **Difficulty:** `Medium`
- **Pattern:** `Binary Search on Timestamps`
- **LeetCode Reference:** [LeetCode #981](https://leetcode.com/problems/time-based-key-value-store/)

### 1. Problem Statement
Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

Implement the `TimeMap` class:
- `TimeMap()` Initializes the object of the data structure.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.

#### Examples:
**Example 1:**
```text
Input: ["TimeMap", "set", "get", "get", "set", "get", "get"]
[[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]
Output: [null, null, "bar", "bar", null, "bar2", "bar2"]
Explanation: TimeMap timeMap = new TimeMap();
timeMap.set("foo", "bar", 1);
timeMap.get("foo", 1); // returns "bar"
timeMap.get("foo", 3); // returns "bar" (since timestamp 1 <= 3)
timeMap.set("foo", "bar2", 4);
timeMap.get("foo", 4); // returns "bar2"
timeMap.get("foo", 5); // returns "bar2"
```

#### Constraints:
- `1 <= key.length, value.length <= 100`
- `key and value consist of lowercase English letters and digits.`
- `1 <= timestamp <= 10^7`
- `All the timestamps timestamp of set are strictly increasing.`
- `At most 2 * 10^5 calls will be made to set and get.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a versioned document repository like Git. When you query a file at timestamp `t`, you get the most recent commit saved at or prior to timestamp `t`. Because commits are inserted in ascending timestamp order, binary search finds the right commit immediately.

### 3. Step-by-Step Progressive Hints
- Hint 1: Store values in a hash map where `key` maps to a list of pairs `[value, timestamp]`.
- Hint 2: Since `set` timestamps are strictly increasing, each key's list is already sorted by timestamp.
- Hint 3: In `get(key, timestamp)`, run binary search on `self.store[key]` to find the largest `timestamp_prev <= timestamp`.

### 4. Detailed Approach Walkthrough
1. In `__init__`, initialize `self.store = {}` mapping `key -> list of [val, timestamp]`.
2. In `set(key, val, timestamp)`, append `[val, timestamp]` to `self.store[key]`.
3. In `get(key, timestamp)`:
   - Fetch `values = self.store.get(key, [])`.
   - Set `l = 0, r = len(values) - 1, res = ""`.
   - While `l <= r`:
     - `m = (l + r) // 2`
     - If `values[m][1] <= timestamp`:
       - `res = values[m][0]` (valid candidate)
       - `l = m + 1` (search for a later valid timestamp)
     - Else:
       - `r = m - 1`
   - Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class TimeMap:
    def __init__(self):
        self.store = {}  # key : list of [val, timestamp]

    def set(self, key: str, value: str, timestamp: int) -> None:
        if key not in self.store:
            self.store[key] = []
        self.store[key].append([value, timestamp])

    def get(self, key: str, timestamp: int) -> str:
        res = ""
        values = self.store.get(key, [])
        l, r = 0, len(values) - 1
        
        while l <= r:
            m = (l + r) // 2
            if values[m][1] <= timestamp:
                res = values[m][0]
                l = m + 1
            else:
                r = m - 1
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `set: O(1); get: O(log n) where n is the number of timestamps for the given key.`
- **Space Complexity:** `O(m * n) - Storing all key-value entries across timestamps.`

---

## <a id="34-median-of-two-sorted-arrays"></a>34. Median of Two Sorted Arrays

- **Difficulty:** `Hard`
- **Pattern:** `Binary Search (Array Partitioning)`
- **LeetCode Reference:** [LeetCode #4](https://leetcode.com/problems/median-of-two-sorted-arrays/)

### 1. Problem Statement
Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the **median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

#### Examples:
**Example 1:**
```text
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: Merged array = [1,2,3] and median is 2.
```

**Example 2:**
```text
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: Merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

#### Constraints:
- `nums1.length == m, nums2.length == n`
- `0 <= m, n <= 1000`
- `1 <= m + n <= 2000`
- `-10^6 <= nums1[i], nums2[i] <= 10^6`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine dividing all elements across both arrays into a Left Half and a Right Half of equal total size. We only need to find the correct partition cut point in the smaller array `A`; the partition cut in `B` is automatically calculated to make the left side contain half the total elements.

### 3. Step-by-Step Progressive Hints
- Hint 1: Always binary search on the shorter array (let `A` be shorter, `B` be longer) to minimize operations to `O(log(min(m, n)))`.
- Hint 2: If we take `i` elements from `A`, we must take `j = (total // 2) - i` elements from `B`.
- Hint 3: The partition is valid when `A_left <= B_right` and `B_left <= A_right`. If `A_left > B_right`, move left in `A`; if `B_left > A_right`, move right in `A`.

### 4. Detailed Approach Walkthrough
1. Let `A, B = nums1, nums2`. Ensure `len(A) <= len(B)` by swapping if needed.
2. `total = len(A) + len(B)`, `half = (total + 1) // 2`.
3. Binary search on `A` with `l = 0, r = len(A)`:
   - `i = (l + r) // 2` (cut in A)
   - `j = half - i` (cut in B)
   - `Aleft = A[i - 1] if i > 0 else float('-inf')`
   - `Aright = A[i] if i < len(A) else float('inf')`
   - `Bleft = B[j - 1] if j > 0 else float('-inf')`
   - `Bright = B[j] if j < len(B) else float('inf')`
   - If `Aleft <= Bright` and `Bleft <= Aright`:
     - If `total % 2 != 0`: return `max(Aleft, Bleft)`
     - Else: return `(max(Aleft, Bleft) + min(Aright, Bright)) / 2`
   - Else if `Aleft > Bright`: `r = i - 1`
   - Else: `l = i + 1`

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findMedianSortedArrays(self, nums1: list[int], nums2: list[int]) -> float:
        A, B = nums1, nums2
        total = len(nums1) + len(nums2)
        half = total // 2
        
        if len(B) < len(A):
            A, B = B, A
            
        l, r = 0, len(A) - 1
        while True:
            i = (l + r) // 2  # A
            j = half - i - 2  # B
            
            Aleft = A[i] if i >= 0 else float("-infinity")
            Aright = A[i + 1] if (i + 1) < len(A) else float("infinity")
            Bleft = B[j] if j >= 0 else float("-infinity")
            Bright = B[j + 1] if (j + 1) < len(B) else float("infinity")
            
            # Partition is correct
            if Aleft <= Bright and Bleft <= Aright:
                # Odd
                if total % 2:
                    return min(Aright, Bright)
                # Even
                return (max(Aleft, Bleft) + min(Aright, Bright)) / 2
            elif Aleft > Bright:
                r = i - 1
            else:
                l = i + 1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log(min(m, n))) - Binary searching only the smaller array.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---
