# Chapter: Math & Geometry

> Math & Geometry problems require spatial reasoning, in-place matrix rotations, cycle detection, fast exponentiation, and arithmetic simulation.

**Total Questions in Topic:** 8

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 136 | [Rotate Image](#136-rotate-image) | **Medium** | `Layer-by-Layer 4-Way In-Place Rotation` | [#48](https://leetcode.com/problems/rotate-image/) |
| 137 | [Spiral Matrix](#137-spiral-matrix) | **Medium** | `4-Boundary Perimeter Traversal` | [#54](https://leetcode.com/problems/spiral-matrix/) |
| 138 | [Set Matrix Zeroes](#138-set-matrix-zeroes) | **Medium** | `O(1) Space In-Place Row/Col Flagging` | [#73](https://leetcode.com/problems/set-matrix-zeroes/) |
| 139 | [Happy Number](#139-happy-number) | **Easy** | `Floyd's Cycle Detection / Hash Set` | [#202](https://leetcode.com/problems/happy-number/) |
| 140 | [Plus One](#140-plus-one) | **Easy** | `Carry Array Simulation` | [#66](https://leetcode.com/problems/plus-one/) |
| 141 | [Pow(x, n)](#141-powx,-n) | **Medium** | `Binary Exponentiation (Divide and Conquer)` | [#50](https://leetcode.com/problems/powx-n/) |
| 142 | [Multiply Strings](#142-multiply-strings) | **Medium** | `Manual Multiplication Array Simulation` | [#43](https://leetcode.com/problems/multiply-strings/) |
| 143 | [Detect Squares](#143-detect-squares) | **Medium** | `Diagonal Point Matching Hash Map` | [#2013](https://leetcode.com/problems/detect-squares/) |

---

## <a id="136-rotate-image"></a>136. Rotate Image

- **Difficulty:** `Medium`
- **Pattern:** `Layer-by-Layer 4-Way In-Place Rotation`
- **LeetCode Reference:** [LeetCode #48](https://leetcode.com/problems/rotate-image/)

### 1. Problem Statement
You are given an `n x n` 2D matrix representing an image, rotate the image by **90 degrees (clockwise)**.

You have to rotate the image **in-place**, which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

#### Examples:
**Example 1:**
```text
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
Explanation: Rotated 90 degrees clockwise in-place.
```

#### Constraints:
- `n == matrix.length == matrix[i].length`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Rotating concentric square onion layers: for each square ring bounded by `l, r, top, bottom`, perform a 4-way cyclic shift of four corner pixels counter-clockwise in reverse order.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain pointers `l = 0, r = len(matrix) - 1`.
- Hint 2: For each layer, loop `i` from 0 to `r - l - 1` and rotate the 4 corresponding edge cells.
- Hint 3: Save `top_left = matrix[top][l + i]`, then shift bottom-left -> top-left, bottom-right -> bottom-left, top-right -> bottom-right, saved top-left -> top-right.

### 4. Detailed Approach Walkthrough
1. `l, r = 0, len(matrix) - 1`.
2. While `l < r`:
   - For `i` in range(`r - l`):
     - `top, bottom = l, r`
     - `topLeft = matrix[top][l + i]`
     - `matrix[top][l + i] = matrix[bottom - i][l]`
     - `matrix[bottom - i][l] = matrix[bottom][r - i]`
     - `matrix[bottom][r - i] = matrix[top + i][r]`
     - `matrix[top + i][r] = topLeft`
   - `l += 1; r -= 1`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def rotate(self, matrix: list[list[int]]) -> None:
        l, r = 0, len(matrix) - 1
        
        while l < r:
            for i in range(r - l):
                top, bottom = l, r
                
                # Save top-left
                topLeft = matrix[top][l + i]
                
                # Move bottom-left into top-left
                matrix[top][l + i] = matrix[bottom - i][l]
                
                # Move bottom-right into bottom-left
                matrix[bottom - i][l] = matrix[bottom][r - i]
                
                # Move top-right into bottom-right
                matrix[bottom][r - i] = matrix[top + i][r]
                
                # Move saved top-left into top-right
                matrix[top + i][r] = topLeft
                
            r -= 1
            l += 1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N^2) - Every cell in the N x N grid is moved once.`
- **Space Complexity:** `O(1) - In-place rotation.`

---

## <a id="137-spiral-matrix"></a>137. Spiral Matrix

- **Difficulty:** `Medium`
- **Pattern:** `4-Boundary Perimeter Traversal`
- **LeetCode Reference:** [LeetCode #54](https://leetcode.com/problems/spiral-matrix/)

### 1. Problem Statement
Given an `m x n` `matrix`, return *all elements of the* `matrix` *in **spiral order***.

#### Examples:
**Example 1:**
```text
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
Explanation: Clockwise spiral path.
```

#### Constraints:
- `m == matrix.length, n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Peeling an apple in a spiral: traverse top row (left to right), shrink `top += 1`. Traverse right col (top to bottom), shrink `right -= 1`. Traverse bottom row (right to left), shrink `bottom -= 1`. Traverse left col (bottom to top), shrink `left += 1`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain four boundaries: `left = 0, right = COLS, top = 0, bottom = ROWS`.
- Hint 2: While `left < right and top < bottom`: traverse 4 perimeter segments in order and update boundaries.

### 4. Detailed Approach Walkthrough
1. `res = []`, `left, right = 0, len(matrix[0])`, `top, bottom = 0, len(matrix)`.
2. While `left < right and top < bottom`:
   - Top row: for `i` in `range(left, right)`: `res.append(matrix[top][i])`; `top += 1`
   - Right col: for `i` in `range(top, bottom)`: `res.append(matrix[i][right - 1])`; `right -= 1`
   - If not `(left < right and top < bottom)`: break
   - Bottom row: for `i` in `range(right - 1, left - 1, -1)`: `res.append(matrix[bottom - 1][i])`; `bottom -= 1`
   - Left col: for `i` in `range(bottom - 1, top - 1, -1)`: `res.append(matrix[i][left])`; `left += 1`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def spiralOrder(self, matrix: list[list[int]]) -> list[int]:
        res = []
        left, right = 0, len(matrix[0])
        top, bottom = 0, len(matrix)
        
        while left < right and top < bottom:
            # Get every i in top row
            for i in range(left, right):
                res.append(matrix[top][i])
            top += 1
            
            # Get every i in right col
            for i in range(top, bottom):
                res.append(matrix[i][right - 1])
            right -= 1
            
            if not (left < right and top < bottom):
                break
                
            # Get every i in bottom row
            for i in range(right - 1, left - 1, -1):
                res.append(matrix[bottom - 1][i])
            bottom -= 1
            
            # Get every i in left col
            for i in range(bottom - 1, top - 1, -1):
                res.append(matrix[i][left])
            left += 1
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(M * N) - Every element is visited once.`
- **Space Complexity:** `O(1) extra space (excluding output array).`

---

## <a id="138-set-matrix-zeroes"></a>138. Set Matrix Zeroes

- **Difficulty:** `Medium`
- **Pattern:** `O(1) Space In-Place Row/Col Flagging`
- **LeetCode Reference:** [LeetCode #73](https://leetcode.com/problems/set-matrix-zeroes/)

### 1. Problem Statement
Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it in place with `O(1)` extra memory.

#### Examples:
**Example 1:**
```text
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
Explanation: Row 1 and Column 1 set to 0.
```

#### Constraints:
- `m == matrix.length, n == matrix[0].length`
- `1 <= m, n <= 200`
- `-2^31 <= matrix[i][j] <= 2^31 - 1`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Using the top row and first column of the matrix itself as the scratchpad flags instead of allocating new memory. Use a single boolean variable `rowZero` to flag whether row 0 itself needs zeroing.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use `matrix[0][c]` and `matrix[r][0]` as indicators for zeroing col `c` and row `r`.
- Hint 2: Track `rowZero = False` separately for row 0 since `matrix[0][0]` overlaps with col 0.
- Hint 3: Zero out internal cells `(r, c)` from `1..ROWS-1, 1..COLS-1` first, then zero row 0 and col 0 last.

### 4. Detailed Approach Walkthrough
1. `ROWS, COLS = len(matrix), len(matrix[0])`, `rowZero = False`.
2. Mark flags in row 0 and col 0:
   - For `r` in range(ROWS), for `c` in range(COLS):
     - If `matrix[r][c] == 0`:
       - `matrix[0][c] = 0`
       - If `r > 0`: `matrix[r][0] = 0`
       - Else: `rowZero = True`
3. Zero out internal cells `r in 1..ROWS-1, c in 1..COLS-1` if `matrix[0][c] == 0 or matrix[r][0] == 0`.
4. If `matrix[0][0] == 0`: zero col 0.
5. If `rowZero`: zero row 0.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def setZeroes(self, matrix: list[list[int]]) -> None:
        ROWS, COLS = len(matrix), len(matrix[0])
        rowZero = False
        
        for r in range(ROWS):
            for c in range(COLS):
                if matrix[r][c] == 0:
                    matrix[0][c] = 0
                    if r > 0:
                        matrix[r][0] = 0
                    else:
                        rowZero = True
                        
        for r in range(1, ROWS):
            for c in range(1, COLS):
                if matrix[0][c] == 0 or matrix[r][0] == 0:
                    matrix[r][c] = 0
                    
        if matrix[0][0] == 0:
            for r in range(ROWS):
                matrix[r][0] = 0
                
        if rowZero:
            for c in range(COLS):
                matrix[0][c] = 0
```

### 6. Complexity Analysis
- **Time Complexity:** `O(M * N) - Matrix passes.`
- **Space Complexity:** `O(1) - Constant memory in-place.`

---

## <a id="139-happy-number"></a>139. Happy Number

- **Difficulty:** `Easy`
- **Pattern:** `Floyd's Cycle Detection / Hash Set`
- **LeetCode Reference:** [LeetCode #202](https://leetcode.com/problems/happy-number/)

### 1. Problem Statement
Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:
- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
- Those numbers for which this process ends in 1 are happy.

Return `true` if `n` is a happy number, and `false` if not.

#### Examples:
**Example 1:**
```text
Input: n = 19
Output: true
Explanation: 1^2 + 9^2 = 82 -> 8^2 + 2^2 = 68 -> 6^2 + 8^2 = 100 -> 1^2 + 0^2 + 0^2 = 1 (Happy!).
```

**Example 2:**
```text
Input: n = 2
Output: false
Explanation: Loops infinitely in an unhappy cycle.
```

#### Constraints:
- `1 <= n <= 2^31 - 1`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Detecting an infinite loop in numeric transformations: replace `n` with sum of squared digits. If `n == 1`, happy! If you encounter a number already in your `visit` set, you are caught in an endless cycle and will never reach 1.

### 3. Step-by-Step Progressive Hints
- Hint 1: Write helper `sumOfSquares(n)` to calculate sum of digits squared.
- Hint 2: Use a hash set `visit` to detect cycles. Loop while `n not in visit`.
- Hint 3: Return `n == 1`.

### 4. Detailed Approach Walkthrough
1. `visit = set()`.
2. While `n not in visit`:
   - `visit.add(n)`
   - `n = self.sumSquareDigits(n)`
   - If `n == 1`: return `True`
3. Return `False`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isHappy(self, n: int) -> bool:
        visit = set()
        
        while n not in visit:
            visit.add(n)
            n = self.sumSquareDigits(n)
            if n == 1:
                return True
        return False
        
    def sumSquareDigits(self, n):
        output = 0
        while n:
            digit = n % 10
            digit = digit ** 2
            output += digit
            n = n // 10
        return output
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log n) - Number of digits is proportional to log10(n).`
- **Space Complexity:** `O(log n) - Visited hash set.`

---

## <a id="140-plus-one"></a>140. Plus One

- **Difficulty:** `Easy`
- **Pattern:** `Carry Array Simulation`
- **LeetCode Reference:** [LeetCode #66](https://leetcode.com/problems/plus-one/)

### 1. Problem Statement
You are given a **large integer** represented as an integer array `digits`, where each `digits[i]` is the `i-th` digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading `0`'s.

Increment the large integer by one and return the **resulting array of digits**.

#### Examples:
**Example 1:**
```text
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: 123 + 1 = 124.
```

**Example 2:**
```text
Input: digits = [9]
Output: [1,0]
Explanation: 9 + 1 = 10.
```

#### Constraints:
- `1 <= digits.length <= 100`
- `0 <= digits[i] <= 9`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Car odometer rollover: adding 1 to the units digit. If it is less than 9, increment and stop immediately. If it is 9, turn to 0 and carry over +1 to the next digit.

### 3. Step-by-Step Progressive Hints
- Hint 1: Iterate backwards from `len(digits) - 1`.
- Hint 2: If `digits[i] < 9`, increment `digits[i] += 1` and return `digits`.
- Hint 3: If `digits[i] == 9`, set `digits[i] = 0`. If loop ends, return `[1] + digits`.

### 4. Detailed Approach Walkthrough
1. For `i` in range(len(digits) - 1, -1, -1):
   - If `digits[i] < 9`:
     - `digits[i] += 1`
     - return `digits`
   - `digits[i] = 0`
2. Return `[1] + digits`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def plusOne(self, digits: list[int]) -> list[int]:
        for i in range(len(digits) - 1, -1, -1):
            if digits[i] < 9:
                digits[i] += 1
                return digits
            digits[i] = 0
            
        return [1] + digits
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass through digits.`
- **Space Complexity:** `O(1) in-place or O(n) for prepended 1.`

---

## <a id="141-powx,-n"></a>141. Pow(x, n)

- **Difficulty:** `Medium`
- **Pattern:** `Binary Exponentiation (Divide and Conquer)`
- **LeetCode Reference:** [LeetCode #50](https://leetcode.com/problems/powx-n/)

### 1. Problem Statement
Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., `x^n`).

#### Examples:
**Example 1:**
```text
Input: x = 2.00000, n = 10
Output: 1024.00000
Explanation: 2^10 = 1024.
```

**Example 2:**
```text
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2^-2 = 1/4 = 0.25.
```

#### Constraints:
- `-100.0 < x < 100.0`
- `-2^31 <= n <= 2^31 - 1`
- `n is an integer.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Fast doubling: to compute `2^100`, compute `res = 2^50`, then simply square it `res * res = 2^100` in 1 multiplication step instead of doing 50 individual multiplications.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `n < 0`, compute `helper(1/x, -n)`.
- Hint 2: If `n == 0`, return 1.
- Hint 3: `res = helper(x, n // 2); res = res * res`. If `n % 2 != 0`, return `x * res` else `res`.

### 4. Detailed Approach Walkthrough
1. Define `helper(x, n)`:
   - If `x == 0`: return 0
   - If `n == 0`: return 1
   - `res = helper(x, n // 2)`
   - `res = res * res`
   - Return `x * res` if `n % 2 != 0` else `res`
2. `res = helper(x, abs(n))`.
3. Return `res` if `n >= 0` else `1 / res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        def helper(x, n):
            if x == 0:
                return 0
            if n == 0:
                return 1
                
            res = helper(x, n // 2)
            res = res * res
            return x * res if n % 2 else res
            
        res = helper(x, abs(n))
        return res if n >= 0 else 1 / res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(log n) - Power halved at each recursive step.`
- **Space Complexity:** `O(log n) - Call stack depth.`

---

## <a id="142-multiply-strings"></a>142. Multiply Strings

- **Difficulty:** `Medium`
- **Pattern:** `Manual Multiplication Array Simulation`
- **LeetCode Reference:** [LeetCode #43](https://leetcode.com/problems/multiply-strings/)

### 1. Problem Statement
Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.

**Note:** You must not use any built-in BigInteger library or convert the inputs to integer directly.

#### Examples:
**Example 1:**
```text
Input: num1 = "2", num2 = "3"
Output: "6"
Explanation: 2 * 3 = 6.
```

**Example 2:**
```text
Input: num1 = "123", num2 = "456"
Output: "56088"
Explanation: 123 * 456 = 56088.
```

#### Constraints:
- `1 <= num1.length, num2.length <= 200`
- `num1 and num2 consist of digits only.`
- `Both num1 and num2 do not contain any leading zero, except the number 0 itself.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Elementary long multiplication grid: multiplying digit at index `i` with digit at index `j` contributes to position `i + j` and carry to `i + j + 1` in the result array.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `"0" in [num1, num2]`, return `"0"`.
- Hint 2: Initialize `res = [0] * (len(num1) + len(num2))`.
- Hint 3: Reverse both strings and compute `res[i + j] += int(num1[i]) * int(num2[j])`, carry over `res[i + j + 1] += res[i + j] // 10`, `res[i + j] %= 10`.

### 4. Detailed Approach Walkthrough
1. If `"0" in [num1, num2]`: return `"0"`.
2. `res = [0] * (len(num1) + len(num2))`.
3. Reverse `num1 = num1[::-1]`, `num2 = num2[::-1]`.
4. For `i1` in range(len(num1)):
   - For `i2` in range(len(num2)):
     - `digit = int(num1[i1]) * int(num2[i2])`
     - `res[i1 + i2] += digit`
     - `res[i1 + i2 + 1] += res[i1 + i2] // 10`
     - `res[i1 + i2] %= 10`
5. Reverse `res = res[::-1]`, skip leading zeros, return string.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        if "0" in [num1, num2]:
            return "0"
            
        res = [0] * (len(num1) + len(num2))
        num1, num2 = num1[::-1], num2[::-1]
        
        for i1 in range(len(num1)):
            for i2 in range(len(num2)):
                digit = int(num1[i1]) * int(num2[i2])
                res[i1 + i2] += digit
                res[i1 + i2 + 1] += res[i1 + i2] // 10
                res[i1 + i2] %= 10
                
        res, beg = res[::-1], 0
        while beg < len(res) and res[beg] == 0:
            beg += 1
            
        return "".join(str(d) for d in res[beg:])
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * M) - Where N and M are string lengths.`
- **Space Complexity:** `O(N + M) - Result digit buffer.`

---

## <a id="143-detect-squares"></a>143. Detect Squares

- **Difficulty:** `Medium`
- **Pattern:** `Diagonal Point Matching Hash Map`
- **LeetCode Reference:** [LeetCode #2013](https://leetcode.com/problems/detect-squares/)

### 1. Problem Statement
You are given a stream of points on the X-Y plane. Design an algorithm that:
- Adds new points from the stream into a data structure. Duplicate points are allowed and should be treated as different points.
- Given a query point, counts the number of ways to choose three points from the data structure such that the three points and the query point form an **axis-aligned square** with **positive area**.

Implement the `DetectSquares` class:
- `DetectSquares()` Initializes the object.
- `void add(int[] point)` Adds a new point `point = [x, y]`.
- `int count(int[] point)` Counts the number of ways to form axis-aligned squares with query point `[x, y]`.

#### Examples:
**Example 1:**
```text
Input: ["DetectSquares", "add", "add", "add", "count", "count", "add", "count"]
[[], [[3, 10]], [[11, 2]], [[3, 2]], [[11, 10]], [[14, 8]], [[11, 2]], [[11, 10]]]
Output: [null, null, null, null, 1, 0, null, 2]
Explanation: DetectSquares detectSquares = new DetectSquares();
detectSquares.add([3, 10]);
detectSquares.add([11, 2]);
detectSquares.add([3, 2]);
detectSquares.count([11, 10]); // return 1
detectSquares.count([14, 8]);  // return 0
detectSquares.add([11, 2]);    // adds duplicate
detectSquares.count([11, 10]); // return 2
```

#### Constraints:
- `point.length == 2`
- `0 <= x, y <= 1000`
- `At most 3000 calls in total will be made to add and count.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Finding square diagonals: given query point `(qx, qy)`, iterate through all candidate opposite diagonal points `(x, y)` where `abs(qx - x) == abs(qy - y) > 0`. The square is completed if both corner points `(qx, y)` and `(x, qy)` exist in the coordinate counter.

### 3. Step-by-Step Progressive Hints
- Hint 1: Store points in `ptsCount = collections.defaultdict(int)` mapping `(x, y) -> count` and a list `pts = []`.
- Hint 2: In `count([qx, qy])`, iterate over diagonal candidate points `(x, y)` in `pts`.
- Hint 3: If `abs(qx - x) == abs(qy - y) and qx != x and qy != y`, add `ptsCount[(x, qy)] * ptsCount[(qx, y)]` to `res`.

### 4. Detailed Approach Walkthrough
1. `ptsCount = collections.defaultdict(int)`, `pts = []`.
2. `add(point)`: `ptsCount[tuple(point)] += 1`, `pts.append(point)`.
3. `count(point)`:
   - `qx, qy = point`, `res = 0`
   - For `x, y` in `pts`:
     - If `abs(qx - x) != abs(qy - y) or qx == x or qy == y`: continue
     - `res += ptsCount[(x, qy)] * ptsCount[(qx, y)]`
   - Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class DetectSquares:
    def __init__(self):
        self.ptsCount = collections.defaultdict(int)
        self.pts = []

    def add(self, point: list[int]) -> None:
        self.ptsCount[tuple(point)] += 1
        self.pts.append(point)

    def count(self, point: list[int]) -> int:
        res = 0
        qx, qy = point
        
        for x, y in self.pts:
            if (abs(qy - y) != abs(qx - x)) or qx == x or qy == y:
                continue
            res += self.ptsCount[(x, qy)] * self.ptsCount[(qx, y)]
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `add: O(1); count: O(N) where N is total number of added points.`
- **Space Complexity:** `O(N) - Points list and frequency dictionary.`

---
