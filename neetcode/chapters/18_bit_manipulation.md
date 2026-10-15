# Chapter: Bit Manipulation

> Bit Manipulation uses bitwise operators (AND `&`, OR `|`, XOR `^`, NOT `~`, Shift `<<`, `>>`) for high-performance arithmetic, bitmasking, and parity calculations.

**Total Questions in Topic:** 7

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 144 | [Single Number](#144-single-number) | **Easy** | `XOR Parity Cancellation` | [#136](https://leetcode.com/problems/single-number/) |
| 145 | [Number of 1 Bits](#145-number-of-1-bits) | **Easy** | `Brian Kernighan's Algorithm (`n & (n - 1)`)` | [#191](https://leetcode.com/problems/number-of-1-bits/) |
| 146 | [Counting Bits](#146-counting-bits) | **Easy** | `Bit DP with Offset (`dp[i] = 1 + dp[i - offset]`)` | [#338](https://leetcode.com/problems/counting-bits/) |
| 147 | [Reverse Bits](#147-reverse-bits) | **Easy** | `Bit Shift & Masking` | [#190](https://leetcode.com/problems/reverse-bits/) |
| 148 | [Missing Number](#148-missing-number) | **Easy** | `XOR / Gauss Sum Formula` | [#268](https://leetcode.com/problems/missing-number/) |
| 149 | [Sum of Two Integers](#149-sum-of-two-integers) | **Medium** | `Bitwise Full Adder (`XOR` and `AND << 1`)` | [#371](https://leetcode.com/problems/sum-of-two-integers/) |
| 150 | [Reverse Integer](#150-reverse-integer) | **Medium** | `Digit Extraction & 32-Bit Overflow Prevention` | [#7](https://leetcode.com/problems/reverse-integer/) |

---

## <a id="144-single-number"></a>144. Single Number

- **Difficulty:** `Easy`
- **Pattern:** `XOR Parity Cancellation`
- **LeetCode Reference:** [LeetCode #136](https://leetcode.com/problems/single-number/)

### 1. Problem Statement
Given a **non-empty** array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

#### Examples:
**Example 1:**
```text
Input: nums = [2,2,1]
Output: 1
Explanation: 2 XOR 2 cancels to 0, leaving 1.
```

**Example 2:**
```text
Input: nums = [4,1,2,1,2]
Output: 4
Explanation: 1^1=0, 2^2=0, leaving 4.
```

#### Constraints:
- `1 <= nums.length <= 3 * 10^4`
- `-3 * 10^4 <= nums[i] <= 3 * 10^4`
- `Each element in the array appears twice except for one element which appears only once.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> XOR operator `^` properties: `x ^ x = 0` and `x ^ 0 = x`. Every paired number cancels itself out to 0, leaving only the unique lone number.

### 3. Step-by-Step Progressive Hints
- Hint 1: XOR all numbers together: `res = 0; for n in nums: res ^= n`.
- Hint 2: Return `res`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = 0`.
2. For each `n` in `nums`:
   - `res ^= n`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def singleNumber(self, nums: list[int]) -> int:
        res = 0
        for n in nums:
            res = n ^ res
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass.`
- **Space Complexity:** `O(1) - Constant auxiliary variable.`

---

## <a id="145-number-of-1-bits"></a>145. Number of 1 Bits

- **Difficulty:** `Easy`
- **Pattern:** `Brian Kernighan's Algorithm (`n & (n - 1)`)`
- **LeetCode Reference:** [LeetCode #191](https://leetcode.com/problems/number-of-1-bits/)

### 1. Problem Statement
Write a function that takes the binary representation of a positive integer and returns the number of **set bits** (also known as the Hamming weight) it has.

#### Examples:
**Example 1:**
```text
Input: n = 11 (binary 1011)
Output: 3
Explanation: Contains three 1 bits.
```

**Example 2:**
```text
Input: n = 128 (binary 10000000)
Output: 1
Explanation: Contains one 1 bit.
```

#### Constraints:
- `1 <= n <= 2^31 - 1`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Brian Kernighan's bit hack: performing `n = n & (n - 1)` directly clears the lowest set 1-bit in `n` in a single operation, running in loops equal only to the number of 1-bits.

### 3. Step-by-Step Progressive Hints
- Hint 1: While `n > 0`, do `n &= (n - 1)` and increment `res += 1`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = 0`.
2. While `n`:
   - `n &= (n - 1)`
   - `res += 1`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0
        while n:
            n &= (n - 1)
            res += 1
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(1) - At most 32 operations for 32-bit integer.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="146-counting-bits"></a>146. Counting Bits

- **Difficulty:** `Easy`
- **Pattern:** `Bit DP with Offset (`dp[i] = 1 + dp[i - offset]`)`
- **LeetCode Reference:** [LeetCode #338](https://leetcode.com/problems/counting-bits/)

### 1. Problem Statement
Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (`0 <= i <= n`), `ans[i]` is the **number of 1's** in the binary representation of `i`.

#### Examples:
**Example 1:**
```text
Input: n = 2
Output: [0,1,1]
Explanation: 0 -> 0; 1 -> 1; 2 -> 10 (1 bit).
```

**Example 2:**
```text
Input: n = 5
Output: [0,1,1,2,1,2]
Explanation: 0:0, 1:1, 2:1, 3:2, 4:1, 5:2.
```

#### Constraints:
- `0 <= n <= 10^5`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Bit count recurrence with power-of-two offset: when `i` reaches a new power of 2 (`offset * 2 == i`), `dp[i]` is simply 1 (the leading bit) plus `dp[i - offset]`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Initialize `dp = [0] * (n + 1)`, `offset = 1`.
- Hint 2: If `offset * 2 == i`, update `offset = i`.
- Hint 3: `dp[i] = 1 + dp[i - offset]`.

### 4. Detailed Approach Walkthrough
1. `dp = [0] * (n + 1)`, `offset = 1`.
2. For `i` in range(1, n + 1):
   - If `offset * 2 == i`: `offset = i`
   - `dp[i] = 1 + dp[i - offset]`
3. Return `dp`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def countBits(self, n: int) -> list[int]:
        dp = [0] * (n + 1)
        offset = 1
        
        for i in range(1, n + 1):
            if offset * 2 == i:
                offset = i
            dp[i] = 1 + dp[i - offset]
            
        return dp
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Linear pass calculating each bit count in O(1).`
- **Space Complexity:** `O(1) extra space (excluding output array).`

---

## <a id="147-reverse-bits"></a>147. Reverse Bits

- **Difficulty:** `Easy`
- **Pattern:** `Bit Shift & Masking`
- **LeetCode Reference:** [LeetCode #190](https://leetcode.com/problems/reverse-bits/)

### 1. Problem Statement
Reverse bits of a given 32 bits unsigned integer.

#### Examples:
**Example 1:**
```text
Input: n = 00000010100101000001111010011100
Output: 964176192 (00111001011110000010100101000000)
Explanation: Reversed 32-bit representation.
```

#### Constraints:
- `The input must be a binary string of length 32`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Extracting bits from the right of `n` one-by-one with `(n >> i) & 1` and pushing them into the opposite left side `res | (bit << (31 - i))`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Loop `i` from 0 to 31.
- Hint 2: Extract bit `bit = (n >> i) & 1`.
- Hint 3: Set bit in result `res = res | (bit << (31 - i))`.

### 4. Detailed Approach Walkthrough
1. `res = 0`.
2. For `i` in range(32):
   - `bit = (n >> i) & 1`
   - `res = res | (bit << (31 - i))`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def reverseBits(self, n: int) -> int:
        res = 0
        for i in range(32):
            bit = (n >> i) & 1
            res = res | (bit << (31 - i))
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(1) - Fixed 32 loop iterations.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="148-missing-number"></a>148. Missing Number

- **Difficulty:** `Easy`
- **Pattern:** `XOR / Gauss Sum Formula`
- **LeetCode Reference:** [LeetCode #268](https://leetcode.com/problems/missing-number/)

### 1. Problem Statement
Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

#### Examples:
**Example 1:**
```text
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers. Missing number in [0,3] is 2.
```

**Example 2:**
```text
Input: nums = [0,1]
Output: 2
Explanation: Missing number is 2.
```

#### Constraints:
- `n == nums.length`
- `1 <= n <= 10^4`
- `0 <= nums[i] <= n`
- `All the numbers of nums are unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> XORing all actual array numbers with all expected numbers `0..n`. All matching numbers cancel out to 0, leaving only the missing number.

### 3. Step-by-Step Progressive Hints
- Hint 1: `res = len(nums)`. For `i` in range(`len(nums)`): `res += (i - nums[i])` (or XOR).

### 4. Detailed Approach Walkthrough
1. `res = len(nums)`.
2. For `i` in range(len(nums)):
   - `res += (i - nums[i])`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def missingNumber(self, nums: list[int]) -> int:
        res = len(nums)
        for i in range(len(nums)):
            res += (i - nums[i])
        return res

# Alternative XOR approach:
# res = len(nums)
# for i in range(len(nums)):
#     res ^= i ^ nums[i]
# return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single linear pass.`
- **Space Complexity:** `O(1) - Constant auxiliary memory.`

---

## <a id="149-sum-of-two-integers"></a>149. Sum of Two Integers

- **Difficulty:** `Medium`
- **Pattern:** `Bitwise Full Adder (`XOR` and `AND << 1`)`
- **LeetCode Reference:** [LeetCode #371](https://leetcode.com/problems/sum-of-two-integers/)

### 1. Problem Statement
Given two integers `a` and `b`, return the sum of the two integers without using the operators `+` and `-`.

#### Examples:
**Example 1:**
```text
Input: a = 1, b = 2
Output: 3
Explanation: Bitwise addition without + or -.
```

**Example 2:**
```text
Input: a = 2, b = 3
Output: 5
Explanation: 2 + 3 = 5.
```

#### Constraints:
- `-1000 <= a, b <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Hardware digital adder circuit: `a ^ b` computes addition without carry. `(a & b) << 1` computes the carry bits. Repeat until carry becomes 0.

### 3. Step-by-Step Progressive Hints
- Hint 1: In Python, integers have arbitrary precision, so mask with `0xffffffff` for 32-bit simulation.
- Hint 2: `carry = (a & b) << 1; a = (a ^ b); b = carry`.
- Hint 3: Handle 32-bit signed integer overflow at the end.

### 4. Detailed Approach Walkthrough
1. Mask `mask = 0xffffffff`.
2. While `b & mask > 0`:
   - `carry = (a & b) << 1`
   - `a = (a ^ b)`
   - `b = carry`
3. Return `(a & mask)` if `b > 0` else `a` (handle 32-bit sign bit `~(a ^ mask)`).

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def getSum(self, a: int, b: int) -> int:
        mask = 0xffffffff
        
        while (b & mask) > 0:
            carry = (a & b) << 1
            a = (a ^ b)
            b = carry
            
        # Handle 32-bit signed integer in Python
        return (a & mask) if b > 0 else a if a <= 0x7fffffff else ~(a ^ mask)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(1) - Bounded by 32 bits.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="150-reverse-integer"></a>150. Reverse Integer

- **Difficulty:** `Medium`
- **Pattern:** `Digit Extraction & 32-Bit Overflow Prevention`
- **LeetCode Reference:** [LeetCode #7](https://leetcode.com/problems/reverse-integer/)

### 1. Problem Statement
Given a signed 32-bit integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^31, 2^31 - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

#### Examples:
**Example 1:**
```text
Input: x = 123
Output: 321
Explanation: Reversed digits.
```

**Example 2:**
```text
Input: x = -123
Output: -321
Explanation: Sign preserved.
```

**Example 3:**
```text
Input: x = 120
Output: 21
Explanation: Leading zeros removed.
```

#### Constraints:
- `-2^31 <= x <= 2^31 - 1`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Popping digits from the back of `x` with `x % 10` and pushing them onto `res = res * 10 + digit`, while checking 32-bit integer boundaries before multiplying by 10.

### 3. Step-by-Step Progressive Hints
- Hint 1: Boundaries are `MIN = -2147483648` and `MAX = 2147483647`.
- Hint 2: If `res > MAX // 10 or (res == MAX // 10 and digit >= MAX % 10)`, overflow occurs: return 0.

### 4. Detailed Approach Walkthrough
1. `MIN = -2147483648, MAX = 2147483647, res = 0`.
2. While `x`:
   - Extract `digit = int(math.fmod(x, 10))`
   - `x = int(x / 10)`
   - Overflow check:
     - If `res > MAX // 10 or (res == MAX // 10 and digit >= MAX % 10)`: return 0
     - If `res < int(MIN / 10) or (res == int(MIN / 10) and digit <= int(math.fmod(MIN, 10)))`: return 0
   - `res = (res * 10) + digit`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
import math

class Solution:
    def reverse(self, x: int) -> int:
        MIN = -2147483648  # -2^31
        MAX = 2147483647   # 2^31 - 1
        
        res = 0
        while x:
            digit = int(math.fmod(x, 10))
            x = int(x / 10)
            
            if (res > MAX // 10 or 
                (res == MAX // 10 and digit >= MAX % 10)):
                return 0
            if (res < int(MIN / 10) or 
                (res == int(MIN / 10) and digit <= int(math.fmod(MIN, 10)))):
                return 0
            res = (res * 10) + digit
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log10(x)) - Number of digits in integer x (at most 10 digits).`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---
