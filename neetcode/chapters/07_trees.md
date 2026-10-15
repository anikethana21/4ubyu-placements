# Chapter: Trees

> Binary Trees and Binary Search Trees (BSTs) require recursive thinking (DFS - Preorder, Inorder, Postorder) and level-by-level queue traversal (BFS).

**Total Questions in Topic:** 15

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 46 | [Invert Binary Tree](#46-invert-binary-tree) | **Easy** | `Recursive DFS (Postorder / Preorder)` | [#226](https://leetcode.com/problems/invert-binary-tree/) |
| 47 | [Maximum Depth of Binary Tree](#47-maximum-depth-of-binary-tree) | **Easy** | `Recursive DFS / BFS` | [#104](https://leetcode.com/problems/maximum-depth-of-binary-tree/) |
| 48 | [Diameter of Binary Tree](#48-diameter-of-binary-tree) | **Easy** | `Bottom-Up DFS (Postorder)` | [#543](https://leetcode.com/problems/diameter-of-binary-tree/) |
| 49 | [Balanced Binary Tree](#49-balanced-binary-tree) | **Easy** | `Bottom-Up DFS with Early Exit` | [#110](https://leetcode.com/problems/balanced-binary-tree/) |
| 50 | [Same Tree](#50-same-tree) | **Easy** | `Recursive Tree Matching` | [#100](https://leetcode.com/problems/same-tree/) |
| 51 | [Subtree of Another Tree](#51-subtree-of-another-tree) | **Easy** | `Tree Matching DFS` | [#572](https://leetcode.com/problems/subtree-of-another-tree/) |
| 52 | [Lowest Common Ancestor of a BST](#52-lowest-common-ancestor-of-a-bst) | **Medium** | `BST Property Traversal` | [#235](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) |
| 53 | [Binary Tree Level Order Traversal](#53-binary-tree-level-order-traversal) | **Medium** | `BFS Queue Traversal` | [#102](https://leetcode.com/problems/binary-tree-level-order-traversal/) |
| 54 | [Binary Tree Right Side View](#54-binary-tree-right-side-view) | **Medium** | `BFS Level Last Element / DFS Right-First` | [#199](https://leetcode.com/problems/binary-tree-right-side-view/) |
| 55 | [Count Good Nodes in Binary Tree](#55-count-good-nodes-in-binary-tree) | **Medium** | `DFS with Running Max Path Value` | [#1448](https://leetcode.com/problems/count-good-nodes-in-binary-tree/) |
| 56 | [Validate Binary Search Tree](#56-validate-binary-search-tree) | **Medium** | `DFS Valid Range Propagation` | [#98](https://leetcode.com/problems/validate-binary-search-tree/) |
| 57 | [Kth Smallest Element in a BST](#57-kth-smallest-element-in-a-bst) | **Medium** | `Inorder Traversal (Sorted Order)` | [#230](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) |
| 58 | [Construct Binary Tree from Preorder and Inorder Traversal](#58-construct-binary-tree-from-preorder-and-inorder-traversal) | **Medium** | `Divide and Conquer Tree Reconstruction` | [#105](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) |
| 59 | [Binary Tree Maximum Path Sum](#59-binary-tree-maximum-path-sum) | **Hard** | `Bottom-Up DFS with Split Max` | [#124](https://leetcode.com/problems/binary-tree-maximum-path-sum/) |
| 60 | [Serialize and Deserialize Binary Tree](#60-serialize-and-deserialize-binary-tree) | **Hard** | `Preorder DFS Serialization` | [#297](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) |

---

## <a id="46-invert-binary-tree"></a>46. Invert Binary Tree

- **Difficulty:** `Easy`
- **Pattern:** `Recursive DFS (Postorder / Preorder)`
- **LeetCode Reference:** [LeetCode #226](https://leetcode.com/problems/invert-binary-tree/)

### 1. Problem Statement
Given the `root` of a binary tree, invert the tree, and return its root.

#### Examples:
**Example 1:**
```text
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
Explanation: Every node's left and right children are swapped.
```

**Example 2:**
```text
Input: root = [2,1,3]
Output: [2,3,1]
Explanation: Left child 1 and right child 3 are swapped.
```

#### Constraints:
- `The number of nodes in the tree is in the range [0, 100].`
- `-100 <= Node.val <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Holding a mirror in front of the tree: every branch flips with its opposite counterpart.

### 3. Step-by-Step Progressive Hints
- Hint 1: Base case: if `root is None`, return `None`.
- Hint 2: Swap `root.left` and `root.right`.
- Hint 3: Recursively call `invertTree` on both children.

### 4. Detailed Approach Walkthrough
1. Base case: If `not root`, return `None`.
2. Swap children: `root.left, root.right = root.right, root.left`.
3. Recurse: `self.invertTree(root.left)` and `self.invertTree(root.right)`.
4. Return `root`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
            
        # Swap children
        root.left, root.right = root.right, root.left
        
        # Invert subtrees
        self.invertTree(root.left)
        self.invertTree(root.right)
        
        return root
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Visits every node once.`
- **Space Complexity:** `O(h) - Where h is tree height (O(log n) for balanced, O(n) for degenerate tree).`

---

## <a id="47-maximum-depth-of-binary-tree"></a>47. Maximum Depth of Binary Tree

- **Difficulty:** `Easy`
- **Pattern:** `Recursive DFS / BFS`
- **LeetCode Reference:** [LeetCode #104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

### 1. Problem Statement
Given the `root` of a binary tree, return its maximum depth.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

#### Examples:
**Example 1:**
```text
Input: root = [3,9,20,null,null,15,7]
Output: 3
Explanation: Longest path is 3 -> 20 -> 15 (depth 3).
```

#### Constraints:
- `The number of nodes in the tree is in the range [0, 10^4].`
- `-100 <= Node.val <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> The height of a building is 1 floor (the roof/root) plus the height of the tallest wing extending beneath it.

### 3. Step-by-Step Progressive Hints
- Hint 1: Base case: empty node has depth 0.
- Hint 2: Depth of any node is `1 + max(depth(left), depth(right))`.

### 4. Detailed Approach Walkthrough
1. If `not root`, return 0.
2. Return `1 + max(self.maxDepth(root.left), self.maxDepth(root.right))`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Visits each node once.`
- **Space Complexity:** `O(h) - Call stack depth equals tree height.`

---

## <a id="48-diameter-of-binary-tree"></a>48. Diameter of Binary Tree

- **Difficulty:** `Easy`
- **Pattern:** `Bottom-Up DFS (Postorder)`
- **LeetCode Reference:** [LeetCode #543](https://leetcode.com/problems/diameter-of-binary-tree/)

### 1. Problem Statement
Given the `root` of a binary tree, return the length of the **diameter** of the tree.

The **diameter** of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

#### Examples:
**Example 1:**
```text
Input: root = [1,2,3,4,5]
Output: 3
Explanation: Length of path [4,2,1,3] or [5,2,1,3] is 3 edges.
```

#### Constraints:
- `The number of nodes in the tree is in the range [1, 10^4].`
- `-100 <= Node.val <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> At any crossroad (node), the longest path turning around at this crossroad is the height of its left branch plus the height of its right branch.

### 3. Step-by-Step Progressive Hints
- Hint 1: For any node, the path length passing through it is `height(left) + height(right)`.
- Hint 2: Track a global `res = 0` variable and update `res = max(res, left + right)` during the height computation.

### 4. Detailed Approach Walkthrough
1. Initialize `res = 0`.
2. Define `dfs(node)`:
   - If `not node`: return 0
   - `left = dfs(node.left)`
   - `right = dfs(node.right)`
   - `res = max(res, left + right)`
   - Return `1 + max(left, right)` (height of subtree)
3. Call `dfs(root)` and return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        res = 0
        
        def dfs(curr):
            nonlocal res
            if not curr:
                return 0
            left = dfs(curr.left)
            right = dfs(curr.right)
            res = max(res, left + right)
            return 1 + max(left, right)
            
        dfs(root)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single DFS traversal.`
- **Space Complexity:** `O(h) - Call stack depth.`

---

## <a id="49-balanced-binary-tree"></a>49. Balanced Binary Tree

- **Difficulty:** `Easy`
- **Pattern:** `Bottom-Up DFS with Early Exit`
- **LeetCode Reference:** [LeetCode #110](https://leetcode.com/problems/balanced-binary-tree/)

### 1. Problem Statement
Given a binary tree, determine if it is **height-balanced** (a binary tree in which the depth of the two subtrees of every node never differs by more than one).

#### Examples:
**Example 1:**
```text
Input: root = [3,9,20,null,null,15,7]
Output: true
Explanation: Height difference at all subtrees is <= 1.
```

**Example 2:**
```text
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
Explanation: Left subtree is deeper by 2 levels.
```

#### Constraints:
- `The number of nodes in the tree is in the range [0, 5000].`
- `-10^4 <= Node.val <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A mobile sculpture hanging from the ceiling: at every balancing junction, the left and right dangling arms must differ in depth by at most 1 level.

### 3. Step-by-Step Progressive Hints
- Hint 1: A top-down approach computing heights repeatedly takes O(n^2).
- Hint 2: Return a pair `[is_balanced, height]` from bottom-up DFS to achieve O(n).

### 4. Detailed Approach Walkthrough
1. Define `dfs(root)` returning `[balanced (bool), height (int)]`:
   - If `not root`: return `[True, 0]`
   - `left, right = dfs(root.left), dfs(root.right)`
   - `balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1`
   - Return `[balanced, 1 + max(left[1], right[1])]`
2. Return `dfs(root)[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(root):
            if not root:
                return [True, 0]
            left, right = dfs(root.left), dfs(root.right)
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            return [balanced, 1 + max(left[1], right[1])]
            
        return dfs(root)[0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single postorder traversal.`
- **Space Complexity:** `O(h) - Recursion stack.`

---

## <a id="50-same-tree"></a>50. Same Tree

- **Difficulty:** `Easy`
- **Pattern:** `Recursive Tree Matching`
- **LeetCode Reference:** [LeetCode #100](https://leetcode.com/problems/same-tree/)

### 1. Problem Statement
Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

#### Examples:
**Example 1:**
```text
Input: p = [1,2,3], q = [1,2,3]
Output: true
Explanation: Identical structure and values.
```

**Example 2:**
```text
Input: p = [1,2], q = [1,null,2]
Output: false
Explanation: Structural difference.
```

#### Constraints:
- `The number of nodes in both trees is in the range [0, 100].`
- `-10^4 <= Node.val <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Verifying twin architectural blueprints: check if current rooms match, then verify both left wings and right wings match.

### 3. Step-by-Step Progressive Hints
- Hint 1: If both `p` and `q` are `None`, return `True`.
- Hint 2: If only one is `None` or `p.val != q.val`, return `False`.
- Hint 3: Recurse on `isSameTree(p.left, q.left)` and `isSameTree(p.right, q.right)`.

### 4. Detailed Approach Walkthrough
1. If `not p and not q`: return `True`.
2. If `not p or not q or p.val != q.val`: return `False`.
3. Return `self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if not p and not q:
            return True
        if not p or not q or p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Where n is the number of nodes in the smaller tree.`
- **Space Complexity:** `O(h) - Tree recursion depth.`

---

## <a id="51-subtree-of-another-tree"></a>51. Subtree of Another Tree

- **Difficulty:** `Easy`
- **Pattern:** `Tree Matching DFS`
- **LeetCode Reference:** [LeetCode #572](https://leetcode.com/problems/subtree-of-another-tree/)

### 1. Problem Statement
Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

#### Examples:
**Example 1:**
```text
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
Explanation: The subtree rooted at 4 matches subRoot perfectly.
```

#### Constraints:
- `The number of nodes in root is in [1, 2000].`
- `The number of nodes in subRoot is in [1, 1000].`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Looking for an exact template stamp within a large sprawling tapestry.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `subRoot` is `None`, an empty tree is always a subtree (return True).
- Hint 2: If `root` is `None`, return False.
- Hint 3: If `sameTree(root, subRoot)` is True, return True. Otherwise check `isSubtree(root.left, subRoot) or isSubtree(root.right, subRoot)`.

### 4. Detailed Approach Walkthrough
1. If `not subRoot`: return `True`.
2. If `not root`: return `False`.
3. If `self.sameTree(root, subRoot)`: return `True`.
4. Return `self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not subRoot:
            return True
        if not root:
            return False
        if self.sameTree(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
        
    def sameTree(self, s, t):
        if not s and not t:
            return True
        if s and t and s.val == t.val:
            return self.sameTree(s.left, t.left) and self.sameTree(s.right, t.right)
        return False
```

### 6. Complexity Analysis
- **Time Complexity:** `O(m * n) - In the worst case where m is size of root and n is size of subRoot.`
- **Space Complexity:** `O(h) - Height of main tree.`

---

## <a id="52-lowest-common-ancestor-of-a-bst"></a>52. Lowest Common Ancestor of a BST

- **Difficulty:** `Medium`
- **Pattern:** `BST Property Traversal`
- **LeetCode Reference:** [LeetCode #235](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

### 1. Problem Statement
Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

#### Examples:
**Example 1:**
```text
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: LCA of nodes 2 and 8 is 6.
```

**Example 2:**
```text
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: LCA of 2 and 4 is 2 itself.
```

#### Constraints:
- `The number of nodes in the tree is in the range [2, 10^5].`
- `All Node.val are unique.`
- `p != q`
- `p and q will exist in the BST.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> In a sorted family tree, if both targets are larger than you, their ancestor must be in the right wing. If both are smaller, in the left wing. The moment the paths split (one smaller, one larger, or you are one of the targets), YOU are their lowest common ancestor.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use the BST property: all values in `root.left` < `root.val` < all values in `root.right`.
- Hint 2: If both `p.val` and `q.val` are greater than `curr.val`, move right `curr = curr.right`.
- Hint 3: If both are less, move left `curr = curr.left`. Otherwise, `curr` is the split point (LCA).

### 4. Detailed Approach Walkthrough
1. Initialize `curr = root`.
2. While `curr`:
   - If `p.val > curr.val` and `q.val > curr.val`: `curr = curr.right`
   - Else if `p.val < curr.val` and `q.val < curr.val`: `curr = curr.left`
   - Else: return `curr`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        curr = root
        while curr:
            if p.val > curr.val and q.val > curr.val:
                curr = curr.right
            elif p.val < curr.val and q.val < curr.val:
                curr = curr.left
            else:
                return curr
```

### 6. Complexity Analysis
- **Time Complexity:** `O(h) - Where h is tree height (O(log n) for balanced BST).`
- **Space Complexity:** `O(1) - Iterative traversal uses constant memory.`

---

## <a id="53-binary-tree-level-order-traversal"></a>53. Binary Tree Level Order Traversal

- **Difficulty:** `Medium`
- **Pattern:** `BFS Queue Traversal`
- **LeetCode Reference:** [LeetCode #102](https://leetcode.com/problems/binary-tree-level-order-traversal/)

### 1. Problem Statement
Given the `root` of a binary tree, return the **level order traversal** of its nodes' values. (i.e., from left to right, level by level).

#### Examples:
**Example 1:**
```text
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
Explanation: Values grouped level by level.
```

#### Constraints:
- `The number of nodes in the tree is in the range [0, 2000].`
- `-1000 <= Node.val <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Taking a roll call floor-by-floor in an office building: finish listing everyone on Floor 1 before moving to Floor 2.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a FIFO queue (`collections.deque`).
- Hint 2: At each step, snapshot `len(q)` to process all nodes of the current level together.
- Hint 3: Pop each node, append its value to `level`, and push non-null children into the queue.

### 4. Detailed Approach Walkthrough
1. If `not root`, return `[]`.
2. Initialize `res = []` and `q = collections.deque([root])`.
3. While `q`:
   - `level = []`
   - For `_` in range(`len(q)`):
     - `node = q.popleft()`
     - `level.append(node.val)`
     - If `node.left`: `q.append(node.left)`
     - If `node.right`: `q.append(node.right)`
   - `res.append(level)`
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> list[list[int]]:
        res = []
        q = collections.deque()
        if root:
            q.append(root)
            
        while q:
            val = []
            for i in range(len(q)):
                node = q.popleft()
                val.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            res.append(val)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Each node is enqueued and dequeued exactly once.`
- **Space Complexity:** `O(n) - Queue holds up to n/2 leaf nodes.`

---

## <a id="54-binary-tree-right-side-view"></a>54. Binary Tree Right Side View

- **Difficulty:** `Medium`
- **Pattern:** `BFS Level Last Element / DFS Right-First`
- **LeetCode Reference:** [LeetCode #199](https://leetcode.com/problems/binary-tree-right-side-view/)

### 1. Problem Statement
Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return the values of the nodes you can see ordered from top to bottom.

#### Examples:
**Example 1:**
```text
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
Explanation: Rightmost visible nodes from top to bottom.
```

#### Constraints:
- `The number of nodes in the tree is in the range [0, 100].`
- `-100 <= Node.val <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Looking at the silhouette of a mountain range from the east: only the rightmost peak at each elevation level is visible.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use BFS level order traversal.
- Hint 2: At each level, the last node popped from the queue is the rightmost node visible from the right side.

### 4. Detailed Approach Walkthrough
1. Initialize `res = []`, `q = collections.deque([root] if root else [])`.
2. While `q`:
   - `rightSide = None`
   - For `_` in range(`len(q)`):
     - `node = q.popleft()`
     - If `node`: `rightSide = node; if node.left: q.append(node.left); if node.right: q.append(node.right)`
   - If `rightSide`: `res.append(rightSide.val)`
3. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> list[int]:
        res = []
        q = collections.deque([root])
        
        while q:
            rightSide = None
            for i in range(len(q)):
                node = q.popleft()
                if node:
                    rightSide = node
                    q.append(node.left)
                    q.append(node.right)
            if rightSide:
                res.append(rightSide.val)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Visits each node once.`
- **Space Complexity:** `O(n) - BFS queue space.`

---

## <a id="55-count-good-nodes-in-binary-tree"></a>55. Count Good Nodes in Binary Tree

- **Difficulty:** `Medium`
- **Pattern:** `DFS with Running Max Path Value`
- **LeetCode Reference:** [LeetCode #1448](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)

### 1. Problem Statement
Given a binary tree `root`, a node `X` in the tree is named **good** if in the path from the root to `X` there are no nodes with a value greater than `X`.

Return the number of **good** nodes in the binary tree.

#### Examples:
**Example 1:**
```text
Input: root = [3,1,4,3,null,1,5]
Output: 4
Explanation: Root (3), (4), (5), and (3) are good nodes.
```

#### Constraints:
- `The number of nodes in the binary tree is in the range [1, 10^5].`
- `Each node's value is between [-10^4, 10^4].`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Climbing a mountain path: a viewpoint is 'good' if you can look straight back down to base camp without any taller peak blocking your line of sight.

### 3. Step-by-Step Progressive Hints
- Hint 1: Pass the maximum value encountered so far along the root-to-node path into the recursive DFS helper.
- Hint 2: If `node.val >= maxVal`, count it (`res = 1`), update `maxVal = max(maxVal, node.val)`, and recurse into children.

### 4. Detailed Approach Walkthrough
1. Define `dfs(node, maxVal)`:
   - If `not node`: return 0
   - `res = 1 if node.val >= maxVal else 0`
   - `maxVal = max(maxVal, node.val)`
   - `res += dfs(node.left, maxVal) + dfs(node.right, maxVal)`
   - Return `res`
2. Return `dfs(root, root.val)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def countGoodNodes(self, root: TreeNode) -> int:
        def dfs(node, maxVal):
            if not node:
                return 0
            res = 1 if node.val >= maxVal else 0
            maxVal = max(maxVal, node.val)
            res += dfs(node.left, maxVal)
            res += dfs(node.right, maxVal)
            return res
            
        return dfs(root, root.val)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single DFS traversal.`
- **Space Complexity:** `O(h) - Height of the binary tree.`

---

## <a id="56-validate-binary-search-tree"></a>56. Validate Binary Search Tree

- **Difficulty:** `Medium`
- **Pattern:** `DFS Valid Range Propagation`
- **LeetCode Reference:** [LeetCode #98](https://leetcode.com/problems/validate-binary-search-tree/)

### 1. Problem Statement
Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).

A **valid BST** is defined as follows:
- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

#### Examples:
**Example 1:**
```text
Input: root = [2,1,3]
Output: true
Explanation: Valid BST.
```

**Example 2:**
```text
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: Root value is 5 but right child's left value is 3 <= 5.
```

#### Constraints:
- `The number of nodes in the tree is in the range [1, 10^4].`
- `-2^31 <= Node.val <= 2^31 - 1`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Every node must satisfy not just its direct parent, but the combined boundary restrictions of ALL its ancestors: `left_bound < node.val < right_bound`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Checking only `node.left.val < node.val` is insufficient because values deep in the right subtree cannot violate root constraints.
- Hint 2: Pass down valid range `(left, right)` where initially `left = -inf, right = inf`.
- Hint 3: When going left, update upper bound `valid(node.left, left, node.val)`. When going right, update lower bound `valid(node.right, node.val, right)`.

### 4. Detailed Approach Walkthrough
1. Define `valid(node, left, right)`:
   - If `not node`: return `True`
   - If not `(left < node.val < right)`: return `False`
   - Return `valid(node.left, left, node.val) and valid(node.right, node.val, right)`
2. Return `valid(root, float('-inf'), float('inf'))`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def valid(node, left, right):
            if not node:
                return True
            if not (left < node.val < right):
                return False
            return valid(node.left, left, node.val) and valid(node.right, node.val, right)
            
        return valid(root, float("-inf"), float("inf"))
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Visits each node once.`
- **Space Complexity:** `O(h) - Recursion stack.`

---

## <a id="57-kth-smallest-element-in-a-bst"></a>57. Kth Smallest Element in a BST

- **Difficulty:** `Medium`
- **Pattern:** `Inorder Traversal (Sorted Order)`
- **LeetCode Reference:** [LeetCode #230](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

### 1. Problem Statement
Given the `root` of a binary search tree, and an integer `k`, return the `k-th` smallest value (**1-indexed**) of all the values of the nodes in the tree.

#### Examples:
**Example 1:**
```text
Input: root = [3,1,4,null,2], k = 1
Output: 1
Explanation: Smallest value is 1.
```

**Example 2:**
```text
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
Explanation: Sorted order: [1, 2, 3, 4, 5, 6]. 3rd smallest is 3.
```

#### Constraints:
- `The number of nodes in the tree is n.`
- `1 <= k <= n <= 10^4`
- `0 <= Node.val <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> An in-order traversal (Left, Root, Right) on any BST visits all elements in strictly ascending sorted order. The k-th visited node is the k-th smallest element.

### 3. Step-by-Step Progressive Hints
- Hint 1: In-order traversal visits BST elements in sorted order.
- Hint 2: Use an iterative stack to simulate in-order traversal and stop immediately when `n == k`.

### 4. Detailed Approach Walkthrough
1. Initialize `stack = []`, `curr = root`, `n = 0`.
2. While `curr` or `stack`:
   - While `curr`: `stack.append(curr); curr = curr.left`
   - `curr = stack.pop()`
   - `n += 1`
   - If `n == k`: return `curr.val`
   - `curr = curr.right`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        curr = root
        n = 0
        
        while curr or stack:
            while curr:
                stack.append(curr)
                curr = curr.left
            curr = stack.pop()
            n += 1
            if n == k:
                return curr.val
            curr = curr.right
```

### 6. Complexity Analysis
- **Time Complexity:** `O(H + k) - Where H is tree height.`
- **Space Complexity:** `O(H) - Stack holds at most height of tree.`

---

## <a id="58-construct-binary-tree-from-preorder-and-inorder-traversal"></a>58. Construct Binary Tree from Preorder and Inorder Traversal

- **Difficulty:** `Medium`
- **Pattern:** `Divide and Conquer Tree Reconstruction`
- **LeetCode Reference:** [LeetCode #105](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

### 1. Problem Statement
Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

#### Examples:
**Example 1:**
```text
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
Explanation: Root is 3. Inorder splits into left subtree [9] and right subtree [15,20,7].
```

#### Constraints:
- `1 <= preorder.length <= 3000`
- `inorder.length == preorder.length`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder and inorder consist of unique values.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> `preorder[0]` always reveals the King (root). Finding the King's location in `inorder` cleanly divides the entire kingdom into the left court (left subtree) and right court (right subtree).

### 3. Step-by-Step Progressive Hints
- Hint 1: First value of `preorder` is always the root of the current subtree.
- Hint 2: Find `mid = inorder.index(preorder[0])`. All values left of `mid` belong to `root.left`; all values right belong to `root.right`.
- Hint 3: Recurse on `preorder[1:mid+1]` with `inorder[:mid]`, and `preorder[mid+1:]` with `inorder[mid+1:]`.

### 4. Detailed Approach Walkthrough
1. If `not preorder` or `not inorder`: return `None`.
2. `root = TreeNode(preorder[0])`.
3. `mid = inorder.index(preorder[0])`.
4. `root.left = self.buildTree(preorder[1 : mid + 1], inorder[:mid])`.
5. `root.right = self.buildTree(preorder[mid + 1 :], inorder[mid + 1 :])`.
6. Return `root`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def buildTree(self, preorder: list[int], inorder: list[int]) -> Optional[TreeNode]:
        if not preorder or not inorder:
            return None
            
        root = TreeNode(preorder[0])
        mid = inorder.index(preorder[0])
        
        root.left = self.buildTree(preorder[1 : mid + 1], inorder[:mid])
        root.right = self.buildTree(preorder[mid + 1 :], inorder[mid + 1 :])
        
        return root
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n^2) naive with slicing/index or O(n) using a hash map for inorder indices.`
- **Space Complexity:** `O(n) - Tree nodes and recursion stack.`

---

## <a id="59-binary-tree-maximum-path-sum"></a>59. Binary Tree Maximum Path Sum

- **Difficulty:** `Hard`
- **Pattern:** `Bottom-Up DFS with Split Max`
- **LeetCode Reference:** [LeetCode #124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

### 1. Problem Statement
A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return the **maximum path sum** of any non-empty path.

#### Examples:
**Example 1:**
```text
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```

**Example 2:**
```text
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: Optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
```

#### Constraints:
- `The number of nodes in the tree is in the range [1, 3 * 10^4].`
- `-1000 <= Node.val <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> At any node, you can consider making this node the archway peak of a complete bridge: `node.val + max(0, leftGain) + max(0, rightGain)`. However, when reporting your value up to your parent, you can only extend ONE branch upward (left or right, not both).

### 3. Step-by-Step Progressive Hints
- Hint 1: Subtree gains can be negative, so take `max(0, gain)` to ignore detrimental branches.
- Hint 2: At each node, calculate the bridge path sum `node.val + leftMax + rightMax` and update global `res`.
- Hint 3: Return `node.val + max(leftMax, rightMax)` to the parent caller.

### 4. Detailed Approach Walkthrough
1. Initialize `res = [root.val]`.
2. Define `dfs(root)`:
   - If `not root`: return 0
   - `leftMax = max(dfs(root.left), 0)`
   - `rightMax = max(dfs(root.right), 0)`
   - Compute max path with split: `res[0] = max(res[0], root.val + leftMax + rightMax)`
   - Return max path without split to parent: `root.val + max(leftMax, rightMax)`
3. Call `dfs(root)` and return `res[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        res = [root.val]
        
        def dfs(root):
            if not root:
                return 0
                
            leftMax = max(dfs(root.left), 0)
            rightMax = max(dfs(root.right), 0)
            
            # Compute max path sum WITH split at current node
            res[0] = max(res[0], root.val + leftMax + rightMax)
            
            # Return WITHOUT split
            return root.val + max(leftMax, rightMax)
            
        dfs(root)
        return res[0]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Visits every node once.`
- **Space Complexity:** `O(h) - Height of binary tree.`

---

## <a id="60-serialize-and-deserialize-binary-tree"></a>60. Serialize and Deserialize Binary Tree

- **Difficulty:** `Hard`
- **Pattern:** `Preorder DFS Serialization`
- **LeetCode Reference:** [LeetCode #297](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

### 1. Problem Statement
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree.

#### Examples:
**Example 1:**
```text
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
Explanation: Serialized to a comma-separated string format and decoded back to the exact identical binary tree structure.
```

#### Constraints:
- `The number of nodes in the tree is in the range [0, 10^4].`
- `-1000 <= Node.val <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Recording audio instructions for building a Lego tree: whenever a branch has no child, say 'N' aloud. When reading the transcript back, create a node, then build its left branch, then its right branch.

### 3. Step-by-Step Progressive Hints
- Hint 1: Preorder traversal (Root -> Left -> Right) encoding `"N"` for null pointers uniquely identifies any tree structure without needing inorder traversal.
- Hint 2: Join serialized node tokens with `","`.
- Hint 3: For deserialization, split by `","` and use an index pointer or iterator to recursively reconstruct `node = TreeNode(int(val))`, `node.left = dfs()`, `node.right = dfs()`.

### 4. Detailed Approach Walkthrough
1. `serialize(root)`:
   - Use preorder DFS appending `str(node.val)` or `"N"` to `res` list.
   - Return `",".join(res)`.
2. `deserialize(data)`:
   - Split `vals = data.split(",")`, maintain pointer `self.i = 0`.
   - Define `dfs()`:
     - If `vals[self.i] == "N"`: increment `self.i += 1`; return `None`.
     - `node = TreeNode(int(vals[self.i]))`
     - `self.i += 1`
     - `node.left = dfs()`
     - `node.right = dfs()`
     - Return `node`.
   - Return `dfs()`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Codec:
    def serialize(self, root: Optional[TreeNode]) -> str:
        res = []
        def dfs(node):
            if not node:
                res.append("N")
                return
            res.append(str(node.val))
            dfs(node.left)
            dfs(node.right)
        dfs(root)
        return ",".join(res)

    def deserialize(self, data: str) -> Optional[TreeNode]:
        vals = data.split(",")
        self.i = 0
        
        def dfs():
            if vals[self.i] == "N":
                self.i += 1
                return None
            node = TreeNode(int(vals[self.i]))
            self.i += 1
            node.left = dfs()
            node.right = dfs()
            return node
            
        return dfs()
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) for both serialize and deserialize.`
- **Space Complexity:** `O(n) - To store string representation and node arrays.`

---
