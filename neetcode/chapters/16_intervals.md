# Chapter: Intervals

> Interval problems deal with ranges of time or coordinates, relying heavily on sorting by start/end times, greedy overlap merges, and min-heap tracking.

**Total Questions in Topic:** 6

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 130 | [Insert Interval](#130-insert-interval) | **Medium** | `Linear Insertion & Overlap Merging` | [#57](https://leetcode.com/problems/insert-interval/) |
| 131 | [Merge Intervals](#131-merge-intervals) | **Medium** | `Sort by Start Time + Overlap Merge` | [#56](https://leetcode.com/problems/merge-intervals/) |
| 132 | [Non-Overlapping Intervals](#132-non-overlapping-intervals) | **Medium** | `Greedy Interval Scheduling (Earliest End Time)` | [#435](https://leetcode.com/problems/non-overlapping-intervals/) |
| 133 | [Meeting Rooms](#133-meeting-rooms) | **Easy** | `Interval Overlap Detection` | [#252](https://neetcode.io/problems/meeting-schedule) |
| 134 | [Meeting Rooms II](#134-meeting-rooms-ii) | **Medium** | `Chronological Event Pointers / Min-Heap` | [#253](https://neetcode.io/problems/meeting-schedule-ii) |
| 135 | [Minimum Interval to Include Each Query](#135-minimum-interval-to-include-each-query) | **Hard** | `Offline Queries + Min-Heap Sweep-Line` | [#1851](https://leetcode.com/problems/minimum-interval-to-include-each-query/) |

---

## <a id="130-insert-interval"></a>130. Insert Interval

- **Difficulty:** `Medium`
- **Pattern:** `Linear Insertion & Overlap Merging`
- **LeetCode Reference:** [LeetCode #57](https://leetcode.com/problems/insert-interval/)

### 1. Problem Statement
You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `i-th` interval and `intervals` is sorted in ascending order by `starti`.

You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

#### Examples:
**Example 1:**
```text
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
Explanation: Interval [2,5] overlaps with [1,3], merging into [1,5].
```

**Example 2:**
```text
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Interval [4,8] overlaps with [3,5],[6,7],[8,10], merging into [3,10].
```

#### Constraints:
- `0 <= intervals.length <= 10^4`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 10^5`
- `intervals is sorted by starti in ascending order.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Booking a new meeting in a calendar: before your meeting starts, add all finished meetings to the itinerary. When meetings overlap with yours, expand your meeting window `[min(start), max(end)]`. Once past the overlap, drop the expanded meeting and append all remaining future meetings.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `newInterval[1] < intervals[i][0]`, `newInterval` comes strictly before `intervals[i]`: append `newInterval` and the rest of the array, then return.
- Hint 2: If `newInterval[0] > intervals[i][1]`, `intervals[i]` comes strictly before `newInterval`: append `intervals[i]`.
- Hint 3: Otherwise, overlap occurs: update `newInterval = [min(newInterval[0], intervals[i][0]), max(newInterval[1], intervals[i][1])]`.

### 4. Detailed Approach Walkthrough
1. Initialize `res = []`.
2. Iterate through index `i` and interval in `intervals`:
   - If `newInterval[1] < intervals[i][0]`: `res.append(newInterval); return res + intervals[i:]`
   - Else if `newInterval[0] > intervals[i][1]`: `res.append(intervals[i])`
   - Else: `newInterval = [min(newInterval[0], intervals[i][0]), max(newInterval[1], intervals[i][1])]`
3. `res.append(newInterval)`.
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def insert(self, intervals: list[list[int]], newInterval: list[int]) -> list[list[int]]:
        res = []
        
        for i in range(len(intervals)):
            if newInterval[1] < intervals[i][0]:
                res.append(newInterval)
                return res + intervals[i:]
            elif newInterval[0] > intervals[i][1]:
                res.append(intervals[i])
            else:
                newInterval = [
                    min(newInterval[0], intervals[i][0]),
                    max(newInterval[1], intervals[i][1])
                ]
                
        res.append(newInterval)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n) - Single pass over intervals.`
- **Space Complexity:** `O(n) - Output array.`

---

## <a id="131-merge-intervals"></a>131. Merge Intervals

- **Difficulty:** `Medium`
- **Pattern:** `Sort by Start Time + Overlap Merge`
- **LeetCode Reference:** [LeetCode #56](https://leetcode.com/problems/merge-intervals/)

### 1. Problem Statement
Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return an array of the **non-overlapping intervals** that cover all the intervals in the input.

#### Examples:
**Example 1:**
```text
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Intervals [1,3] and [2,6] overlap, merging into [1,6].
```

**Example 2:**
```text
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

#### Constraints:
- `1 <= intervals.length <= 10^4`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Merging paint brush strokes along a timeline: sort strokes by their starting point. If a new stroke begins before the previous stroke finishes (`start <= prevEnd`), extend the previous stroke's endpoint to `max(prevEnd, end)`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort intervals by starting time: `intervals.sort(key=lambda i: i[0])`.
- Hint 2: Initialize `output = [intervals[0]]`.
- Hint 3: For each interval, if `start <= output[-1][1]`, merge: `output[-1][1] = max(output[-1][1], end)`. Else append `[start, end]`.

### 4. Detailed Approach Walkthrough
1. Sort `intervals` by `i[0]`.
2. Initialize `output = [intervals[0]]`.
3. For `start, end` in `intervals[1:]`:
   - `lastEnd = output[-1][1]`
   - If `start <= lastEnd`:
     - `output[-1][1] = max(lastEnd, end)`
   - Else:
     - `output.append([start, end])`
4. Return `output`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def merge(self, intervals: list[list[int]]) -> list[list[int]]:
        intervals.sort(key=lambda i: i[0])
        output = [intervals[0]]
        
        for start, end in intervals[1:]:
            lastEnd = output[-1][1]
            
            if start <= lastEnd:
                output[-1][1] = max(lastEnd, end)
            else:
                output.append([start, end])
                
        return output
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n log n) - Dominated by sorting intervals.`
- **Space Complexity:** `O(n) - Output list and sort buffer.`

---

## <a id="132-non-overlapping-intervals"></a>132. Non-Overlapping Intervals

- **Difficulty:** `Medium`
- **Pattern:** `Greedy Interval Scheduling (Earliest End Time)`
- **LeetCode Reference:** [LeetCode #435](https://leetcode.com/problems/non-overlapping-intervals/)

### 1. Problem Statement
Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return the **minimum number of intervals** you need to remove to make the rest of the intervals non-overlapping.

#### Examples:
**Example 1:**
```text
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.
```

**Example 2:**
```text
Input: intervals = [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to model non-overlapping intervals.
```

#### Constraints:
- `1 <= intervals.length <= 10^5`
- `intervals[i].length == 2`
- `-5 * 10^4 <= starti < endi <= 5 * 10^4`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Booking the maximum number of movie screenings in a theater: when two movies clash, greedily keep the movie that FINISHES EARLIEST (`min(end1, end2)`), because it leaves the maximum free time for future movies.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort intervals by start time.
- Hint 2: Track `prevEnd = intervals[0][1]`, `res = 0`.
- Hint 3: If `start < prevEnd` (overlap), increment `res += 1` and greedily keep the interval with smaller end time: `prevEnd = min(end, prevEnd)`. Else update `prevEnd = end`.

### 4. Detailed Approach Walkthrough
1. Sort `intervals` by `i[0]`.
2. `res = 0, prevEnd = intervals[0][1]`.
3. For `start, end` in `intervals[1:]`:
   - If `start >= prevEnd`:
     - `prevEnd = end`
   - Else:
     - `res += 1`
     - `prevEnd = min(end, prevEnd)`
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def eraseOverlapIntervals(self, intervals: list[list[int]]) -> int:
        intervals.sort()
        res = 0
        prevEnd = intervals[0][1]
        
        for start, end in intervals[1:]:
            if start >= prevEnd:
                prevEnd = end
            else:
                res += 1
                prevEnd = min(end, prevEnd)
                
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n log n) - Sorting intervals.`
- **Space Complexity:** `O(1) - Constant auxiliary space.`

---

## <a id="133-meeting-rooms"></a>133. Meeting Rooms

- **Difficulty:** `Easy`
- **Pattern:** `Interval Overlap Detection`
- **LeetCode Reference:** [LeetCode #252](https://neetcode.io/problems/meeting-schedule)

### 1. Problem Statement
Given an array of meeting time interval objects consisting of start and end times `[[start_1,end_1],[start_2,end_2],...]` (`start_i < end_i`), determine if a person could attend all meetings.

#### Examples:
**Example 1:**
```text
Input: intervals = [(0,30),(5,10),(15,20)]
Output: false
Explanation: (0,30) overlaps with (5,10) and (15,20).
```

**Example 2:**
```text
Input: intervals = [(5,8),(9,15)]
Output: true
Explanation: No overlapping intervals.
```

#### Constraints:
- `0 <= intervals.length <= 500`
- `0 <= start < end <= 10^6`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A person can only be in one conference room at a time: sort meetings by start time, and check if any meeting begins before the previous one concludes.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort meetings by start time.
- Hint 2: For each adjacent pair `intervals[i]` and `intervals[i+1]`, if `intervals[i][1] > intervals[i+1][0]`, return False.

### 4. Detailed Approach Walkthrough
1. Sort `intervals` by `i[0]`.
2. For `i` in range(`len(intervals) - 1`):
   - If `intervals[i][1] > intervals[i + 1][0]`:
     - return `False`
3. Return `True`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def canAttendMeetings(self, intervals: list[list[int]]) -> bool:
        intervals.sort(key=lambda i: i[0])
        
        for i in range(len(intervals) - 1):
            if intervals[i][1] > intervals[i + 1][0]:
                return False
                
        return True
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n log n) - Sorting meetings.`
- **Space Complexity:** `O(1) - In-place comparison.`

---

## <a id="134-meeting-rooms-ii"></a>134. Meeting Rooms II

- **Difficulty:** `Medium`
- **Pattern:** `Chronological Event Pointers / Min-Heap`
- **LeetCode Reference:** [LeetCode #253](https://neetcode.io/problems/meeting-schedule-ii)

### 1. Problem Statement
Given an array of meeting time intervals consisting of start and end times `[[start_1,end_1],[start_2,end_2],...]`, find the **minimum number of conference rooms** required.

#### Examples:
**Example 1:**
```text
Input: intervals = [(0,40),(5,10),(15,20)]
Output: 2
Explanation: Room 1: (0, 40); Room 2: (5, 10) and (15, 20).
```

**Example 2:**
```text
Input: intervals = [(4,9)]
Output: 1
Explanation: Single meeting requires 1 room.
```

#### Constraints:
- `1 <= intervals.length <= 10^4`
- `0 <= start < end <= 10^6`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Turnstile counter tracking concurrent room occupancy: whenever a meeting starts (`start[s] < end[e]`), increment active room count `count += 1`. Whenever a meeting ends (`end[e] <= start[s]`), decrement active room count `count -= 1`. The peak count reached is the minimum rooms required.

### 3. Step-by-Step Progressive Hints
- Hint 1: Extract and sort all start times into `start = sorted(...)` and all end times into `end = sorted(...)`.
- Hint 2: Maintain two pointers `s, e = 0, 0` and track `count` and `res`.
- Hint 3: If `start[s] < end[e]`, `count += 1; s += 1`. Else `count -= 1; e += 1`.

### 4. Detailed Approach Walkthrough
1. `start = sorted([i[0] for i in intervals])`.
2. `end = sorted([i[1] for i in intervals])`.
3. `res, count = 0, 0`, `s, e = 0, 0`.
4. While `s < len(intervals)`:
   - If `start[s] < end[e]`:
     - `count += 1; s += 1`
   - Else:
     - `count -= 1; e += 1`
   - `res = max(res, count)`
5. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def minMeetingRooms(self, intervals: list[list[int]]) -> int:
        start = sorted([i[0] for i in intervals])
        end = sorted([i[1] for i in intervals])
        
        res, count = 0, 0
        s, e = 0, 0
        
        while s < len(intervals):
            if start[s] < end[e]:
                s += 1
                count += 1
            else:
                e += 1
                count -= 1
            res = max(res, count)
            
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(n log n) - Sorting start and end time arrays.`
- **Space Complexity:** `O(n) - Storing separate start and end arrays.`

---

## <a id="135-minimum-interval-to-include-each-query"></a>135. Minimum Interval to Include Each Query

- **Difficulty:** `Hard`
- **Pattern:** `Offline Queries + Min-Heap Sweep-Line`
- **LeetCode Reference:** [LeetCode #1851](https://leetcode.com/problems/minimum-interval-to-include-each-query/)

### 1. Problem Statement
You are given a 2D integer array `intervals`, where `intervals[i] = [lefti, righti]` describes the `i-th` interval. The **size** of an interval is defined as `righti - lefti + 1`.

You are also given an integer array `queries`. The answer to the `j-th` query is the **minimum size** of an interval `i` such that `lefti <= queries[j] <= righti`. If no such interval exists, the answer is `-1`.

Return an array `ans` where `ans[j]` is the answer to the `j-th` query.

#### Examples:
**Example 1:**
```text
Input: intervals = [[1,4],[2,4],[3,6],[4,4]], queries = [2,3,4,5]
Output: [3,3,1,4]
Explanation: Query 2: [2,4] (size 3); Query 3: [2,4] (size 3); Query 4: [4,4] (size 1); Query 5: [3,6] (size 4).
```

#### Constraints:
- `1 <= intervals.length <= 10^5`
- `1 <= queries.length <= 10^5`
- `intervals[i].length == 2`
- `1 <= lefti <= righti <= 10^7`
- `1 <= queries[j] <= 10^7`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Processing queries in sorted chronological order (sweep-line): as you advance `q`, activate all intervals whose `start <= q` by pushing `[size, right]` into a Min-Heap. Then discard all expired intervals where `right < q`. The top of the min-heap immediately yields the smallest valid interval enclosing `q`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort both `intervals` and `queries` (keeping original query indices).
- Hint 2: Maintain a Min-Heap storing pairs `[interval_size, end_time]`.
- Hint 3: For each query `q`, push all intervals with `left <= q`. Pop expired intervals with `end < q`. Answer for `q` is `minHeap[0][0]` if heap non-empty else -1.

### 4. Detailed Approach Walkthrough
1. Sort `intervals`.
2. `minHeap = []`, `res = {}`, `i = 0`.
3. For `q` in `sorted(queries)`:
   - While `i < len(intervals)` and `intervals[i][0] <= q`:
     - `l, r = intervals[i]`
     - `heapq.heappush(minHeap, (r - l + 1, r))`
     - `i += 1`
   - While `minHeap` and `minHeap[0][1] < q`:
     - `heapq.heappop(minHeap)`
   - `res[q] = minHeap[0][0] if minHeap else -1`
4. Return `[res[q] for q in queries]`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq

class Solution:
    def minInterval(self, intervals: list[list[int]], queries: list[int]) -> list[int]:
        intervals.sort()
        minHeap = []
        res = {}
        i = 0
        
        for q in sorted(queries):
            while i < len(intervals) and intervals[i][0] <= q:
                l, r = intervals[i]
                heapq.heappush(minHeap, (r - l + 1, r))
                i += 1
                
            while minHeap and minHeap[0][1] < q:
                heapq.heappop(minHeap)
                
            res[q] = minHeap[0][0] if minHeap else -1
            
        return [res[q] for q in queries]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N log N + Q log Q) - Sorting intervals and queries with heap operations.`
- **Space Complexity:** `O(N + Q) - Min-heap and result dictionary.`

---
