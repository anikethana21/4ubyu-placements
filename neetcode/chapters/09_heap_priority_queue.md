# Chapter: Heap / Priority Queue

> Heaps provide logarithmic O(log n) insertions and O(1) minimum/maximum element access, making them ideal for dynamic top-k elements, scheduling, and streaming medians.

**Total Questions in Topic:** 7

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 64 | [Kth Largest Element in a Stream](#64-kth-largest-element-in-a-stream) | **Easy** | `Min-Heap of Size K` | [#703](https://leetcode.com/problems/kth-largest-element-in-a-stream/) |
| 65 | [Last Stone Weight](#65-last-stone-weight) | **Easy** | `Max-Heap Simulation` | [#1046](https://leetcode.com/problems/last-stone-weight/) |
| 66 | [K Closest Points to Origin](#66-k-closest-points-to-origin) | **Medium** | `Min-Heap / Max-Heap of Size K` | [#973](https://leetcode.com/problems/k-closest-points-to-origin/) |
| 67 | [Kth Largest Element in an Array](#67-kth-largest-element-in-an-array) | **Medium** | `QuickSelect / Min-Heap` | [#215](https://leetcode.com/problems/kth-largest-element-in-an-array/) |
| 68 | [Task Scheduler](#68-task-scheduler) | **Medium** | `Max-Heap + Cooldown Queue / Math Greedy` | [#621](https://leetcode.com/problems/task-scheduler/) |
| 69 | [Design Twitter](#69-design-twitter) | **Medium** | `Max-Heap + Hash Map (K-Way Merge)` | [#355](https://leetcode.com/problems/design-twitter/) |
| 70 | [Find Median from Data Stream](#70-find-median-from-data-stream) | **Hard** | `Two Heaps (Small Max-Heap & Large Min-Heap)` | [#295](https://leetcode.com/problems/find-median-from-data-stream/) |

---

## <a id="64-kth-largest-element-in-a-stream"></a>64. Kth Largest Element in a Stream

- **Difficulty:** `Easy`
- **Pattern:** `Min-Heap of Size K`
- **LeetCode Reference:** [LeetCode #703](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

### 1. Problem Statement
Design a class to find the `k-th` largest element in a stream. Note that it is the `k-th` largest element in the sorted order, not the `k-th` distinct element.

Implement `KthLargest` class:
- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `k-th` largest element in the stream.

#### Examples:
**Example 1:**
```text
Input: ["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output: [null, 4, 5, 5, 8, 8]
Explanation: KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
```

#### Constraints:
- `1 <= k <= 10^4`
- `0 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `At most 10^4 calls will be made to add.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Imagine a VIP lounge with only `k` seats for the wealthiest guests. Because the lounge is bounded to `k` seats, the poorest person currently sitting inside the lounge (`minHeap[0]`) is precisely the k-th wealthiest person overall.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain a Min-Heap of size `k`.
- Hint 2: When adding a new number, push it into the min-heap. If the heap size exceeds `k`, pop the minimum element.
- Hint 3: The root of the min-heap `self.minHeap[0]` is always the k-th largest element.

### 4. Detailed Approach Walkthrough
1. In `__init__`, store `self.minHeap = nums` and `self.k = k`.
2. Run `heapq.heapify(self.minHeap)`.
3. While `len(self.minHeap) > k`: `heapq.heappop(self.minHeap)`.
4. In `add(val)`: `heapq.heappush(self.minHeap, val)`.
5. If `len(self.minHeap) > self.k`: `heapq.heappop(self.minHeap)`.
6. Return `self.minHeap[0]`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq

class KthLargest:
    def __init__(self, k: int, nums: list[int]):
        self.minHeap = nums
        self.k = k
        heapq.heapify(self.minHeap)
        while len(self.minHeap) > k:
            heapq.heappop(self.minHeap)

    def add(self, val: int) -> int:
        heapq.heappush(self.minHeap, val)
        if len(self.minHeap) > self.k:
            heapq.heappop(self.minHeap)
        return self.minHeap[0]
```

### 6. Complexity Analysis
- **Time Complexity:** `Constructor: O(N log k); add: O(log k).`
- **Space Complexity:** `O(k) - Heap stores at most k elements.`

---

## <a id="65-last-stone-weight"></a>65. Last Stone Weight

- **Difficulty:** `Easy`
- **Pattern:** `Max-Heap Simulation`
- **LeetCode Reference:** [LeetCode #1046](https://leetcode.com/problems/last-stone-weight/)

### 1. Problem Statement
You are given an array of integers `stones` where `stones[i]` is the weight of the `i-th` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:
- If `x == y`, both stones are destroyed.
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left. Return the weight of the last remaining stone. If there are no stones left, return `0`.

#### Examples:
**Example 1:**
```text
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation: Smash 7 and 8 -> 1 remaining. Smash 4 and 2 -> 2 remaining. Smash 2 and 1 -> 1 remaining. Smash 1 and 1 -> 0 remaining. Last stone is 1.
```

#### Constraints:
- `1 <= stones.length <= 30`
- `1 <= stones[i] <= 1000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A gladiator tournament where the two biggest contenders always fight each other first. The damage is calculated, and the wounded survivor re-enters the arena until at most one fighter remains.

### 3. Step-by-Step Progressive Hints
- Hint 1: Python provides `heapq` as a min-heap by default. Multiply all values by `-1` to simulate a max-heap.
- Hint 2: Pop the two largest stones `first = -heappop()` and `second = -heappop()`.
- Hint 3: If `second < first`, push `-(first - second)` back into the heap.

### 4. Detailed Approach Walkthrough
1. Negate all stone weights: `stones = [-s for s in stones]`.
2. `heapq.heapify(stones)`.
3. While `len(stones) > 1`:
   - `first = abs(heapq.heappop(stones))`
   - `second = abs(heapq.heappop(stones))`
   - If `second < first`:
     - `heapq.heappush(stones, -(first - second))`
4. Return `abs(stones[0])` if `stones` else 0.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq

class Solution:
    def lastStoneWeight(self, stones: list[int]) -> int:
        stones = [-s for s in stones]
        heapq.heapify(stones)
        
        while len(stones) > 1:
            first = abs(heapq.heappop(stones))
            second = abs(heapq.heappop(stones))
            if second < first:
                heapq.heappush(stones, -(first - second))
                
        return abs(stones[0]) if stones else 0
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n log n) - In the worst case, n smashes with O(log n) heap operations.`
- **Space Complexity:** `O(1) extra space or O(n) for negated array.`

---

## <a id="66-k-closest-points-to-origin"></a>66. K Closest Points to Origin

- **Difficulty:** `Medium`
- **Pattern:** `Min-Heap / Max-Heap of Size K`
- **LeetCode Reference:** [LeetCode #973](https://leetcode.com/problems/k-closest-points-to-origin/)

### 1. Problem Statement
Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance: `sqrt((x1 - x2)^2 + (y1 - y2)^2)`.

You may return the answer in **any order**.

#### Examples:
**Example 1:**
```text
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]
Explanation: Distance of (1, 3) is sqrt(10). Distance of (-2, 2) is sqrt(8). Since sqrt(8) < sqrt(10), [-2, 2] is closer.
```

**Example 2:**
```text
Input: points = [[3,3],[5,-1],[-2,4]], k = 2
Output: [[3,3],[-2,4]]
Explanation: Distances are 18, 26, 20. Two closest are [3,3] and [-2,4].
```

#### Constraints:
- `1 <= k <= points.length <= 10^4`
- `-10^4 <= xi, yi <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Throwing darts onto a target board: calculate squared distance `x^2 + y^2` (no need to compute slow square roots) and pick the `k` darts closest to the bullseye.

### 3. Step-by-Step Progressive Hints
- Hint 1: Euclidean distance comparison does not require `sqrt` since `x^2 + y^2` preserves relative ordering.
- Hint 2: Compute `[x**2 + y**2, x, y]` for all points and heapify in O(n).
- Hint 3: Pop from the min-heap `k` times and collect the coordinates.

### 4. Detailed Approach Walkthrough
1. Build `minHeap = [[x**2 + y**2, x, y] for x, y in points]`.
2. `heapq.heapify(minHeap)`.
3. Initialize `res = []`.
4. Loop `k` times: pop `dist, x, y = heapq.heappop(minHeap)` and append `[x, y]` to `res`.
5. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq

class Solution:
    def kClosest(self, points: list[list[int]], k: int) -> list[list[int]]:
        minHeap = []
        for x, y in points:
            dist = (x ** 2) + (y ** 2)
            minHeap.append([dist, x, y])
            
        heapq.heapify(minHeap)
        res = []
        while k > 0:
            dist, x, y = heapq.heappop(minHeap)
            res.append([x, y])
            k -= 1
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(k log n) - Heapify is O(n), followed by k extractions of O(log n).`
- **Space Complexity:** `O(n) - Heap stores all points.`

---

## <a id="67-kth-largest-element-in-an-array"></a>67. Kth Largest Element in an Array

- **Difficulty:** `Medium`
- **Pattern:** `QuickSelect / Min-Heap`
- **LeetCode Reference:** [LeetCode #215](https://leetcode.com/problems/kth-largest-element-in-an-array/)

### 1. Problem Statement
Given an integer array `nums` and an integer `k`, return the `k-th` largest element in the array.

Note that it is the `k-th` largest element in the sorted order, not the `k-th` distinct element.

Can you solve it without sorting in `O(n)` average time?

#### Examples:
**Example 1:**
```text
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
Explanation: Sorted order is [1,2,3,4,5,6], 2nd largest is 5.
```

**Example 2:**
```text
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
Explanation: 4th largest element is 4.
```

#### Constraints:
- `1 <= k <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> QuickSelect is like QuickSort's laser-focused sibling: after partitioning around a pivot, if the pivot lands right on index `target = len(nums) - k`, you're finished immediately! If not, only recurse on the single side containing the target index.

### 3. Step-by-Step Progressive Hints
- Hint 1: The k-th largest element is equivalent to the `(len(nums) - k)`-th smallest element (0-indexed).
- Hint 2: QuickSelect partitions array around a pivot in O(n) average time.
- Hint 3: If pivot index `p == k`, return `nums[p]`. If `p < k`, search right `[p+1..r]`. If `p > k`, search left `[l..p-1]`.

### 4. Detailed Approach Walkthrough
1. `k = len(nums) - k` (target index for k-th smallest).
2. Define `quickSelect(l, r)`:
   - Pivot `pivot = nums[r]`, `p = l`
   - For `i` from `l` to `r - 1`:
     - If `nums[i] <= pivot`: swap `nums[p], nums[i]`; `p += 1`
   - Swap `nums[p], nums[r]`
   - If `p > k`: return `quickSelect(l, p - 1)`
   - Else if `p < k`: return `quickSelect(p + 1, r)`
   - Else: return `nums[p]`
3. Return `quickSelect(0, len(nums) - 1)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findKthLargest(self, nums: list[int], k: int) -> int:
        k = len(nums) - k
        
        def quickSelect(l, r):
            pivot, p = nums[r], l
            for i in range(l, r):
                if nums[i] <= pivot:
                    nums[p], nums[i] = nums[i], nums[p]
                    p += 1
            nums[p], nums[r] = nums[r], nums[p]
            
            if p > k:
                return quickSelect(l, p - 1)
            elif p < k:
                return quickSelect(p + 1, r)
            else:
                return nums[p]
                
        return quickSelect(0, len(nums) - 1)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) average time with QuickSelect (O(n^2) worst case) or O(n log k) using Min-Heap.`
- **Space Complexity:** `O(1) auxiliary space (in-place partitioning).`

---

## <a id="68-task-scheduler"></a>68. Task Scheduler

- **Difficulty:** `Medium`
- **Pattern:** `Max-Heap + Cooldown Queue / Math Greedy`
- **LeetCode Reference:** [LeetCode #621](https://leetcode.com/problems/task-scheduler/)

### 1. Problem Statement
Given a characters array `tasks`, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.

However, there is a non-negative integer `n` that represents the cooldown period between two **same tasks** (the same letter in the array), that is that there must be at least `n` units of time between any two same tasks.

Return the **least number of units of times** that the CPU will take to finish all the given tasks.

#### Examples:
**Example 1:**
```text
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B. Total time = 8.
```

**Example 2:**
```text
Input: tasks = ["A","A","A","B","B","B"], n = 0
Output: 6
Explanation: No cooldown needed, total time = 6.
```

#### Constraints:
- `1 <= tasks.length <= 10^4`
- `tasks[i] is upper-case English letter.`
- `0 <= n <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Greedy scheduling: always process the task with the highest remaining frequency first (Max-Heap) to avoid having leftover identical tasks crammed together creating massive idle penalties at the end. While cooling down, tasks rest in a waiting queue `[remaining_count, available_time]`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a Max-Heap to track task frequencies.
- Hint 2: Use a Queue `q` storing pairs `[-remaining_count, idle_time_ready]`.
- Hint 3: In each time step `time += 1`, pop the most frequent task from max-heap, decrement its count, and if count > 0, push to `q` with `time + n`. If `q` has tasks ready at `time`, push them back into max-heap.

### 4. Detailed Approach Walkthrough
1. Count task frequencies with `collections.Counter(tasks)`.
2. Initialize `maxHeap = [-cnt for cnt in count.values()]`, `heapq.heapify(maxHeap)`.
3. `q = collections.deque()`, `time = 0`.
4. While `maxHeap` or `q`:
   - `time += 1`
   - If `maxHeap`:
     - `cnt = 1 + heapq.heappop(maxHeap)` (since values are negative)
     - If `cnt != 0`: `q.append([cnt, time + n])`
   - If `q` and `q[0][1] == time`:
     - `heapq.heappush(maxHeap, q.popleft()[0])`
5. Return `time`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq
import collections

class Solution:
    def leastInterval(self, tasks: list[str], n: int) -> int:
        count = collections.Counter(tasks)
        maxHeap = [-cnt for cnt in count.values()]
        heapq.heapify(maxHeap)
        
        time = 0
        q = collections.deque()  # pairs: [-cnt, idleTime]
        
        while maxHeap or q:
            time += 1
            
            if maxHeap:
                cnt = 1 + heapq.heappop(maxHeap)
                if cnt:
                    q.append([cnt, time + n])
                    
            if q and q[0][1] == time:
                heapq.heappush(maxHeap, q.popleft()[0])
                
        return time
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * n) where N is total tasks or O(N) since unique tasks <= 26.`
- **Space Complexity:** `O(1) - Max-heap and queue size bounded by 26 English letters.`

---

## <a id="69-design-twitter"></a>69. Design Twitter

- **Difficulty:** `Medium`
- **Pattern:** `Max-Heap + Hash Map (K-Way Merge)`
- **LeetCode Reference:** [LeetCode #355](https://leetcode.com/problems/design-twitter/)

### 1. Problem Statement
Design a simplified version of Twitter where users can post tweets, follow/unfollow another user, and is able to see the `10` most recent tweets in the user's news feed.

Implement the `Twitter` class:
- `Twitter()` Initializes your twitter object.
- `void postTweet(int userId, int tweetId)` Composes a new tweet with ID `tweetId` by the user `userId`.
- `List<Integer> getNewsFeed(int userId)` Retrieves the 10 most recent tweet IDs in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user themself. Tweets must be **ordered from most recent to least recent**.
- `void follow(int followerId, int followeeId)` The user with ID `followerId` started following the user with ID `followeeId`.
- `void unfollow(int followerId, int followeeId)` The user with ID `followerId` started unfollowing the user with ID `followeeId`.

#### Examples:
**Example 1:**
```text
Input: ["Twitter", "postTweet", "getNewsFeed", "follow", "postTweet", "getNewsFeed", "unfollow", "getNewsFeed"]
[[], [1, 5], [1], [1, 2], [2, 6], [1], [1, 2], [1]]
Output: [null, null, [5], null, null, [6, 5], null, [5]]
Explanation: Twitter twitter = new Twitter();
twitter.postTweet(1, 5); // User 1 posts tweet 5
twitter.getNewsFeed(1);  // returns [5]
twitter.follow(1, 2);    // User 1 follows user 2
twitter.postTweet(2, 6); // User 2 posts tweet 6
twitter.getNewsFeed(1);  // returns [6, 5]
twitter.unfollow(1, 2);  // User 1 unfollows user 2
twitter.getNewsFeed(1);  // returns [5]
```

#### Constraints:
- `1 <= userId, followerId, followeeId <= 500`
- `0 <= tweetId <= 10^4`
- `All the tweets have unique IDs.`
- `At most 3 * 10^4 calls will be made to postTweet, getNewsFeed, follow, and unfollow.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Like merging the most recent messages across multiple chat channels: each followed friend has a timeline sorted by timestamp. Using a Max-Heap, you pull the newest tweet among all friends, advance that friend's pointer, and repeat up to 10 times.

### 3. Step-by-Step Progressive Hints
- Hint 1: Maintain a global decrementing `count` variable to assign decreasing timestamps to tweets.
- Hint 2: Store tweets in `tweetMap = defaultdict(list)` mapping `userId -> list of [count, tweetId]`.
- Hint 3: In `getNewsFeed`, push the most recent tweet of every followed user (plus self) into a min/max-heap and pop up to 10 times (K-Way Merge).

### 4. Detailed Approach Walkthrough
1. `count`: global timestamp counter (decrementing from 0).
2. `tweetMap`: `defaultdict(list)` mapping `userId -> [[count, tweetId], ...]`.
3. `followMap`: `defaultdict(set)` mapping `userId -> {followeeId, ...}`.
4. `postTweet`: append `[count, tweetId]` to `tweetMap[userId]`, decrement `count`.
5. `follow`: add `followeeId` to `followMap[followerId]`.
6. `unfollow`: remove `followeeId` from `followMap[followerId]` if present.
7. `getNewsFeed`: gather followed users + self. Push `[count, tweetId, followeeId, nextIndex]` into minHeap. Pop top 10 tweets and advance user indices.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq
import collections

class Twitter:
    def __init__(self):
        self.count = 0
        self.tweetMap = collections.defaultdict(list)  # userId -> list of [count, tweetId]
        self.followMap = collections.defaultdict(set)  # userId -> set of followeeIds

    def postTweet(self, userId: int, tweetId: int) -> None:
        self.tweetMap[userId].append([self.count, tweetId])
        self.count -= 1

    def getNewsFeed(self, userId: int) -> list[int]:
        res = []
        minHeap = []
        
        self.followMap[userId].add(userId)  # user follows self
        for followeeId in self.followMap[userId]:
            if followeeId in self.tweetMap and self.tweetMap[followeeId]:
                index = len(self.tweetMap[followeeId]) - 1
                count, tweetId = self.tweetMap[followeeId][index]
                minHeap.append([count, tweetId, followeeId, index - 1])
                
        heapq.heapify(minHeap)
        while minHeap and len(res) < 10:
            count, tweetId, followeeId, index = heapq.heappop(minHeap)
            res.append(tweetId)
            if index >= 0:
                count, tweetId = self.tweetMap[followeeId][index]
                heapq.heappush(minHeap, [count, tweetId, followeeId, index - 1])
                
        return res

    def follow(self, followerId: int, followeeId: int) -> None:
        self.followMap[followerId].add(followeeId)

    def unfollow(self, followerId: int, followeeId: int) -> None:
        if followeeId in self.followMap[followerId]:
            self.followMap[followerId].remove(followeeId)
```

### 6. Complexity Analysis
- **Time Complexity:** `postTweet: O(1); getNewsFeed: O(k log N) where k=10 and N is number of followees.`
- **Space Complexity:** `O(U + T) - Where U is total users/relationships and T is total tweets.`

---

## <a id="70-find-median-from-data-stream"></a>70. Find Median from Data Stream

- **Difficulty:** `Hard`
- **Pattern:** `Two Heaps (Small Max-Heap & Large Min-Heap)`
- **LeetCode Reference:** [LeetCode #295](https://leetcode.com/problems/find-median-from-data-stream/)

### 1. Problem Statement
The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

Implement the `MedianFinder` class:
- `MedianFinder()` initializes the `MedianFinder` object.
- `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far.

#### Examples:
**Example 1:**
```text
Input: ["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output: [null, null, null, 1.5, null, 2.0]
Explanation: MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
```

#### Constraints:
- `-10^5 <= num <= 10^5`
- `There will be at least one element in the data structure before calling findMedian.`
- `At most 5 * 10^4 calls will be made to addNum and findMedian.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Picture an hourglass: the bottom bulb is a Max-Heap holding the smaller half of all numbers, and the top bulb is a Min-Heap holding the larger half of all numbers. The meeting junction where sand passes through is precisely the median!

### 3. Step-by-Step Progressive Hints
- Hint 1: Use two heaps: `small` (Max-Heap) for smaller numbers and `large` (Min-Heap) for larger numbers.
- Hint 2: Maintain two invariants: 1) Every element in `small` <= every element in `large`. 2) Size difference `abs(len(small) - len(large)) <= 1`.
- Hint 3: If total length is odd, median is the top of the larger heap. If even, median is `(-small[0] + large[0]) / 2.0`.

### 4. Detailed Approach Walkthrough
1. Initialize `self.small = []` (max-heap) and `self.large = []` (min-heap).
2. `addNum(num)`:
   - Push `num` into `self.small` (`heapq.heappush(self.small, -1 * num)`).
   - If `self.small` and `self.large` and `(-1 * self.small[0]) > self.large[0]`:
     - `val = -1 * heapq.heappop(self.small)`
     - `heapq.heappush(self.large, val)`
   - Balance sizes:
     - If `len(self.small) > len(self.large) + 1`:
       - `val = -1 * heapq.heappop(self.small)`
       - `heapq.heappush(self.large, val)`
     - If `len(self.large) > len(self.small) + 1`:
       - `val = heapq.heappop(self.large)`
       - `heapq.heappush(self.small, -1 * val)`
3. `findMedian()`:
   - If `len(self.small) > len(self.large)`: return `-1 * self.small[0]`
   - If `len(self.large) > len(self.small)`: return `self.large[0]`
   - Return `(-1 * self.small[0] + self.large[0]) / 2.0`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq

class MedianFinder:
    def __init__(self):
        # small: maxHeap, large: minHeap
        self.small, self.large = [], []

    def addNum(self, num: int) -> None:
        heapq.heappush(self.small, -1 * num)
        
        # Invariant 1: all elements in small <= all in large
        if self.small and self.large and (-1 * self.small[0]) > self.large[0]:
            val = -1 * heapq.heappop(self.small)
            heapq.heappush(self.large, val)
            
        # Invariant 2: size difference <= 1
        if len(self.small) > len(self.large) + 1:
            val = -1 * heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        if len(self.large) > len(self.small) + 1:
            val = heapq.heappop(self.large)
            heapq.heappush(self.small, -1 * val)

    def findMedian(self) -> float:
        if len(self.small) > len(self.large):
            return -1 * self.small[0]
        if len(self.large) > len(self.small):
            return self.large[0]
        return (-1 * self.small[0] + self.large[0]) / 2.0
```

### 6. Complexity Analysis
- **Time Complexity:** `addNum: O(log n); findMedian: O(1).`
- **Space Complexity:** `O(n) - Storing n elements across two heaps.`

---
