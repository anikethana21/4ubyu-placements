# Chapter: Linked List

> Linked Lists store elements non-contiguously in memory linked via pointers. Mastering pointer reassignment, dummy sentinel heads, and fast/slow pointer techniques is crucial.

**Total Questions in Topic:** 11

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 35 | [Reverse Linked List](#35-reverse-linked-list) | **Easy** | `Iterative Pointer Reversal` | [#206](https://leetcode.com/problems/reverse-linked-list/) |
| 36 | [Merge Two Sorted Lists](#36-merge-two-sorted-lists) | **Easy** | `Dummy Sentinel Head + Two Pointers` | [#21](https://leetcode.com/problems/merge-two-sorted-lists/) |
| 37 | [Reorder List](#37-reorder-list) | **Medium** | `Fast & Slow + Reverse + Interleave` | [#143](https://leetcode.com/problems/reorder-list/) |
| 38 | [Remove Nth Node From End of List](#38-remove-nth-node-from-end-of-list) | **Medium** | `Two Pointers with Offset` | [#19](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) |
| 39 | [Copy List with Random Pointer](#39-copy-list-with-random-pointer) | **Medium** | `Hash Map Node Mapping / Interleaving` | [#138](https://leetcode.com/problems/copy-list-with-random-pointer/) |
| 40 | [Add Two Numbers](#40-add-two-numbers) | **Medium** | `Elementary Math / Carry Simulation` | [#2](https://leetcode.com/problems/add-two-numbers/) |
| 41 | [Linked List Cycle](#41-linked-list-cycle) | **Easy** | `Floyd's Tortoise and Hare` | [#141](https://leetcode.com/problems/linked-list-cycle/) |
| 42 | [Find the Duplicate Number](#42-find-the-duplicate-number) | **Medium** | `Floyd's Cycle Detection (Array as Linked List)` | [#287](https://leetcode.com/problems/find-the-duplicate-number/) |
| 43 | [LRU Cache](#43-lru-cache) | **Medium** | `Hash Map + Doubly Linked List` | [#146](https://leetcode.com/problems/lru-cache/) |
| 44 | [Merge K Sorted Lists](#44-merge-k-sorted-lists) | **Hard** | `Divide and Conquer (Merge Sort Lists)` | [#23](https://leetcode.com/problems/merge-k-sorted-lists/) |
| 45 | [Reverse Nodes in k-Group](#45-reverse-nodes-in-k-group) | **Hard** | `Segment Pointer Manipulation` | [#25](https://leetcode.com/problems/reverse-nodes-in-k-group/) |

---

## <a id="35-reverse-linked-list"></a>35. Reverse Linked List

- **Difficulty:** `Easy`
- **Pattern:** `Iterative Pointer Reversal`
- **LeetCode Reference:** [LeetCode #206](https://leetcode.com/problems/reverse-linked-list/)

### 1. Problem Statement
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

#### Examples:
**Example 1:**
```text
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
Explanation: Pointer arrows are completely reversed.
```

**Example 2:**
```text
Input: head = [1,2]
Output: [2,1]
Explanation: Reversed two-node list.
```

#### Constraints:
- `The number of nodes in the list is the range [0, 5000].`
- `-5000 <= Node.val <= 5000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a line of people holding onto the shoulder of the person ahead of them. To reverse the line, each person lets go of the person in front and turns around to grab the shoulder of the person who was behind them.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain two pointers: `prev = None` and `curr = head`.
- Hint 2: Before redirecting `curr.next = prev`, save `nxt = curr.next` so you don't lose the rest of the list.
- Hint 3: Advance `prev = curr` and `curr = nxt` until `curr` becomes `None`.

### 4. Detailed Approach Walkthrough
1. Initialize `prev = None` and `curr = head`.
2. While `curr` is not `None`:
   - Save next node: `nxt = curr.next`
   - Reverse pointer: `curr.next = prev`
   - Advance `prev = curr`
   - Advance `curr = nxt`
3. Return `prev` (new head).

### 5. Canonical NeetCode Python 3 Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev, curr = None, head
        
        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt
            
        return prev
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single linear traversal over n nodes.`
- **Space Complexity:** `O(1) - Iterative in-place pointer updates.`

---

## <a id="36-merge-two-sorted-lists"></a>36. Merge Two Sorted Lists

- **Difficulty:** `Easy`
- **Pattern:** `Dummy Sentinel Head + Two Pointers`
- **LeetCode Reference:** [LeetCode #21](https://leetcode.com/problems/merge-two-sorted-lists/)

### 1. Problem Statement
You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

#### Examples:
**Example 1:**
```text
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
Explanation: Merged list preserves ascending order.
```

**Example 2:**
```text
Input: list1 = [], list2 = []
Output: []
Explanation: Merging two empty lists yields empty list.
```

#### Constraints:
- `The number of nodes in both lists is in the range [0, 50].`
- `-100 <= Node.val <= 100`
- `Both list1 and list2 are sorted in non-decreasing order.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine two sorted decks of numbered playing cards. You compare the top card of each deck, pick the smaller one, place it face up onto the combined deck, and repeat until one deck runs out.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a `dummy = ListNode()` node to avoid edge cases when creating the new list's head.
- Hint 2: Compare `list1.val` and `list2.val`, attach the smaller node to `tail.next`, and advance that list.
- Hint 3: Once one list is exhausted, attach the remainder of the non-empty list directly to `tail.next`.

### 4. Detailed Approach Walkthrough
1. Create `dummy = ListNode()` and set `tail = dummy`.
2. While `list1` and `list2`:
   - If `list1.val < list2.val`:
     - `tail.next = list1`
     - `list1 = list1.next`
   - Else:
     - `tail.next = list2`
     - `list2 = list2.next`
   - `tail = tail.next`
3. Attach remaining nodes: `tail.next = list1 or list2`.
4. Return `dummy.next`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        tail = dummy
        
        while list1 and list2:
            if list1.val < list2.val:
                tail.next = list1
                list1 = list1.next
            else:
                tail.next = list2
                list2 = list2.next
            tail = tail.next
            
        tail.next = list1 or list2
        return dummy.next
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n + m) - Where n and m are lengths of list1 and list2.`
- **Space Complexity:** `O(1) - Merging is done by rewiring existing node pointers.`

---

## <a id="37-reorder-list"></a>37. Reorder List

- **Difficulty:** `Medium`
- **Pattern:** `Fast & Slow + Reverse + Interleave`
- **LeetCode Reference:** [LeetCode #143](https://leetcode.com/problems/reorder-list/)

### 1. Problem Statement
You are given the head of a singly linked-list: `L0 -> L1 -> ... -> Ln - 1 -> Ln`.

Reorder the list to be on the following form: `L0 -> Ln -> L1 -> Ln - 1 -> L2 -> Ln - 2 -> ...`

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

#### Examples:
**Example 1:**
```text
Input: head = [1,2,3,4]
Output: [1,4,2,3]
Explanation: Interleaved from front and back.
```

**Example 2:**
```text
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
Explanation: Interleaved from front and back.
```

#### Constraints:
- `The number of nodes in the list is in the range [1, 5 * 10^4].`
- `1 <= Node.val <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Think of dealing a deck of cards: split the deck exactly in half, flip the second half upside-down, and then riffle-shuffle the two halves alternating one card from each pile.

### 3. Step-by-Step Progressive Hints
- Hint 1: Find the middle of the linked list using fast and slow pointers (`slow = slow.next, fast = fast.next.next`).
- Hint 2: Reverse the second half of the list starting from `slow.next`.
- Hint 3: Merge the first half and the reversed second half by interleaving nodes alternately.

### 4. Detailed Approach Walkthrough
1. Find middle node using `slow, fast = head, head.next`.
2. Separate and reverse second half starting from `slow.next`. Set `slow.next = None`.
3. Reverse second half into `second`.
4. Merge `first = head` and `second` by alternating pointers:
   - `tmp1, tmp2 = first.next, second.next`
   - `first.next = second`
   - `second.next = tmp1`
   - `first, second = tmp1, tmp2`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        # 1. Find middle
        slow, fast = head, head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
        # 2. Reverse second half
        second = slow.next
        prev = slow.next = None
        while second:
            nxt = second.next
            second.next = prev
            prev = second
            second = nxt
            
        # 3. Merge two halves
        first, second = head, prev
        while second:
            tmp1, tmp2 = first.next, second.next
            first.next = second
            second.next = tmp1
            first, second = tmp1, tmp2
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Linear time for middle finding, reversal, and merge.`
- **Space Complexity:** `O(1) - Constant auxiliary memory in-place.`

---

## <a id="38-remove-nth-node-from-end-of-list"></a>38. Remove Nth Node From End of List

- **Difficulty:** `Medium`
- **Pattern:** `Two Pointers with Offset`
- **LeetCode Reference:** [LeetCode #19](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

### 1. Problem Statement
Given the `head` of a linked list, remove the `n-th` node from the end of the list and return its head.

#### Examples:
**Example 1:**
```text
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Explanation: 2nd node from end (4) is removed.
```

**Example 2:**
```text
Input: head = [1], n = 1
Output: []
Explanation: Single node removed yields empty list.
```

#### Constraints:
- `The number of nodes in the list is sz.`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine two walkers separated by a fixed tether of length `n`. When the lead walker reaches the finish line (`None`), the trailing walker is positioned exactly `n` steps behind, right at the node that needs to be unhooked.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a dummy node pointing to `head` to handle removing the head node cleanly.
- Hint 2: Advance `right` pointer `n` steps ahead of `left`.
- Hint 3: Move both `left` and `right` forward one node at a time until `right` reaches `None`. Then delete `left.next = left.next.next`.

### 4. Detailed Approach Walkthrough
1. Initialize `dummy = ListNode(0, head)`.
2. Set `left = dummy` and `right = head`.
3. Advance `right` by `n` steps.
4. While `right` is not `None`:
   - `left = left.next`
   - `right = right.next`
5. Delete the node: `left.next = left.next.next`.
6. Return `dummy.next`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        left = dummy
        right = head
        
        while n > 0 and right:
            right = right.next
            n -= 1
            
        while right:
            left = left.next
            right = right.next
            
        # Delete node
        left.next = left.next.next
        return dummy.next
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single linear pass over the list.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="39-copy-list-with-random-pointer"></a>39. Copy List with Random Pointer

- **Difficulty:** `Medium`
- **Pattern:** `Hash Map Node Mapping / Interleaving`
- **LeetCode Reference:** [LeetCode #138](https://leetcode.com/problems/copy-list-with-random-pointer/)

### 1. Problem Statement
A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a **deep copy** of the list. Return the head of the copied linked list.

#### Examples:
**Example 1:**
```text
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
Explanation: Deep copy reproduces all node values, next pointers, and random pointers identically.
```

#### Constraints:
- `0 <= n <= 1000`
- `-10^4 <= Node.val <= 10^4`
- `Node.random is null or is pointing to some node in the linked list.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine creating a cloned duplicate of a team where every person points to their direct teammate (`next`) and their best friend (`random`). Using a phone directory (hash map `old_person -> clone`), after creating clone bodies, you can link every clone's `next` and `random` directly to the clones of their friends.

### 3. Step-by-Step Progressive Hints
- Hint 1: In Pass 1, traverse the original list and create a new `Node(curr.val)` for each node, storing `oldToCopy[curr] = copy`.
- Hint 2: In Pass 2, set `copy.next = oldToCopy[curr.next]` and `copy.random = oldToCopy[curr.random]`.
- Hint 3: Map `None` to `None` in the hash map (`oldToCopy = {None: None}`) to handle null pointers without extra conditionals.

### 4. Detailed Approach Walkthrough
1. Initialize `oldToCopy = {None: None}`.
2. First pass: iterate `curr = head`, for each node create `copy = Node(curr.val)` and record `oldToCopy[curr] = copy`.
3. Second pass: iterate `curr = head`, set `copy = oldToCopy[curr]`, then `copy.next = oldToCopy[curr.next]` and `copy.random = oldToCopy[curr.random]`.
4. Return `oldToCopy[head]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        oldToCopy = {None: None}
        
        # Pass 1: Create cloned nodes
        curr = head
        while curr:
            copy = Node(curr.val)
            oldToCopy[curr] = copy
            curr = curr.next
            
        # Pass 2: Connect next and random pointers
        curr = head
        while curr:
            copy = oldToCopy[curr]
            copy.next = oldToCopy[curr.next]
            copy.random = oldToCopy[curr.random]
            curr = curr.next
            
        return oldToCopy[head]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Two linear passes over the list of n nodes.`
- **Space Complexity:** `O(n) - Hash map mapping original nodes to clones.`

---

## <a id="40-add-two-numbers"></a>40. Add Two Numbers

- **Difficulty:** `Medium`
- **Pattern:** `Elementary Math / Carry Simulation`
- **LeetCode Reference:** [LeetCode #2](https://leetcode.com/problems/add-two-numbers/)

### 1. Problem Statement
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

#### Examples:
**Example 1:**
```text
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807, represented as [7, 0, 8].
```

**Example 2:**
```text
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
Explanation: Handles carries across unequal length lists.
```

#### Constraints:
- `The number of nodes in each linked list is in the range [1, 100].`
- `0 <= Node.val <= 9`
- `It is guaranteed that the list represents a number that does not have leading zeros.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Column addition taught in elementary school: add the ones column, write down `val % 10`, carry over `val // 10` to the tens column, and repeat.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a `dummy = ListNode()` and maintain a `carry = 0` variable.
- Hint 2: Loop while `l1` or `l2` or `carry` is non-zero.
- Hint 3: Sum `val = (l1.val if l1 else 0) + (l2.val if l2 else 0) + carry`, compute new `carry = val // 10`, and append `ListNode(val % 10)`.

### 4. Detailed Approach Walkthrough
1. Initialize `dummy = ListNode()`, `curr = dummy`, `carry = 0`.
2. While `l1` or `l2` or `carry`:
   - `v1 = l1.val if l1 else 0`
   - `v2 = l2.val if l2 else 0`
   - `val = v1 + v2 + carry`
   - `carry = val // 10`
   - `val = val % 10`
   - `curr.next = ListNode(val)`
   - `curr = curr.next`
   - `l1 = l1.next if l1 else None`
   - `l2 = l2.next if l2 else None`
3. Return `dummy.next`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        curr = dummy
        carry = 0
        
        while l1 or l2 or carry:
            v1 = l1.val if l1 else 0
            v2 = l2.val if l2 else 0
            
            val = v1 + v2 + carry
            carry = val // 10
            val = val % 10
            curr.next = ListNode(val)
            
            curr = curr.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
            
        return dummy.next
```

### 6. Complexity Analysis
- **Time Complexity:** `O(max(n, m)) - Where n and m are lengths of l1 and l2.`
- **Space Complexity:** `O(max(n, m)) - Length of the newly generated answer linked list.`

---

## <a id="41-linked-list-cycle"></a>41. Linked List Cycle

- **Difficulty:** `Easy`
- **Pattern:** `Floyd's Tortoise and Hare`
- **LeetCode Reference:** [LeetCode #141](https://leetcode.com/problems/linked-list-cycle/)

### 1. Problem Statement
Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

Return `true` if there is some cycle in the linked list. Otherwise, return `false`.

#### Examples:
**Example 1:**
```text
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

**Example 2:**
```text
Input: head = [1], pos = -1
Output: false
Explanation: Single node with no cycle.
```

#### Constraints:
- `The number of the nodes in the list is in the range [0, 10^4].`
- `-10^5 <= Node.val <= 10^5`
- `pos is -1 or a valid index in the linked-list.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine two runners on a running track: a fast runner moving 2 steps per second and a slow runner moving 1 step per second. If the track is a straight open road, the fast runner reaches the end and stops. If the track is a closed circular loop, the fast runner is guaranteed to lap and collide with the slow runner.

### 3. Step-by-Step Progressive Hints
- Hint 1: A hash set of visited nodes solves this in O(n) space.
- Hint 2: To solve in O(1) space, use Floyd's Tortoise and Hare algorithm.
- Hint 3: Advance `slow = slow.next` and `fast = fast.next.next`. If `slow == fast`, return True. If `fast` or `fast.next` is None, return False.

### 4. Detailed Approach Walkthrough
1. Initialize `slow = head` and `fast = head`.
2. While `fast` and `fast.next`:
   - `slow = slow.next`
   - `fast = fast.next.next`
   - If `slow == fast`: return `True`
3. If loop ends, return `False`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
                
        return False
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Fast pointer travels at most 2n steps.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="42-find-the-duplicate-number"></a>42. Find the Duplicate Number

- **Difficulty:** `Medium`
- **Pattern:** `Floyd's Cycle Detection (Array as Linked List)`
- **LeetCode Reference:** [LeetCode #287](https://leetcode.com/problems/find-the-duplicate-number/)

### 1. Problem Statement
Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return this repeated number.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

#### Examples:
**Example 1:**
```text
Input: nums = [1,3,4,2,2]
Output: 2
Explanation: 2 is repeated.
```

**Example 2:**
```text
Input: nums = [3,1,3,4,2]
Output: 3
Explanation: 3 is repeated.
```

#### Constraints:
- `1 <= n <= 10^5`
- `nums.length == n + 1`
- `1 <= nums[i] <= n`
- `All the integers in nums appear only once except for precisely one integer which appears two or more times.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Treat the array as a linked list where each index `i` points to `nums[i]`. Because numbers are `1..n` and array size is `n+1`, index 0 is guaranteed to enter a cycle, and the entry point of the cycle is the duplicate value having multiple incoming pointers.

### 3. Step-by-Step Progressive Hints
- Hint 1: Treat `nums[i]` as the `next` pointer of node `i`.
- Hint 2: Find the intersection point of `slow` and `fast` pointers.
- Hint 3: Once they meet, initialize `slow2 = 0`. Advance `slow` and `slow2` one step at a time until they meet. Their meeting point is the entry of the cycle (the duplicate number).

### 4. Detailed Approach Walkthrough
1. Phase 1: Initialize `slow = 0, fast = 0`.
   - While True:
     - `slow = nums[slow]`
     - `fast = nums[nums[fast]]`
     - If `slow == fast`: break
2. Phase 2: Initialize `slow2 = 0`.
   - While True:
     - `slow = nums[slow]`
     - `slow2 = nums[slow2]`
     - If `slow == slow2`: return `slow`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findDuplicate(self, nums: list[int]) -> int:
        slow, fast = 0, 0
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break
                
        slow2 = 0
        while True:
            slow = nums[slow]
            slow2 = nums[slow2]
            if slow == slow2:
                return slow
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Linear cycle traversal.`
- **Space Complexity:** `O(1) - Constant auxiliary pointers without mutating the input array.`

---

## <a id="43-lru-cache"></a>43. LRU Cache

- **Difficulty:** `Medium`
- **Pattern:** `Hash Map + Doubly Linked List`
- **LeetCode Reference:** [LeetCode #146](https://leetcode.com/problems/lru-cache/)

### 1. Problem Statement
Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache**.

Implement the `LRUCache` class:
- `LRUCache(int capacity)` Initialize the LRU cache with positive size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

#### Examples:
**Example 1:**
```text
Input: ["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output: [null, null, null, 1, null, -1, null, -1, 3, 4]
Explanation: LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

#### Constraints:
- `1 <= capacity <= 3000`
- `0 <= key <= 10^4`
- `0 <= value <= 10^5`
- `At most 2 * 10^5 calls will be made to get and put.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a bookshelf with fixed slots. Whenever you read or insert a book, you place it at the far right of the shelf (Most Recently Used). When the shelf is full and a new book arrives, the book sitting neglected at the far left (Least Recently Used) is evicted to make room.

### 3. Step-by-Step Progressive Hints
- Hint 1: A Hash Map provides O(1) lookup, but does not track usage order.
- Hint 2: A Doubly Linked List allows O(1) node removal and insertion anywhere.
- Hint 3: Combine both: Hash Map maps `key -> ListNode(key, val)`. Maintain dummy nodes `left` (LRU) and `right` (MRU). Whenever a node is accessed or updated, remove it from the list and re-insert it right before `right`.

### 4. Detailed Approach Walkthrough
1. Define `Node(key, val, prev, next)`.
2. In `LRUCache`, create dummy nodes `self.left` (LRU) and `self.right` (MRU) connected to each other, and `self.cache = {}`.
3. Helper `remove(node)`: connects `node.prev.next = node.next` and `node.next.prev = node.prev`.
4. Helper `insert(node)`: inserts `node` immediately before `self.right`.
5. `get(key)`: If `key` in `cache`, `remove(node)`, `insert(node)`, return `node.val`. Else return `-1`.
6. `put(key, value)`: If `key` in `cache`, `remove(cache[key])`. Create `node = Node(key, value)`, `cache[key] = node`, `insert(node)`. If `len(cache) > capacity`, evict `lru = self.left.next`, `remove(lru)`, `del cache[lru.key]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Node:
    def __init__(self, key, val):
        self.key, self.val = key, val
        self.prev = self.next = None

class LRUCache:
    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {}  # key -> node
        
        # Left = LRU, Right = Most Recently Used
        self.left, self.right = Node(0, 0), Node(0, 0)
        self.left.next, self.right.prev = self.right, self.left
        
    def remove(self, node):
        prev, nxt = node.prev, node.next
        prev.next, nxt.prev = nxt, prev
        
    def insert(self, node):
        prev, nxt = self.right.prev, self.right
        prev.next = nxt.prev = node
        node.prev, node.next = prev, nxt
        
    def get(self, key: int) -> int:
        if key in self.cache:
            self.remove(self.cache[key])
            self.insert(self.cache[key])
            return self.cache[key].val
        return -1

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.remove(self.cache[key])
        self.cache[key] = Node(key, value)
        self.insert(self.cache[key])
        
        if len(self.cache) > self.cap:
            # Remove and delete LRU from hashmap
            lru = self.left.next
            self.remove(lru)
            del self.cache[lru.key]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(1) for both get and put operations.`
- **Space Complexity:** `O(capacity) - To store nodes in the hash map and doubly linked list.`

---

## <a id="44-merge-k-sorted-lists"></a>44. Merge K Sorted Lists

- **Difficulty:** `Hard`
- **Pattern:** `Divide and Conquer (Merge Sort Lists)`
- **LeetCode Reference:** [LeetCode #23](https://leetcode.com/problems/merge-k-sorted-lists/)

### 1. Problem Statement
You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

#### Examples:
**Example 1:**
```text
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: All 3 sorted lists merged into one single sorted list.
```

**Example 2:**
```text
Input: lists = []
Output: []
Explanation: Empty list input returns empty list.
```

#### Constraints:
- `k == lists.length`
- `0 <= k <= 10^4`
- `0 <= lists[i].length <= 500`
- `-10^4 <= lists[i][j] <= 10^4`
- `lists[i] is sorted in ascending order.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Tournament bracket style: instead of merging 100 teams one-by-one sequentially (which takes O(k * N)), pair them up in rounds: 100 -> 50 -> 25 -> 12 -> 6 -> 3 -> 2 -> 1 champion list in just O(log k) rounds.

### 3. Step-by-Step Progressive Hints
- Hint 1: Iteratively merging one list into an accumulator takes O(k * N).
- Hint 2: We can merge pairs of lists using Divide and Conquer, taking O(N log k) total time.
- Hint 3: In each round, take pairs `lists[i]` and `lists[i+1]`, merge them using `mergeTwoLists`, and replace `lists` with the merged list until only 1 remains.

### 4. Detailed Approach Walkthrough
1. If `not lists` or `len(lists) == 0`, return `None`.
2. While `len(lists) > 1`:
   - Initialize `mergedLists = []`.
   - Iterate `i` from 0 to `len(lists)` with step 2:
     - `l1 = lists[i]`
     - `l2 = lists[i + 1] if (i + 1) < len(lists) else None`
     - `mergedLists.append(self.mergeTwoLists(l1, l2))`
   - Update `lists = mergedLists`.
3. Return `lists[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def mergeKLists(self, lists: list[Optional[ListNode]]) -> Optional[ListNode]:
        if not lists or len(lists) == 0:
            return None
            
        while len(lists) > 1:
            mergedLists = []
            for i in range(0, len(lists), 2):
                l1 = lists[i]
                l2 = lists[i + 1] if (i + 1) < len(lists) else None
                mergedLists.append(self.mergeTwoLists(l1, l2))
            lists = mergedLists
        return lists[0]
        
    def mergeTwoLists(self, l1, l2):
        dummy = ListNode()
        tail = dummy
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        tail.next = l1 or l2
        return dummy.next
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N log k) - Where N is total number of nodes across all k lists, and log k is the number of merge levels.`
- **Space Complexity:** `O(1) - Merging is done in-place by updating pointers.`

---

## <a id="45-reverse-nodes-in-k-group"></a>45. Reverse Nodes in k-Group

- **Difficulty:** `Hard`
- **Pattern:** `Segment Pointer Manipulation`
- **LeetCode Reference:** [LeetCode #25](https://leetcode.com/problems/reverse-nodes-in-k-group/)

### 1. Problem Statement
Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return the modified list.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

#### Examples:
**Example 1:**
```text
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
Explanation: Nodes 1-2 reversed, nodes 3-4 reversed, node 5 remains as-is.
```

**Example 2:**
```text
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
Explanation: Nodes 1-2-3 reversed, nodes 4-5 remain unchanged.
```

#### Constraints:
- `The number of nodes in the list is n.`
- `1 <= k <= n <= 5000`
- `0 <= Node.val <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a train made of cars. You inspect the next `k` train cars ahead. If there are at least `k` cars, you detach that segment, reverse their couplings, reconnect them to the train, and advance forward to the next `k` cars.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a dummy node pointing to `head` and maintain `groupPrev` pointing to the node preceding the current k-group.
- Hint 2: Write a helper `getKth(curr, k)` to verify if `k` nodes exist ahead. If `kth` is `None`, break.
- Hint 3: Reverse the `k` nodes between `groupPrev.next` and `kth.next`, reconnect pointers, and advance `groupPrev`.

### 4. Detailed Approach Walkthrough
1. Initialize `dummy = ListNode(0, head)`, `groupPrev = dummy`.
2. While True:
   - `kth = self.getKth(groupPrev, k)`
   - If not `kth`: break (fewer than k nodes remain)
   - `groupNext = kth.next`
   - Reverse group: `prev = kth.next`, `curr = groupPrev.next`
   - While `curr != groupNext`:
     - `nxt = curr.next`
     - `curr.next = prev`
     - `prev = curr`
     - `curr = nxt`
   - Reconnect: `tmp = groupPrev.next`, `groupPrev.next = kth`, `groupPrev = tmp`
3. Return `dummy.next`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        groupPrev = dummy
        
        while True:
            kth = self.getKth(groupPrev, k)
            if not kth:
                break
            groupNext = kth.next
            
            # Reverse group
            prev, curr = kth.next, groupPrev.next
            while curr != groupNext:
                nxt = curr.next
                curr.next = prev
                prev = curr
                curr = nxt
                
            tmp = groupPrev.next
            groupPrev.next = kth
            groupPrev = tmp
            
        return dummy.next
        
    def getKth(self, curr, k):
        while curr and k > 0:
            curr = curr.next
            k -= 1
        return curr
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Every node is visited twice (once to find kth, once to reverse).`
- **Space Complexity:** `O(1) - Constant auxiliary memory in-place.`

---
