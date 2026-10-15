# 🚀 NeetCode 150 Master Study Guide & Curriculum

> A comprehensive, production-grade guide covering all **150 coding interview problems** from the NeetCode Roadmap with standard problem statements, real-world intuitive analogies, progressive hints, line-by-line algorithm walkthroughs, canonical NeetCode Python 3 solutions, and formal Big-O complexity analyses.

## 📚 Master Table of Contents (18 Topics)

| Topic # | Chapter Title | Problems | Core Pattern Focus | Markdown Link |
|---|---|---|---|---|
| 01 | **Arrays & Hashing** | 9 Problems | Hash Set | [View Chapter](chapters/01_arrays_and_hashing.md) |
| 02 | **Two Pointers** | 5 Problems | Converging Pointers | [View Chapter](chapters/02_two_pointers.md) |
| 03 | **Sliding Window** | 6 Problems | Sliding Window / Two Pointers | [View Chapter](chapters/03_sliding_window.md) |
| 04 | **Stack** | 7 Problems | LIFO Matching | [View Chapter](chapters/04_stack.md) |
| 05 | **Binary Search** | 7 Problems | Standard Binary Search | [View Chapter](chapters/05_binary_search.md) |
| 06 | **Linked List** | 11 Problems | Iterative Pointer Reversal | [View Chapter](chapters/06_linked_list.md) |
| 07 | **Trees** | 15 Problems | Recursive DFS (Postorder / Preorder) | [View Chapter](chapters/07_trees.md) |
| 08 | **Tries** | 3 Problems | Prefix Tree Node Implementation | [View Chapter](chapters/08_tries.md) |
| 09 | **Heap / Priority Queue** | 7 Problems | Min-Heap of Size K | [View Chapter](chapters/09_heap_priority_queue.md) |
| 10 | **Backtracking** | 9 Problems | Include / Exclude Decision Tree | [View Chapter](chapters/10_backtracking.md) |
| 11 | **Graphs** | 13 Problems | Connected Components BFS / DFS | [View Chapter](chapters/11_graphs.md) |
| 12 | **Advanced Graphs** | 6 Problems | Eulerian Path (Hierholzer's Algorithm) | [View Chapter](chapters/12_advanced_graphs.md) |
| 13 | **1-D Dynamic Programming** | 12 Problems | Fibonacci DP (Two Variables) | [View Chapter](chapters/13_1d_dynamic_programming.md) |
| 14 | **2-D Dynamic Programming** | 11 Problems | 2D Grid DP / Combinatorics | [View Chapter](chapters/14_2d_dynamic_programming.md) |
| 15 | **Greedy** | 8 Problems | Kadane's Algorithm | [View Chapter](chapters/15_greedy.md) |
| 16 | **Intervals** | 6 Problems | Linear Insertion & Overlap Merging | [View Chapter](chapters/16_intervals.md) |
| 17 | **Math & Geometry** | 8 Problems | Layer-by-Layer 4-Way In-Place Rotation | [View Chapter](chapters/17_math_and_geometry.md) |
| 18 | **Bit Manipulation** | 7 Problems | XOR Parity Cancellation | [View Chapter](chapters/18_bit_manipulation.md) |

---

## 🗺️ Visual NeetCode 150 Dependency Roadmap

```text
Arrays & Hashing (9)
 ├──> Two Pointers (5) ───> Sliding Window (6)
 ├──> Stack (7)
 ├──> Binary Search (7)
 └──> Linked List (11)
       ├──> Trees (15) ───> Tries (3)
       │     ├──> Heap / Priority Queue (7)
       │     ├──> Backtracking (9)
       │     └──> Graphs (13) ───> Advanced Graphs (6)
       └──> 1-D DP (12) ───> 2-D DP (11)
             ├──> Greedy (8) ───> Intervals (6)
             └──> Math & Geometry (8) / Bit Manipulation (7)
```

---

## 📑 Complete 150 Problems Master Index

| # | Problem Name | Topic | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|---|
| 1 | [Contains Duplicate](chapters/01_arrays_and_hashing.md#1-contains-duplicate) | Arrays & Hashing | `Easy` | `Hash Set` | [#217](https://leetcode.com/problems/contains-duplicate/) |
| 2 | [Valid Anagram](chapters/01_arrays_and_hashing.md#2-valid-anagram) | Arrays & Hashing | `Easy` | `Frequency Counter / Hash Map` | [#242](https://leetcode.com/problems/valid-anagram/) |
| 3 | [Two Sum](chapters/01_arrays_and_hashing.md#3-two-sum) | Arrays & Hashing | `Easy` | `Hash Map (Complement Search)` | [#1](https://leetcode.com/problems/two-sum/) |
| 4 | [Group Anagrams](chapters/01_arrays_and_hashing.md#4-group-anagrams) | Arrays & Hashing | `Medium` | `Hash Map Categorization` | [#49](https://leetcode.com/problems/group-anagrams/) |
| 5 | [Top K Frequent Elements](chapters/01_arrays_and_hashing.md#5-top-k-frequent-elements) | Arrays & Hashing | `Medium` | `Bucket Sort / Min-Heap` | [#347](https://leetcode.com/problems/top-k-frequent-elements/) |
| 6 | [Product of Array Except Self](chapters/01_arrays_and_hashing.md#6-product-of-array-except-self) | Arrays & Hashing | `Medium` | `Prefix and Postfix Products` | [#238](https://leetcode.com/problems/product-of-array-except-self/) |
| 7 | [Valid Sudoku](chapters/01_arrays_and_hashing.md#7-valid-sudoku) | Arrays & Hashing | `Medium` | `Matrix Hashing / Set Validation` | [#36](https://leetcode.com/problems/valid-sudoku/) |
| 8 | [Encode and Decode Strings](chapters/01_arrays_and_hashing.md#8-encode-and-decode-strings) | Arrays & Hashing | `Medium` | `String Serialization (Length-Delimited)` | [#271](https://neetcode.io/problems/string-encode-and-decode) |
| 9 | [Longest Consecutive Sequence](chapters/01_arrays_and_hashing.md#9-longest-consecutive-sequence) | Arrays & Hashing | `Medium` | `Hash Set (Sequence Start Detection)` | [#128](https://leetcode.com/problems/longest-consecutive-sequence/) |
| 10 | [Valid Palindrome](chapters/02_two_pointers.md#10-valid-palindrome) | Two Pointers | `Easy` | `Converging Pointers` | [#125](https://leetcode.com/problems/valid-palindrome/) |
| 11 | [Two Sum II Input Array Is Sorted](chapters/02_two_pointers.md#11-two-sum-ii-input-array-is-sorted) | Two Pointers | `Medium` | `Two Pointers (Sorted Array)` | [#167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) |
| 12 | [3Sum](chapters/02_two_pointers.md#12-3sum) | Two Pointers | `Medium` | `Sort + Two Pointers` | [#15](https://leetcode.com/problems/3sum/) |
| 13 | [Container With Most Water](chapters/02_two_pointers.md#13-container-with-most-water) | Two Pointers | `Medium` | `Greedy Two Pointers` | [#11](https://leetcode.com/problems/container-with-most-water/) |
| 14 | [Trapping Rain Water](chapters/02_two_pointers.md#14-trapping-rain-water) | Two Pointers | `Hard` | `Two Pointers (Min of Max Heights)` | [#42](https://leetcode.com/problems/trapping-rain-water/) |
| 15 | [Best Time to Buy and Sell Stock](chapters/03_sliding_window.md#15-best-time-to-buy-and-sell-stock) | Sliding Window | `Easy` | `Sliding Window / Two Pointers` | [#121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) |
| 16 | [Longest Substring Without Repeating Characters](chapters/03_sliding_window.md#16-longest-substring-without-repeating-characters) | Sliding Window | `Medium` | `Dynamic Sliding Window + Set` | [#3](https://leetcode.com/problems/longest-substring-without-repeating-characters/) |
| 17 | [Longest Repeating Character Replacement](chapters/03_sliding_window.md#17-longest-repeating-character-replacement) | Sliding Window | `Medium` | `Sliding Window + Frequency Tracking` | [#424](https://leetcode.com/problems/longest-repeating-character-replacement/) |
| 18 | [Permutation in String](chapters/03_sliding_window.md#18-permutation-in-string) | Sliding Window | `Medium` | `Fixed-Size Sliding Window + Match Counter` | [#567](https://leetcode.com/problems/permutation-in-string/) |
| 19 | [Minimum Window Substring](chapters/03_sliding_window.md#19-minimum-window-substring) | Sliding Window | `Hard` | `Dynamic Sliding Window + Condition Met` | [#76](https://leetcode.com/problems/minimum-window-substring/) |
| 20 | [Sliding Window Maximum](chapters/03_sliding_window.md#20-sliding-window-maximum) | Sliding Window | `Hard` | `Monotonic Decreasing Deque` | [#239](https://leetcode.com/problems/sliding-window-maximum/) |
| 21 | [Valid Parentheses](chapters/04_stack.md#21-valid-parentheses) | Stack | `Easy` | `LIFO Matching` | [#20](https://leetcode.com/problems/valid-parentheses/) |
| 22 | [Min Stack](chapters/04_stack.md#22-min-stack) | Stack | `Medium` | `Auxiliary Min Tracker` | [#155](https://leetcode.com/problems/min-stack/) |
| 23 | [Evaluate Reverse Polish Notation](chapters/04_stack.md#23-evaluate-reverse-polish-notation) | Stack | `Medium` | `Postfix Expression Evaluation` | [#150](https://leetcode.com/problems/evaluate-reverse-polish-notation/) |
| 24 | [Generate Parentheses](chapters/04_stack.md#24-generate-parentheses) | Stack | `Medium` | `Backtracking with Stack / State` | [#22](https://leetcode.com/problems/generate-parentheses/) |
| 25 | [Daily Temperatures](chapters/04_stack.md#25-daily-temperatures) | Stack | `Medium` | `Monotonic Decreasing Stack` | [#739](https://leetcode.com/problems/daily-temperatures/) |
| 26 | [Car Fleet](chapters/04_stack.md#26-car-fleet) | Stack | `Medium` | `Monotonic Stack / Sort by Position` | [#853](https://leetcode.com/problems/car-fleet/) |
| 27 | [Largest Rectangle in Histogram](chapters/04_stack.md#27-largest-rectangle-in-histogram) | Stack | `Hard` | `Monotonic Increasing Stack` | [#84](https://leetcode.com/problems/largest-rectangle-in-histogram/) |
| 28 | [Binary Search](chapters/05_binary_search.md#28-binary-search) | Binary Search | `Easy` | `Standard Binary Search` | [#704](https://leetcode.com/problems/binary-search/) |
| 29 | [Search a 2D Matrix](chapters/05_binary_search.md#29-search-a-2d-matrix) | Binary Search | `Medium` | `2D Binary Search / Row-Column Elimination` | [#74](https://leetcode.com/problems/search-a-2d-matrix/) |
| 30 | [Koko Eating Bananas](chapters/05_binary_search.md#30-koko-eating-bananas) | Binary Search | `Medium` | `Binary Search on Solution Space` | [#875](https://leetcode.com/problems/koko-eating-bananas/) |
| 31 | [Find Minimum in Rotated Sorted Array](chapters/05_binary_search.md#31-find-minimum-in-rotated-sorted-array) | Binary Search | `Medium` | `Rotated Binary Search (Pivot Finding)` | [#153](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) |
| 32 | [Search in Rotated Sorted Array](chapters/05_binary_search.md#32-search-in-rotated-sorted-array) | Binary Search | `Medium` | `Rotated Binary Search (Half Selection)` | [#33](https://leetcode.com/problems/search-in-rotated-sorted-array/) |
| 33 | [Time Based Key-Value Store](chapters/05_binary_search.md#33-time-based-key-value-store) | Binary Search | `Medium` | `Binary Search on Timestamps` | [#981](https://leetcode.com/problems/time-based-key-value-store/) |
| 34 | [Median of Two Sorted Arrays](chapters/05_binary_search.md#34-median-of-two-sorted-arrays) | Binary Search | `Hard` | `Binary Search (Array Partitioning)` | [#4](https://leetcode.com/problems/median-of-two-sorted-arrays/) |
| 35 | [Reverse Linked List](chapters/06_linked_list.md#35-reverse-linked-list) | Linked List | `Easy` | `Iterative Pointer Reversal` | [#206](https://leetcode.com/problems/reverse-linked-list/) |
| 36 | [Merge Two Sorted Lists](chapters/06_linked_list.md#36-merge-two-sorted-lists) | Linked List | `Easy` | `Dummy Sentinel Head + Two Pointers` | [#21](https://leetcode.com/problems/merge-two-sorted-lists/) |
| 37 | [Reorder List](chapters/06_linked_list.md#37-reorder-list) | Linked List | `Medium` | `Fast & Slow + Reverse + Interleave` | [#143](https://leetcode.com/problems/reorder-list/) |
| 38 | [Remove Nth Node From End of List](chapters/06_linked_list.md#38-remove-nth-node-from-end-of-list) | Linked List | `Medium` | `Two Pointers with Offset` | [#19](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) |
| 39 | [Copy List with Random Pointer](chapters/06_linked_list.md#39-copy-list-with-random-pointer) | Linked List | `Medium` | `Hash Map Node Mapping / Interleaving` | [#138](https://leetcode.com/problems/copy-list-with-random-pointer/) |
| 40 | [Add Two Numbers](chapters/06_linked_list.md#40-add-two-numbers) | Linked List | `Medium` | `Elementary Math / Carry Simulation` | [#2](https://leetcode.com/problems/add-two-numbers/) |
| 41 | [Linked List Cycle](chapters/06_linked_list.md#41-linked-list-cycle) | Linked List | `Easy` | `Floyd's Tortoise and Hare` | [#141](https://leetcode.com/problems/linked-list-cycle/) |
| 42 | [Find the Duplicate Number](chapters/06_linked_list.md#42-find-the-duplicate-number) | Linked List | `Medium` | `Floyd's Cycle Detection (Array as Linked List)` | [#287](https://leetcode.com/problems/find-the-duplicate-number/) |
| 43 | [LRU Cache](chapters/06_linked_list.md#43-lru-cache) | Linked List | `Medium` | `Hash Map + Doubly Linked List` | [#146](https://leetcode.com/problems/lru-cache/) |
| 44 | [Merge K Sorted Lists](chapters/06_linked_list.md#44-merge-k-sorted-lists) | Linked List | `Hard` | `Divide and Conquer (Merge Sort Lists)` | [#23](https://leetcode.com/problems/merge-k-sorted-lists/) |
| 45 | [Reverse Nodes in k-Group](chapters/06_linked_list.md#45-reverse-nodes-in-k-group) | Linked List | `Hard` | `Segment Pointer Manipulation` | [#25](https://leetcode.com/problems/reverse-nodes-in-k-group/) |
| 46 | [Invert Binary Tree](chapters/07_trees.md#46-invert-binary-tree) | Trees | `Easy` | `Recursive DFS (Postorder / Preorder)` | [#226](https://leetcode.com/problems/invert-binary-tree/) |
| 47 | [Maximum Depth of Binary Tree](chapters/07_trees.md#47-maximum-depth-of-binary-tree) | Trees | `Easy` | `Recursive DFS / BFS` | [#104](https://leetcode.com/problems/maximum-depth-of-binary-tree/) |
| 48 | [Diameter of Binary Tree](chapters/07_trees.md#48-diameter-of-binary-tree) | Trees | `Easy` | `Bottom-Up DFS (Postorder)` | [#543](https://leetcode.com/problems/diameter-of-binary-tree/) |
| 49 | [Balanced Binary Tree](chapters/07_trees.md#49-balanced-binary-tree) | Trees | `Easy` | `Bottom-Up DFS with Early Exit` | [#110](https://leetcode.com/problems/balanced-binary-tree/) |
| 50 | [Same Tree](chapters/07_trees.md#50-same-tree) | Trees | `Easy` | `Recursive Tree Matching` | [#100](https://leetcode.com/problems/same-tree/) |
| 51 | [Subtree of Another Tree](chapters/07_trees.md#51-subtree-of-another-tree) | Trees | `Easy` | `Tree Matching DFS` | [#572](https://leetcode.com/problems/subtree-of-another-tree/) |
| 52 | [Lowest Common Ancestor of a BST](chapters/07_trees.md#52-lowest-common-ancestor-of-a-bst) | Trees | `Medium` | `BST Property Traversal` | [#235](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) |
| 53 | [Binary Tree Level Order Traversal](chapters/07_trees.md#53-binary-tree-level-order-traversal) | Trees | `Medium` | `BFS Queue Traversal` | [#102](https://leetcode.com/problems/binary-tree-level-order-traversal/) |
| 54 | [Binary Tree Right Side View](chapters/07_trees.md#54-binary-tree-right-side-view) | Trees | `Medium` | `BFS Level Last Element / DFS Right-First` | [#199](https://leetcode.com/problems/binary-tree-right-side-view/) |
| 55 | [Count Good Nodes in Binary Tree](chapters/07_trees.md#55-count-good-nodes-in-binary-tree) | Trees | `Medium` | `DFS with Running Max Path Value` | [#1448](https://leetcode.com/problems/count-good-nodes-in-binary-tree/) |
| 56 | [Validate Binary Search Tree](chapters/07_trees.md#56-validate-binary-search-tree) | Trees | `Medium` | `DFS Valid Range Propagation` | [#98](https://leetcode.com/problems/validate-binary-search-tree/) |
| 57 | [Kth Smallest Element in a BST](chapters/07_trees.md#57-kth-smallest-element-in-a-bst) | Trees | `Medium` | `Inorder Traversal (Sorted Order)` | [#230](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) |
| 58 | [Construct Binary Tree from Preorder and Inorder Traversal](chapters/07_trees.md#58-construct-binary-tree-from-preorder-and-inorder-traversal) | Trees | `Medium` | `Divide and Conquer Tree Reconstruction` | [#105](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) |
| 59 | [Binary Tree Maximum Path Sum](chapters/07_trees.md#59-binary-tree-maximum-path-sum) | Trees | `Hard` | `Bottom-Up DFS with Split Max` | [#124](https://leetcode.com/problems/binary-tree-maximum-path-sum/) |
| 60 | [Serialize and Deserialize Binary Tree](chapters/07_trees.md#60-serialize-and-deserialize-binary-tree) | Trees | `Hard` | `Preorder DFS Serialization` | [#297](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) |
| 61 | [Implement Trie (Prefix Tree)](chapters/08_tries.md#61-implement-trie-prefix-tree) | Tries | `Medium` | `Prefix Tree Node Implementation` | [#208](https://leetcode.com/problems/implement-trie-prefix-tree/) |
| 62 | [Design Add and Search Words Data Structure](chapters/08_tries.md#62-design-add-and-search-words-data-structure) | Tries | `Medium` | `Trie DFS with Wildcard Matching` | [#211](https://leetcode.com/problems/design-add-and-search-words-data-structure/) |
| 63 | [Word Search II](chapters/08_tries.md#63-word-search-ii) | Tries | `Hard` | `Trie + 2D Backtracking DFS` | [#212](https://leetcode.com/problems/word-search-ii/) |
| 64 | [Kth Largest Element in a Stream](chapters/09_heap_priority_queue.md#64-kth-largest-element-in-a-stream) | Heap / Priority Queue | `Easy` | `Min-Heap of Size K` | [#703](https://leetcode.com/problems/kth-largest-element-in-a-stream/) |
| 65 | [Last Stone Weight](chapters/09_heap_priority_queue.md#65-last-stone-weight) | Heap / Priority Queue | `Easy` | `Max-Heap Simulation` | [#1046](https://leetcode.com/problems/last-stone-weight/) |
| 66 | [K Closest Points to Origin](chapters/09_heap_priority_queue.md#66-k-closest-points-to-origin) | Heap / Priority Queue | `Medium` | `Min-Heap / Max-Heap of Size K` | [#973](https://leetcode.com/problems/k-closest-points-to-origin/) |
| 67 | [Kth Largest Element in an Array](chapters/09_heap_priority_queue.md#67-kth-largest-element-in-an-array) | Heap / Priority Queue | `Medium` | `QuickSelect / Min-Heap` | [#215](https://leetcode.com/problems/kth-largest-element-in-an-array/) |
| 68 | [Task Scheduler](chapters/09_heap_priority_queue.md#68-task-scheduler) | Heap / Priority Queue | `Medium` | `Max-Heap + Cooldown Queue / Math Greedy` | [#621](https://leetcode.com/problems/task-scheduler/) |
| 69 | [Design Twitter](chapters/09_heap_priority_queue.md#69-design-twitter) | Heap / Priority Queue | `Medium` | `Max-Heap + Hash Map (K-Way Merge)` | [#355](https://leetcode.com/problems/design-twitter/) |
| 70 | [Find Median from Data Stream](chapters/09_heap_priority_queue.md#70-find-median-from-data-stream) | Heap / Priority Queue | `Hard` | `Two Heaps (Small Max-Heap & Large Min-Heap)` | [#295](https://leetcode.com/problems/find-median-from-data-stream/) |
| 71 | [Subsets](chapters/10_backtracking.md#71-subsets) | Backtracking | `Medium` | `Include / Exclude Decision Tree` | [#78](https://leetcode.com/problems/subsets/) |
| 72 | [Combination Sum](chapters/10_backtracking.md#72-combination-sum) | Backtracking | `Medium` | `Unbounded Knapsack Backtracking` | [#39](https://leetcode.com/problems/combination-sum/) |
| 73 | [Permutations](chapters/10_backtracking.md#73-permutations) | Backtracking | `Medium` | `Recursive Element Insertion / Swapping` | [#46](https://leetcode.com/problems/permutations/) |
| 74 | [Subsets II](chapters/10_backtracking.md#74-subsets-ii) | Backtracking | `Medium` | `Backtracking with Duplicate Skipping` | [#90](https://leetcode.com/problems/subsets-ii/) |
| 75 | [Combination Sum II](chapters/10_backtracking.md#75-combination-sum-ii) | Backtracking | `Medium` | `Sorted Backtracking with Duplicate Pruning` | [#40](https://leetcode.com/problems/combination-sum-ii/) |
| 76 | [Word Search](chapters/10_backtracking.md#76-word-search) | Backtracking | `Medium` | `2D Grid Backtracking DFS` | [#79](https://leetcode.com/problems/word-search/) |
| 77 | [Palindrome Partitioning](chapters/10_backtracking.md#77-palindrome-partitioning) | Backtracking | `Medium` | `Backtracking Partition Search` | [#131](https://leetcode.com/problems/palindrome-partitioning/) |
| 78 | [Letter Combinations of a Phone Number](chapters/10_backtracking.md#78-letter-combinations-of-a-phone-number) | Backtracking | `Medium` | `Combinatorial Backtracking` | [#17](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) |
| 79 | [N-Queens](chapters/10_backtracking.md#79-n-queens) | Backtracking | `Hard` | `Row-by-Row Constraint Propagation` | [#51](https://leetcode.com/problems/n-queens/) |
| 80 | [Number of Islands](chapters/11_graphs.md#80-number-of-islands) | Graphs | `Medium` | `Connected Components BFS / DFS` | [#200](https://leetcode.com/problems/number-of-islands/) |
| 81 | [Clone Graph](chapters/11_graphs.md#81-clone-graph) | Graphs | `Medium` | `DFS Node Hash Map Cloning` | [#133](https://leetcode.com/problems/clone-graph/) |
| 82 | [Max Area of Island](chapters/11_graphs.md#82-max-area-of-island) | Graphs | `Medium` | `Grid DFS Flood Fill Counting` | [#695](https://leetcode.com/problems/max-area-of-island/) |
| 83 | [Pacific Atlantic Water Flow](chapters/11_graphs.md#83-pacific-atlantic-water-flow) | Graphs | `Medium` | `Reverse DFS from Ocean Borders` | [#417](https://leetcode.com/problems/pacific-atlantic-water-flow/) |
| 84 | [Surrounded Regions](chapters/11_graphs.md#84-surrounded-regions) | Graphs | `Medium` | `Border Flood Fill / Un-capture Marking` | [#130](https://leetcode.com/problems/surrounded-regions/) |
| 85 | [Rotting Oranges](chapters/11_graphs.md#85-rotting-oranges) | Graphs | `Medium` | `Multi-Source BFS` | [#994](https://leetcode.com/problems/rotting-oranges/) |
| 86 | [Walls and Gates (Islands and Treasure)](chapters/11_graphs.md#86-walls-and-gates-islands-and-treasure) | Graphs | `Medium` | `Multi-Source BFS Distance Propagation` | [#286](https://neetcode.io/problems/islands-and-treasure) |
| 87 | [Course Schedule](chapters/11_graphs.md#87-course-schedule) | Graphs | `Medium` | `Topological Sort / Cycle Detection (Kahn's or DFS)` | [#207](https://leetcode.com/problems/course-schedule/) |
| 88 | [Course Schedule II](chapters/11_graphs.md#88-course-schedule-ii) | Graphs | `Medium` | `Topological Sort (Postorder DFS)` | [#210](https://leetcode.com/problems/course-schedule-ii/) |
| 89 | [Redundant Connection](chapters/11_graphs.md#89-redundant-connection) | Graphs | `Medium` | `Union-Find (Disjoint Set Union)` | [#684](https://leetcode.com/problems/redundant-connection/) |
| 90 | [Number of Connected Components in an Undirected Graph](chapters/11_graphs.md#90-number-of-connected-components-in-an-undirected-graph) | Graphs | `Medium` | `Union-Find Component Counting` | [#323](https://neetcode.io/problems/count-connected-components) |
| 91 | [Graph Valid Tree](chapters/11_graphs.md#91-graph-valid-tree) | Graphs | `Medium` | `Tree Invariant (Cycle-Free & Fully Connected)` | [#261](https://neetcode.io/problems/valid-tree) |
| 92 | [Word Ladder](chapters/11_graphs.md#92-word-ladder) | Graphs | `Hard` | `BFS Shortest Path on Generic Patterns` | [#127](https://leetcode.com/problems/word-ladder/) |
| 93 | [Reconstruct Itinerary](chapters/12_advanced_graphs.md#93-reconstruct-itinerary) | Advanced Graphs | `Hard` | `Eulerian Path (Hierholzer's Algorithm)` | [#332](https://leetcode.com/problems/reconstruct-itinerary/) |
| 94 | [Min Cost to Connect All Points](chapters/12_advanced_graphs.md#94-min-cost-to-connect-all-points) | Advanced Graphs | `Medium` | `Minimum Spanning Tree (Prim's Algorithm)` | [#1584](https://leetcode.com/problems/min-cost-to-connect-all-points/) |
| 95 | [Network Delay Time](chapters/12_advanced_graphs.md#95-network-delay-time) | Advanced Graphs | `Medium` | `Dijkstra's Shortest Path` | [#743](https://leetcode.com/problems/network-delay-time/) |
| 96 | [Swim in Rising Water](chapters/12_advanced_graphs.md#96-swim-in-rising-water) | Advanced Graphs | `Hard` | `Modified Dijkstra (Minimax Path)` | [#778](https://leetcode.com/problems/swim-in-rising-water/) |
| 97 | [Alien Dictionary](chapters/12_advanced_graphs.md#97-alien-dictionary) | Advanced Graphs | `Hard` | `Topological Sort on Character Graph` | [#269](https://neetcode.io/problems/foreign-dictionary) |
| 98 | [Cheapest Flights Within K Stops](chapters/12_advanced_graphs.md#98-cheapest-flights-within-k-stops) | Advanced Graphs | `Medium` | `Bellman-Ford / BFS Level Relaxation` | [#787](https://leetcode.com/problems/cheapest-flights-within-k-stops/) |
| 99 | [Climbing Stairs](chapters/13_1d_dynamic_programming.md#99-climbing-stairs) | 1-D Dynamic Programming | `Easy` | `Fibonacci DP (Two Variables)` | [#70](https://leetcode.com/problems/climbing-stairs/) |
| 100 | [Min Cost Climbing Stairs](chapters/13_1d_dynamic_programming.md#100-min-cost-climbing-stairs) | 1-D Dynamic Programming | `Easy` | `Bottom-Up Linear DP` | [#746](https://leetcode.com/problems/min-cost-climbing-stairs/) |
| 101 | [House Robber](chapters/13_1d_dynamic_programming.md#101-house-robber) | 1-D Dynamic Programming | `Medium` | `Include / Exclude Linear DP` | [#198](https://leetcode.com/problems/house-robber/) |
| 102 | [House Robber II](chapters/13_1d_dynamic_programming.md#102-house-robber-ii) | 1-D Dynamic Programming | `Medium` | `Circular Array DP Splitting` | [#213](https://leetcode.com/problems/house-robber-ii/) |
| 103 | [Longest Palindromic Substring](chapters/13_1d_dynamic_programming.md#103-longest-palindromic-substring) | 1-D Dynamic Programming | `Medium` | `Expand Around Center` | [#5](https://leetcode.com/problems/longest-palindromic-substring/) |
| 104 | [Palindromic Substrings](chapters/13_1d_dynamic_programming.md#104-palindromic-substrings) | 1-D Dynamic Programming | `Medium` | `Expand Around Center (Counting)` | [#647](https://leetcode.com/problems/palindromic-substrings/) |
| 105 | [Decode Ways](chapters/13_1d_dynamic_programming.md#105-decode-ways) | 1-D Dynamic Programming | `Medium` | `1-D Dynamic Programming` | [#91](https://leetcode.com/problems/decode-ways/) |
| 106 | [Coin Change](chapters/13_1d_dynamic_programming.md#106-coin-change) | 1-D Dynamic Programming | `Medium` | `Unbounded Knapsack DP (Bottom-Up)` | [#322](https://leetcode.com/problems/coin-change/) |
| 107 | [Maximum Product Subarray](chapters/13_1d_dynamic_programming.md#107-maximum-product-subarray) | 1-D Dynamic Programming | `Medium` | `Min / Max Tracking DP` | [#152](https://leetcode.com/problems/maximum-product-subarray/) |
| 108 | [Word Break](chapters/13_1d_dynamic_programming.md#108-word-break) | 1-D Dynamic Programming | `Medium` | `1-D Substring Matching DP` | [#139](https://leetcode.com/problems/word-break/) |
| 109 | [Longest Increasing Subsequence](chapters/13_1d_dynamic_programming.md#109-longest-increasing-subsequence) | 1-D Dynamic Programming | `Medium` | `1-D DP (O(n^2)) or Patience Sorting Binary Search (O(n log n))` | [#300](https://leetcode.com/problems/longest-increasing-subsequence/) |
| 110 | [Partition Equal Subset Sum](chapters/13_1d_dynamic_programming.md#110-partition-equal-subset-sum) | 1-D Dynamic Programming | `Medium` | `0/1 Knapsack (Subset Sum Target)` | [#416](https://leetcode.com/problems/partition-equal-subset-sum/) |
| 111 | [Unique Paths](chapters/14_2d_dynamic_programming.md#111-unique-paths) | 2-D Dynamic Programming | `Medium` | `2D Grid DP / Combinatorics` | [#62](https://leetcode.com/problems/unique-paths/) |
| 112 | [Longest Common Subsequence](chapters/14_2d_dynamic_programming.md#112-longest-common-subsequence) | 2-D Dynamic Programming | `Medium` | `2D String Alignment Matrix` | [#1143](https://leetcode.com/problems/longest-common-subsequence/) |
| 113 | [Best Time to Buy and Sell Stock with Cooldown](chapters/14_2d_dynamic_programming.md#113-best-time-to-buy-and-sell-stock-with-cooldown) | 2-D Dynamic Programming | `Medium` | `State Machine DP` | [#309](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/) |
| 114 | [Coin Change II](chapters/14_2d_dynamic_programming.md#114-coin-change-ii) | 2-D Dynamic Programming | `Medium` | `Unbounded Knapsack Combinations DP` | [#518](https://leetcode.com/problems/coin-change-ii/) |
| 115 | [Target Sum](chapters/14_2d_dynamic_programming.md#115-target-sum) | 2-D Dynamic Programming | `Medium` | `2D DP / Knapsack Memoization` | [#494](https://leetcode.com/problems/target-sum/) |
| 116 | [Interleaving String](chapters/14_2d_dynamic_programming.md#116-interleaving-string) | 2-D Dynamic Programming | `Medium` | `2D Grid DP` | [#97](https://leetcode.com/problems/interleaving-string/) |
| 117 | [Longest Increasing Path in a Matrix](chapters/14_2d_dynamic_programming.md#117-longest-increasing-path-in-a-matrix) | 2-D Dynamic Programming | `Hard` | `2D Grid DFS with Memoization` | [#329](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/) |
| 118 | [Distinct Subsequences](chapters/14_2d_dynamic_programming.md#118-distinct-subsequences) | 2-D Dynamic Programming | `Hard` | `2D String DP (Matching Counts)` | [#115](https://leetcode.com/problems/distinct-subsequences/) |
| 119 | [Edit Distance](chapters/14_2d_dynamic_programming.md#119-edit-distance) | 2-D Dynamic Programming | `Medium` | `2D Levenshtein Distance Matrix` | [#72](https://leetcode.com/problems/edit-distance/) |
| 120 | [Burst Balloons](chapters/14_2d_dynamic_programming.md#120-burst-balloons) | 2-D Dynamic Programming | `Hard` | `Matrix Chain Multiplication DP (Reverse Thinking)` | [#312](https://leetcode.com/problems/burst-balloons/) |
| 121 | [Regular Expression Matching](chapters/14_2d_dynamic_programming.md#121-regular-expression-matching) | 2-D Dynamic Programming | `Hard` | `2D Regex Parsing DP` | [#10](https://leetcode.com/problems/regular-expression-matching/) |
| 122 | [Maximum Subarray](chapters/15_greedy.md#122-maximum-subarray) | Greedy | `Medium` | `Kadane's Algorithm` | [#53](https://leetcode.com/problems/maximum-subarray/) |
| 123 | [Jump Game](chapters/15_greedy.md#123-jump-game) | Greedy | `Medium` | `Greedy Goal Post Shifting` | [#55](https://leetcode.com/problems/jump-game/) |
| 124 | [Jump Game II](chapters/15_greedy.md#124-jump-game-ii) | Greedy | `Medium` | `Greedy BFS Window Expansion` | [#45](https://leetcode.com/problems/jump-game-ii/) |
| 125 | [Gas Station](chapters/15_greedy.md#125-gas-station) | Greedy | `Medium` | `Greedy Reset Linear Scan` | [#134](https://leetcode.com/problems/gas-station/) |
| 126 | [Hand of Straights](chapters/15_greedy.md#126-hand-of-straights) | Greedy | `Medium` | `Min-Heap Frequency Greedy Matching` | [#846](https://leetcode.com/problems/hand-of-straights/) |
| 127 | [Merge Triplets to Form Target Triplet](chapters/15_greedy.md#127-merge-triplets-to-form-target-triplet) | Greedy | `Medium` | `Greedy Elimination Filter` | [#1899](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/) |
| 128 | [Partition Labels](chapters/15_greedy.md#128-partition-labels) | Greedy | `Medium` | `Last Occurrence Greedy Partitioning` | [#763](https://leetcode.com/problems/partition-labels/) |
| 129 | [Valid Parenthesis String](chapters/15_greedy.md#129-valid-parenthesis-string) | Greedy | `Medium` | `Greedy Min/Max Open Range` | [#678](https://leetcode.com/problems/valid-parenthesis-string/) |
| 130 | [Insert Interval](chapters/16_intervals.md#130-insert-interval) | Intervals | `Medium` | `Linear Insertion & Overlap Merging` | [#57](https://leetcode.com/problems/insert-interval/) |
| 131 | [Merge Intervals](chapters/16_intervals.md#131-merge-intervals) | Intervals | `Medium` | `Sort by Start Time + Overlap Merge` | [#56](https://leetcode.com/problems/merge-intervals/) |
| 132 | [Non-Overlapping Intervals](chapters/16_intervals.md#132-non-overlapping-intervals) | Intervals | `Medium` | `Greedy Interval Scheduling (Earliest End Time)` | [#435](https://leetcode.com/problems/non-overlapping-intervals/) |
| 133 | [Meeting Rooms](chapters/16_intervals.md#133-meeting-rooms) | Intervals | `Easy` | `Interval Overlap Detection` | [#252](https://neetcode.io/problems/meeting-schedule) |
| 134 | [Meeting Rooms II](chapters/16_intervals.md#134-meeting-rooms-ii) | Intervals | `Medium` | `Chronological Event Pointers / Min-Heap` | [#253](https://neetcode.io/problems/meeting-schedule-ii) |
| 135 | [Minimum Interval to Include Each Query](chapters/16_intervals.md#135-minimum-interval-to-include-each-query) | Intervals | `Hard` | `Offline Queries + Min-Heap Sweep-Line` | [#1851](https://leetcode.com/problems/minimum-interval-to-include-each-query/) |
| 136 | [Rotate Image](chapters/17_math_and_geometry.md#136-rotate-image) | Math & Geometry | `Medium` | `Layer-by-Layer 4-Way In-Place Rotation` | [#48](https://leetcode.com/problems/rotate-image/) |
| 137 | [Spiral Matrix](chapters/17_math_and_geometry.md#137-spiral-matrix) | Math & Geometry | `Medium` | `4-Boundary Perimeter Traversal` | [#54](https://leetcode.com/problems/spiral-matrix/) |
| 138 | [Set Matrix Zeroes](chapters/17_math_and_geometry.md#138-set-matrix-zeroes) | Math & Geometry | `Medium` | `O(1) Space In-Place Row/Col Flagging` | [#73](https://leetcode.com/problems/set-matrix-zeroes/) |
| 139 | [Happy Number](chapters/17_math_and_geometry.md#139-happy-number) | Math & Geometry | `Easy` | `Floyd's Cycle Detection / Hash Set` | [#202](https://leetcode.com/problems/happy-number/) |
| 140 | [Plus One](chapters/17_math_and_geometry.md#140-plus-one) | Math & Geometry | `Easy` | `Carry Array Simulation` | [#66](https://leetcode.com/problems/plus-one/) |
| 141 | [Pow(x, n)](chapters/17_math_and_geometry.md#141-powx,-n) | Math & Geometry | `Medium` | `Binary Exponentiation (Divide and Conquer)` | [#50](https://leetcode.com/problems/powx-n/) |
| 142 | [Multiply Strings](chapters/17_math_and_geometry.md#142-multiply-strings) | Math & Geometry | `Medium` | `Manual Multiplication Array Simulation` | [#43](https://leetcode.com/problems/multiply-strings/) |
| 143 | [Detect Squares](chapters/17_math_and_geometry.md#143-detect-squares) | Math & Geometry | `Medium` | `Diagonal Point Matching Hash Map` | [#2013](https://leetcode.com/problems/detect-squares/) |
| 144 | [Single Number](chapters/18_bit_manipulation.md#144-single-number) | Bit Manipulation | `Easy` | `XOR Parity Cancellation` | [#136](https://leetcode.com/problems/single-number/) |
| 145 | [Number of 1 Bits](chapters/18_bit_manipulation.md#145-number-of-1-bits) | Bit Manipulation | `Easy` | `Brian Kernighan's Algorithm (`n & (n - 1)`)` | [#191](https://leetcode.com/problems/number-of-1-bits/) |
| 146 | [Counting Bits](chapters/18_bit_manipulation.md#146-counting-bits) | Bit Manipulation | `Easy` | `Bit DP with Offset (`dp[i] = 1 + dp[i - offset]`)` | [#338](https://leetcode.com/problems/counting-bits/) |
| 147 | [Reverse Bits](chapters/18_bit_manipulation.md#147-reverse-bits) | Bit Manipulation | `Easy` | `Bit Shift & Masking` | [#190](https://leetcode.com/problems/reverse-bits/) |
| 148 | [Missing Number](chapters/18_bit_manipulation.md#148-missing-number) | Bit Manipulation | `Easy` | `XOR / Gauss Sum Formula` | [#268](https://leetcode.com/problems/missing-number/) |
| 149 | [Sum of Two Integers](chapters/18_bit_manipulation.md#149-sum-of-two-integers) | Bit Manipulation | `Medium` | `Bitwise Full Adder (`XOR` and `AND << 1`)` | [#371](https://leetcode.com/problems/sum-of-two-integers/) |
| 150 | [Reverse Integer](chapters/18_bit_manipulation.md#150-reverse-integer) | Bit Manipulation | `Medium` | `Digit Extraction & 32-Bit Overflow Prevention` | [#7](https://leetcode.com/problems/reverse-integer/) |

---

## 📖 Standard Pedagogical Template for Every Question

Each question in this curriculum is strictly engineered with 6 learning phases:
1. **Problem Statement & Standard Specification**: Complete problem description, constraints, and standard LeetCode/NeetCode formatted Input/Output examples.
2. **Intuitive Analogy & Mental Model**: Real-world analogy and conceptual visualization to build lasting intuition before writing code.
3. **Step-by-Step Progressive Hints**: Progressive hints (Hint 1: Direction & Data Structure, Hint 2: Invariant Transition, Hint 3: Concrete Step Logic) so you can test yourself before looking at the solution.
4. **Detailed Approach Walkthrough**: Step-by-step logic explaining the exact algorithmic mechanism.
5. **Canonical NeetCode Solution**: NeetCode's clean, idiomatic Python 3 solution with inline commentary.
6. **Complexity Analysis**: Big-O Time and Space complexities with rigorous justifications.

---

## 🖥️ Interactive Web Document & Print Book

Open [`index.html`](index.html) in any modern web browser to access the complete **Interactive Web Guide** featuring:
- 🔍 Live search by title, pattern, or category.
- 💡 Interactive collapsible hint accordions (practice without spoilers!).
- 🖨️ **Print-Ready 2-Questions-Per-Page Layout** (`Ctrl + P` / Print View toggle).
- 🌓 Dark & Light mode theme toggle.