# Chapter: Arrays & Hashing

> Arrays and Hash Tables form the bedrock of technical interviews. Hash tables offer O(1) average-time lookups, insertions, and deletions, trading space for speed.

**Total Questions in Topic:** 9

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 1 | [Contains Duplicate](#1-contains-duplicate) | **Easy** | `Hash Set` | [#217](https://leetcode.com/problems/contains-duplicate/) |
| 2 | [Valid Anagram](#2-valid-anagram) | **Easy** | `Frequency Counter / Hash Map` | [#242](https://leetcode.com/problems/valid-anagram/) |
| 3 | [Two Sum](#3-two-sum) | **Easy** | `Hash Map (Complement Search)` | [#1](https://leetcode.com/problems/two-sum/) |
| 4 | [Group Anagrams](#4-group-anagrams) | **Medium** | `Hash Map Categorization` | [#49](https://leetcode.com/problems/group-anagrams/) |
| 5 | [Top K Frequent Elements](#5-top-k-frequent-elements) | **Medium** | `Bucket Sort / Min-Heap` | [#347](https://leetcode.com/problems/top-k-frequent-elements/) |
| 6 | [Product of Array Except Self](#6-product-of-array-except-self) | **Medium** | `Prefix and Postfix Products` | [#238](https://leetcode.com/problems/product-of-array-except-self/) |
| 7 | [Valid Sudoku](#7-valid-sudoku) | **Medium** | `Matrix Hashing / Set Validation` | [#36](https://leetcode.com/problems/valid-sudoku/) |
| 8 | [Encode and Decode Strings](#8-encode-and-decode-strings) | **Medium** | `String Serialization (Length-Delimited)` | [#271](https://neetcode.io/problems/string-encode-and-decode) |
| 9 | [Longest Consecutive Sequence](#9-longest-consecutive-sequence) | **Medium** | `Hash Set (Sequence Start Detection)` | [#128](https://leetcode.com/problems/longest-consecutive-sequence/) |

---

## <a id="1-contains-duplicate"></a>1. Contains Duplicate

- **Difficulty:** `Easy`
- **Pattern:** `Hash Set`
- **LeetCode Reference:** [LeetCode #217](https://leetcode.com/problems/contains-duplicate/)

### 1. Problem Statement
Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

#### Examples:
**Example 1:**
```text
Input: nums = [1,2,3,1]
Output: true
Explanation: The value 1 appears at indices 0 and 3.
```

**Example 2:**
```text
Input: nums = [1,2,3,4]
Output: false
Explanation: All elements are distinct.
```

**Example 3:**
```text
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
Explanation: Multiple numbers appear more than once.
```

#### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a guest checklist at an exclusive party. As each guest arrives, the bouncer checks if their name is already on the signed-in list. If it is, an impostor or duplicate entry is caught immediately without needing to interview every guest inside.

### 3. Step-by-Step Progressive Hints
- Hint 1: A brute-force approach compares every pair in O(n^2). Sorting takes O(n log n). Can we do O(n) using additional space?
- Hint 2: What data structure provides O(1) average lookup and insertion?
- Hint 3: Iterate through the array while maintaining a `seen` hash set. If the current number is already in `seen`, return True. Otherwise, add it. If the loop finishes, return False.

### 4. Detailed Approach Walkthrough
1. Initialize an empty hash set called `seen`.
2. Iterate through each number `n` in `nums`.
3. Check if `n` exists in `seen`. If it does, a duplicate has been found; return `True`.
4. If not, insert `n` into `seen`.
5. If the loop completes without finding any duplicates, return `False`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def containsDuplicate(self, nums: list[int]) -> bool:
        seen = set()
        for n in nums:
            if n in seen:
                return True
            seen.add(n)
        return False

# Alternative one-liner:
# return len(nums) != len(set(nums))
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - We perform a single pass over the array of size n, and set lookups/insertions are O(1) on average.`
- **Space Complexity:** `O(n) - In the worst case where all elements are unique, the hash set stores all n elements.`

---

## <a id="2-valid-anagram"></a>2. Valid Anagram

- **Difficulty:** `Easy`
- **Pattern:** `Frequency Counter / Hash Map`
- **LeetCode Reference:** [LeetCode #242](https://leetcode.com/problems/valid-anagram/)

### 1. Problem Statement
Given two strings `s` and `t`, return `true` if `t` is an **anagram** of `s`, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

#### Examples:
**Example 1:**
```text
Input: s = "anagram", t = "nagaram"
Output: true
Explanation: Both strings contain 3 'a's, 1 'g', 1 'm', 1 'n', and 1 'r'.
```

**Example 2:**
```text
Input: s = "rat", t = "car"
Output: false
Explanation: Characters and frequencies do not match.
```

#### Constraints:
- `1 <= s.length, t.length <= 5 * 10^4`
- `s and t consist of lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Think of two Scrabble player trays. If both players have the exact same count of each letter tile in their trays, they can spell different anagrams using the exact same inventory.

### 3. Step-by-Step Progressive Hints
- Hint 1: If the lengths of `s` and `t` differ, they cannot possibly be anagrams.
- Hint 2: You can count the frequency of each character in both strings and compare counts.
- Hint 3: Use either two hash maps or an integer array of size 26 for counting. Increment for `s` and decrement for `t`, or use Python's `collections.Counter`.

### 4. Detailed Approach Walkthrough
1. First, check if `len(s) != len(t)`. If so, return `False`.
2. Create hash maps `countS` and `countT` to store character frequencies.
3. Loop through both strings simultaneously, populating counts.
4. Compare `countS` with `countT`.
5. Alternatively, use a single frequency array of size 26 for optimal memory performance.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        countS, countT = {}, {}
        for i in range(len(s)):
            countS[s[i]] = countS.get(s[i], 0) + 1
            countT[t[i]] = countT.get(t[i], 0) + 1
            
        return countS == countT

# Alternative:
# return collections.Counter(s) == collections.Counter(t)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Where n is the length of strings s and t. We iterate through the strings once.`
- **Space Complexity:** `O(1) - Since the character set is bounded to 26 lowercase English letters, space used is bounded by O(26) = O(1).`

---

## <a id="3-two-sum"></a>3. Two Sum

- **Difficulty:** `Easy`
- **Pattern:** `Hash Map (Complement Search)`
- **LeetCode Reference:** [LeetCode #1](https://leetcode.com/problems/two-sum/)

### 1. Problem Statement
Given an array of integers `nums` and an integer `target`, return **indices of the two numbers** such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

#### Examples:
**Example 1:**
```text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**
```text
Input: nums = [3,2,4], target = 6
Output: [1,2]
Explanation: nums[1] + nums[2] == 6, so we return [1, 2].
```

**Example 3:**
```text
Input: nums = [3,3], target = 6
Output: [0,1]
Explanation: nums[0] + nums[1] == 6, so we return [0, 1].
```

#### Constraints:
- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- `Only one valid answer exists.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine you have a puzzle piece with value `x` and need a total sum of `target`. Instead of searching through every other piece in the box repeatedly, you calculate your missing piece's value `diff = target - x` and check a quick-lookup shelf to see if someone already placed that exact piece there.

### 3. Step-by-Step Progressive Hints
- Hint 1: For each element `nums[i]`, what number are we looking for to reach `target`?
- Hint 2: The required complement is `diff = target - nums[i]`. Can we remember past numbers and their indices in O(1)?
- Hint 3: Store visited elements in a hash map where `key = number` and `value = index`. Check if `diff` is already in the map before adding the current element.

### 4. Detailed Approach Walkthrough
1. Initialize a hash map `prevMap = {}` mapping value -> index.
2. Iterate through `nums` with index `i` and value `n`.
3. Compute `diff = target - n`.
4. If `diff` exists in `prevMap`, return `[prevMap[diff], i]`.
5. Otherwise, store `prevMap[n] = i`.
6. Guaranteed to find a solution as per problem constraints.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        prevMap = {}  # val -> index
        
        for i, n in enumerate(nums):
            diff = target - n
            if diff in prevMap:
                return [prevMap[diff], i]
            prevMap[n] = i
        return []
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass over the array with O(1) hash map operations.`
- **Space Complexity:** `O(n) - In the worst case, we store up to n - 1 items in the hash map.`

---

## <a id="4-group-anagrams"></a>4. Group Anagrams

- **Difficulty:** `Medium`
- **Pattern:** `Hash Map Categorization`
- **LeetCode Reference:** [LeetCode #49](https://leetcode.com/problems/group-anagrams/)

### 1. Problem Statement
Given an array of strings `strs`, group the **anagrams** together. You can return the answer in **any order**.

#### Examples:
**Example 1:**
```text
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
Explanation: Anagrams are grouped into lists sharing identical letter frequencies.
```

**Example 2:**
```text
Input: strs = [""]
Output: [[""]]
Explanation: Empty string forms a group of size 1.
```

**Example 3:**
```text
Input: strs = ["a"]
Output: [["a"]]
Explanation: Single string forms a group of size 1.
```

#### Constraints:
- `1 <= strs.length <= 10^4`
- `0 <= strs[i].length <= 100`
- `strs[i] consists of lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine sorting incoming mail into sorting bins. You label each bin not by the exact word, but by its character fingerprint (e.g. 1 'a', 1 'e', 1 't'). Every word with that fingerprint drops into the exact same bin.

### 3. Step-by-Step Progressive Hints
- Hint 1: Two words are anagrams if and only if their sorted versions are identical, or their character counts are identical.
- Hint 2: Sorting each word takes O(k log k). Can we represent the character frequency tuple as an immutable key of length 26 to achieve O(k)?
- Hint 3: Use a hash map where the key is a tuple of 26 integers representing counts of 'a' through 'z', and the value is a list of matching words.

### 4. Detailed Approach Walkthrough
1. Initialize `ans = collections.defaultdict(list)`.
2. For each string `s` in `strs`, create an array `count = [0] * 26`.
3. Count the frequency of each character `c` in `s` by computing `ord(c) - ord('a')`.
4. Convert the `count` array to a tuple (so it can be used as a hash map key) and append `s` to `ans[tuple(count)]`.
5. Return `list(ans.values())`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        ans = collections.defaultdict(list)
        
        for s in strs:
            count = [0] * 26  # a ... z
            for c in s:
                count[ord(c) - ord('a')] += 1
            ans[tuple(count)].append(s)
            
        return list(ans.values())
```

### 6. Complexity Analysis
- **Time Complexity:** `O(m * k) - Where m is the number of strings and k is the maximum length of a string. Counting takes O(k) per string.`
- **Space Complexity:** `O(m * k) - To store all strings in the dictionary.`

---

## <a id="5-top-k-frequent-elements"></a>5. Top K Frequent Elements

- **Difficulty:** `Medium`
- **Pattern:** `Bucket Sort / Min-Heap`
- **LeetCode Reference:** [LeetCode #347](https://leetcode.com/problems/top-k-frequent-elements/)

### 1. Problem Statement
Given an integer array `nums` and an integer `k`, return the `k` **most frequent elements**. You may return the answer in **any order**.

#### Examples:
**Example 1:**
```text
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Explanation: 1 appears 3 times, 2 appears 2 times, and 3 appears 1 time. Top 2 frequent are [1, 2].
```

**Example 2:**
```text
Input: nums = [1], k = 1
Output: [1]
Explanation: Single element is the most frequent.
```

#### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `k is in the range [1, the number of unique elements in the array].`
- `It is guaranteed that the answer is unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a leaderboard podium where slots are frequency counts (0 to n). After counting votes for each candidate, you place each candidate in the bucket corresponding to their vote total. Then you simply read the leaderboard from highest vote bucket down until you have `k` candidates.

### 3. Step-by-Step Progressive Hints
- Hint 1: First, build a frequency map of each number using a hash map.
- Hint 2: Sorting the counts takes O(n log n), and a Min-Heap of size k takes O(n log k). Can we do O(n) linearly?
- Hint 3: Use Bucket Sort! Create an array `freq` of size `len(nums) + 1` where index `i` holds a list of numbers that appeared exactly `i` times. Iterate backwards from highest frequency.

### 4. Detailed Approach Walkthrough
1. Count occurrences of each number using a hash map `count`.
2. Create an array of buckets `freq = [[] for _ in range(len(nums) + 1)]` where the index represents frequency.
3. For each number and its count, append the number to `freq[count]`.
4. Traverse `freq` in reverse order (from highest frequency `len(nums)` down to 1).
5. Accumulate numbers into `res` until `len(res) == k`.
6. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def topKFrequent(self, nums: list[int], k: int) -> list[int]:
        count = {}
        freq = [[] for _ in range(len(nums) + 1)]
        
        for n in nums:
            count[n] = 1 + count.get(n, 0)
            
        for n, c in count.items():
            freq[c].append(n)
            
        res = []
        for i in range(len(freq) - 1, 0, -1):
            for n in freq[i]:
                res.append(n)
                if len(res) == k:
                    return res
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Counting frequencies takes O(n), populating buckets takes O(n), and iterating backwards takes O(n).`
- **Space Complexity:** `O(n) - Hash map and bucket array both take O(n) space.`

---

## <a id="6-product-of-array-except-self"></a>6. Product of Array Except Self

- **Difficulty:** `Medium`
- **Pattern:** `Prefix and Postfix Products`
- **LeetCode Reference:** [LeetCode #238](https://leetcode.com/problems/product-of-array-except-self/)

### 1. Problem Statement
Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and **without using the division operation**.

#### Examples:
**Example 1:**
```text
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Explanation: For i=0: 2*3*4=24; i=1: 1*3*4=12; i=2: 1*2*4=8; i=3: 1*2*3=6.
```

**Example 2:**
```text
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
Explanation: Any position other than the 0 element multiplies with 0, yielding 0.
```

#### Constraints:
- `2 <= nums.length <= 10^5`
- `-30 <= nums[i] <= 30`
- `Product fits in a 32-bit integer.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine standing in a line of people holding multipliers. To calculate the combined multiplier of everyone except you, you multiply the product of everyone to your left (prefix) by the product of everyone to your right (postfix).

### 3. Step-by-Step Progressive Hints
- Hint 1: For any index `i`, `answer[i] = (product of elements before i) * (product of elements after i)`.
- Hint 2: Can we calculate the prefix products in a left-to-right pass and store them in the output array?
- Hint 3: In a second right-to-left pass, maintain a running `postfix` accumulator variable and multiply it into the prefix values in `res`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = [1] * len(nums)`.
2. Make a forward pass: maintain a running `prefix` variable (initially 1). At each index `i`, set `res[i] = prefix`, then update `prefix *= nums[i]`.
3. Make a backward pass: maintain a running `postfix` variable (initially 1). At each index `i` (from `len(nums)-1` down to 0), multiply `res[i] *= postfix`, then update `postfix *= nums[i]`.
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def productExceptSelf(self, nums: list[int]) -> list[int]:
        res = [1] * len(nums)
        
        # Left-to-right prefix pass
        prefix = 1
        for i in range(len(nums)):
            res[i] = prefix
            prefix *= nums[i]
            
        # Right-to-left postfix pass
        postfix = 1
        for i in range(len(nums) - 1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Two linear passes through the array.`
- **Space Complexity:** `O(1) extra space - Output array does not count toward extra space as per problem specification.`

---

## <a id="7-valid-sudoku"></a>7. Valid Sudoku

- **Difficulty:** `Medium`
- **Pattern:** `Matrix Hashing / Set Validation`
- **LeetCode Reference:** [LeetCode #36](https://leetcode.com/problems/valid-sudoku/)

### 1. Problem Statement
Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

#### Examples:
**Example 1:**
```text
Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: true
Explanation: All rows, columns, and 3x3 subgrids contain unique digits from '1'-'9'.
```

#### Constraints:
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j] is a digit '1'-'9' or '.'.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a 3-way security checkpoint for a convention. Every attendee (digit) must present an ID that has never been registered in their row room, their column corridor, or their designated 3x3 banquet section `(r // 3, c // 3)`.

### 3. Step-by-Step Progressive Hints
- Hint 1: You need to track seen numbers across 9 rows, 9 columns, and 9 3x3 squares.
- Hint 2: How do you identify which 3x3 square a cell `(r, c)` belongs to? Notice that integer division `(r // 3, c // 3)` maps indices from 0..8 into (0..2, 0..2) coordinate pairs.
- Hint 3: Use hash sets mapped by row index `r`, column index `c`, and square coordinate `(r // 3, c // 3)`.

### 4. Detailed Approach Walkthrough
1. Initialize three hash map collections of sets: `cols = defaultdict(set)`, `rows = defaultdict(set)`, and `squares = defaultdict(set)`.
2. Iterate through every cell `(r, c)` in the 9x9 grid.
3. If `board[r][c] == "."`, skip it.
4. Check if `board[r][c]` already exists in `rows[r]`, `cols[c]`, or `squares[(r // 3, c // 3)]`.
5. If it does, return `False` immediately.
6. Otherwise, add the value to all three corresponding sets.
7. If all cells pass validation, return `True`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def isValidSudoku(self, board: list[list[str]]) -> bool:
        cols = collections.defaultdict(set)
        rows = collections.defaultdict(set)
        squares = collections.defaultdict(set)  # key: (r // 3, c // 3)
        
        for r in range(9):
            for c in range(9):
                val = board[r][c]
                if val == ".":
                    continue
                
                square_key = (r // 3, c // 3)
                if (val in rows[r] or 
                    val in cols[c] or 
                    val in squares[square_key]):
                    return False
                
                rows[r].add(val)
                cols[c].add(val)
                squares[square_key].add(val)
                
        return True
```

### 6. Complexity Analysis
- **Time Complexity:** `O(1) - The board size is fixed at 9x9 (81 cells), taking constant time.`
- **Space Complexity:** `O(1) - The number of tracked elements is fixed to 81 cells across hash sets.`

---

## <a id="8-encode-and-decode-strings"></a>8. Encode and Decode Strings

- **Difficulty:** `Medium`
- **Pattern:** `String Serialization (Length-Delimited)`
- **LeetCode Reference:** [LeetCode #271](https://neetcode.io/problems/string-encode-and-decode)

### 1. Problem Statement
Design an algorithm to encode a list of strings to a single string. The encoded string is then sent over the network and decoded back to the original list of strings.

Please implement `encode` and `decode`.

#### Examples:
**Example 1:**
```text
Input: dummy_input = ["neet","code","love","you"]
Output: ["neet","code","love","you"]
Explanation: Original list is encoded to a string and decoded back into the exact same array.
```

**Example 2:**
```text
Input: dummy_input = ["we","say",":","yes"]
Output: ["we","say",":","yes"]
Explanation: Handles arbitrary special delimiter characters inside the strings.
```

#### Constraints:
- `0 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i] contains any possible characters out of 256 valid ASCII characters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Like HTTP chunked transfer encoding or network packets: prefixing each payload with its exact byte length followed by a boundary marker (e.g. `4#neet4#code`) guarantees that even if the word contains `#` or symbols, the parser knows exactly how many characters to consume.

### 3. Step-by-Step Progressive Hints
- Hint 1: A simple delimiter like `,` or `#` fails if the string itself contains `,` or `#`.
- Hint 2: How can we unambiguously tell the parser where each string ends?
- Hint 3: Encode each string as `<length>#<string>`. When decoding, read digits until `#` to find the length `L`, then read the next `L` characters as the string.

### 4. Detailed Approach Walkthrough
1. **Encode**: Iterate through the list of strings. For each string `s`, append `str(len(s)) + "#" + s` to the result string.
2. **Decode**: Maintain pointer `i = 0`.
3. Find the index `j` of the delimiter `#` starting from `i`.
4. Parse `length = int(s[i:j])`.
5. Extract the substring `s[j + 1 : j + 1 + length]` and append to the result list.
6. Advance `i = j + 1 + length` and repeat until the end of `s`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def encode(self, strs: list[str]) -> str:
        res = ""
        for s in strs:
            res += str(len(s)) + "#" + s
        return res

    def decode(self, s: str) -> list[str]:
        res = []
        i = 0
        while i < len(s):
            j = i
            while s[j] != "#":
                j += 1
            length = int(s[i:j])
            word = s[j + 1 : j + 1 + length]
            res.append(word)
            i = j + 1 + length
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N) for both encode and decode, where N is the total number of characters across all strings.`
- **Space Complexity:** `O(1) extra space (excluding space needed for the output).`

---

## <a id="9-longest-consecutive-sequence"></a>9. Longest Consecutive Sequence

- **Difficulty:** `Medium`
- **Pattern:** `Hash Set (Sequence Start Detection)`
- **LeetCode Reference:** [LeetCode #128](https://leetcode.com/problems/longest-consecutive-sequence/)

### 1. Problem Statement
Given an unsorted array of integers `nums`, return the length of the **longest consecutive elements sequence**.

You must write an algorithm that runs in `O(n)` time.

#### Examples:
**Example 1:**
```text
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Its length is 4.
```

**Example 2:**
```text
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
Explanation: The sequence is [0, 1, 2, 3, 4, 5, 6, 7, 8], length = 9.
```

#### Constraints:
- `0 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine people standing randomly in a room holding numbered cards. To find the longest continuous train of numbers without sorting everyone, you only ask a person to start counting upward if nobody in the room is holding the number directly before theirs `(n - 1)`. If someone has `n - 1`, they are not the locomotive!

### 3. Step-by-Step Progressive Hints
- Hint 1: Sorting takes O(n log n), which violates the required O(n) runtime.
- Hint 2: Convert `nums` to a hash set for O(1) membership checks.
- Hint 3: How do you identify the start of a consecutive sequence? A number `n` is the start if `n - 1` is NOT in the set! Only expand sequences from sequence heads.

### 4. Detailed Approach Walkthrough
1. Insert all numbers from `nums` into a hash set `numSet`.
2. Initialize `longest = 0`.
3. Iterate through each number `n` in `numSet`:
   - Check if `(n - 1)` is in `numSet`.
   - If NOT, `n` is the beginning of a new sequence.
   - Initialize `length = 1` and loop while `(n + length)` is in `numSet`, incrementing `length`.
   - Update `longest = max(longest, length)`.
4. Return `longest`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def longestConsecutive(self, nums: list[int]) -> int:
        numSet = set(nums)
        longest = 0
        
        for n in numSet:
            # Check if n is the start of a sequence
            if (n - 1) not in numSet:
                length = 1
                while (n + length) in numSet:
                    length += 1
                longest = max(longest, length)
                
        return longest
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Each number is visited at most twice (once in outer loop, once in while loop when building sequence).`
- **Space Complexity:** `O(n) - Storing numbers in the hash set.`

---
