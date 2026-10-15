# Chapter: Advanced Graphs

> Advanced graph topics cover Dijkstra's shortest path, Prim's / Kruskal's Minimum Spanning Tree (MST), Eulerian Path (Hierholzer's), and Bellman-Ford algorithms.

**Total Questions in Topic:** 6

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 93 | [Reconstruct Itinerary](#93-reconstruct-itinerary) | **Hard** | `Eulerian Path (Hierholzer's Algorithm)` | [#332](https://leetcode.com/problems/reconstruct-itinerary/) |
| 94 | [Min Cost to Connect All Points](#94-min-cost-to-connect-all-points) | **Medium** | `Minimum Spanning Tree (Prim's Algorithm)` | [#1584](https://leetcode.com/problems/min-cost-to-connect-all-points/) |
| 95 | [Network Delay Time](#95-network-delay-time) | **Medium** | `Dijkstra's Shortest Path` | [#743](https://leetcode.com/problems/network-delay-time/) |
| 96 | [Swim in Rising Water](#96-swim-in-rising-water) | **Hard** | `Modified Dijkstra (Minimax Path)` | [#778](https://leetcode.com/problems/swim-in-rising-water/) |
| 97 | [Alien Dictionary](#97-alien-dictionary) | **Hard** | `Topological Sort on Character Graph` | [#269](https://neetcode.io/problems/foreign-dictionary) |
| 98 | [Cheapest Flights Within K Stops](#98-cheapest-flights-within-k-stops) | **Medium** | `Bellman-Ford / BFS Level Relaxation` | [#787](https://leetcode.com/problems/cheapest-flights-within-k-stops/) |

---

## <a id="93-reconstruct-itinerary"></a>93. Reconstruct Itinerary

- **Difficulty:** `Hard`
- **Pattern:** `Eulerian Path (Hierholzer's Algorithm)`
- **LeetCode Reference:** [LeetCode #332](https://leetcode.com/problems/reconstruct-itinerary/)

### 1. Problem Statement
You are given a list of airline `tickets` where `tickets[i] = [fromi, toi]` represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from `"JFK"`, thus, the itinerary must begin with `"JFK"`.

If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. You must use all the tickets once and only once.

#### Examples:
**Example 1:**
```text
Input: tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
Output: ["JFK","MUC","LHR","SFO","SJC"]
Explanation: All tickets visited in order starting from JFK.
```

#### Constraints:
- `1 <= tickets.length <= 300`
- `tickets[i].length == 2`
- `fromi.length == 3, toi.length == 3`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Drawing a continuous figure without lifting your pencil from paper (Eulerian path): sort destinations alphabetically, follow the trail until you hit a dead-end airport, and record that dead-end at the back of the route.

### 3. Step-by-Step Progressive Hints
- Hint 1: Sort tickets in descending alphabetical order so we can pop from the back of adjacency lists in O(1).
- Hint 2: Use DFS: while `adj[src]` has outgoing flights, pop the next destination and recurse.
- Hint 3: After exhausting all outgoing flights from `src`, append `src` to `res`. Return `res[::-1]`.

### 4. Detailed Approach Walkthrough
1. Build sorted adjacency list: `adj = {src: [] for src, dst in tickets}`.
2. Sort `tickets` in reverse alphabetical order: `for src, dst in sorted(tickets, reverse=True): adj[src].append(dst)`.
3. `res = []`.
4. Define `dfs(src)`:
   - While `adj.get(src, [])`:
     - `nxt = adj[src].pop()`
     - `dfs(nxt)`
   - `res.append(src)`
5. `dfs("JFK")`.
6. Return `res[::-1]`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def findItinerary(self, tickets: list[list[str]]) -> list[str]:
        adj = collections.defaultdict(list)
        for src, dst in sorted(tickets, reverse=True):
            adj[src].append(dst)
            
        res = []
        def dfs(src):
            while adj[src]:
                nxt = adj[src].pop()
                dfs(nxt)
            res.append(src)
            
        dfs("JFK")
        return res[::-1]
```

### 6. Complexity Analysis
- **Time Complexity:** `O(E log E) - Due to sorting edges, where E is number of tickets.`
- **Space Complexity:** `O(E) - Adjacency lists and recursion stack.`

---

## <a id="94-min-cost-to-connect-all-points"></a>94. Min Cost to Connect All Points

- **Difficulty:** `Medium`
- **Pattern:** `Minimum Spanning Tree (Prim's Algorithm)`
- **LeetCode Reference:** [LeetCode #1584](https://leetcode.com/problems/min-cost-to-connect-all-points/)

### 1. Problem Statement
You are given an array `points` representing integer coordinates of some points on a 2D-plane, where `points[i] = [xi, yi]`.

The cost of connecting two points `[xi, yi]` and `[xj, yj]` is the **Manhattan distance**: `|xi - xj| + |yi - yj|`.

Return the **minimum cost** to make all points connected.

#### Examples:
**Example 1:**
```text
Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
Output: 20
Explanation: Minimum cost spanning tree connects all 5 points for cost 20.
```

#### Constraints:
- `1 <= points.length <= 1000`
- `-10^6 <= xi, yi <= 10^6`
- `All pairs (xi, yi) are distinct.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Paving roads between towns: start with Town 0 connected. At every step, use a Min-Heap to find the absolute cheapest road connecting any already-paved town to an unpaved town (Prim's MST algorithm).

### 3. Step-by-Step Progressive Hints
- Hint 1: Build an adjacency list of Manhattan distances between all point pairs.
- Hint 2: Use Prim's algorithm with a Min-Heap `minHeap = [[cost, point_index]]`.
- Hint 3: Pop the cheapest edge. If point is unvisited, add cost to `res`, mark visited, and push its unvisited neighbors.

### 4. Detailed Approach Walkthrough
1. `N = len(points)`, `adj = {i: [] for i in range(N)}`.
2. Calculate pairwise Manhattan distances between `i` and `j`.
3. `res = 0, visit = set(), minHeap = [[0, 0]]` (cost 0 to start at node 0).
4. While `len(visit) < N`:
   - `cost, i = heapq.heappop(minHeap)`
   - If `i in visit`: continue
   - `res += cost; visit.add(i)`
   - For `neiCost, nei` in `adj[i]`:
     - If `nei not in visit`:
       - `heapq.heappush(minHeap, [neiCost, nei])`
5. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq

class Solution:
    def minCostConnectPoints(self, points: list[list[int]]) -> int:
        N = len(points)
        adj = {i: [] for i in range(N)}
        for i in range(N):
            x1, y1 = points[i]
            for j in range(i + 1, N):
                x2, y2 = points[j]
                dist = abs(x1 - x2) + abs(y1 - y2)
                adj[i].append([dist, j])
                adj[j].append([dist, i])
                
        res = 0
        visit = set()
        minHeap = [[0, 0]]  # [cost, point]
        
        while len(visit) < N:
            cost, i = heapq.heappop(minHeap)
            if i in visit:
                continue
            res += cost
            visit.add(i)
            for neiCost, nei in adj[i]:
                if nei not in visit:
                    heapq.heappush(minHeap, [neiCost, nei])
                    
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N^2 log N) - N^2 edges pushed and popped from min-heap.`
- **Space Complexity:** `O(N^2) - Pairwise graph representation.`

---

## <a id="95-network-delay-time"></a>95. Network Delay Time

- **Difficulty:** `Medium`
- **Pattern:** `Dijkstra's Shortest Path`
- **LeetCode Reference:** [LeetCode #743](https://leetcode.com/problems/network-delay-time/)

### 1. Problem Statement
You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.

We will send a signal from a given node `k`. Return the **minimum time** it takes for all the `n` nodes to receive the signal. If it is impossible for all the `n` nodes to receive the signal, return `-1`.

#### Examples:
**Example 1:**
```text
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
Explanation: Signal sent from node 2 reaches 1 and 3 in time 1, and reaches 4 in time 2.
```

#### Constraints:
- `1 <= k <= n <= 100`
- `1 <= times.length <= 6000`
- `1 <= ui, vi <= n`
- `0 <= wi <= 100`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> GPS Navigation computing shortest arrival times to all cities simultaneously using Dijkstra's algorithm. The total time for the network is the time taken to reach the farthest city.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use Dijkstra's algorithm with a Min-Heap initialized to `[[0, k]]`.
- Hint 2: Pop `(w1, n1)`. If `n1` already visited, skip. Otherwise record shortest path `t = w1` and mark visited.
- Hint 3: Push neighbors `[w1 + w2, n2]` into heap. If `len(visit) == n`, return `t`; else return `-1`.

### 4. Detailed Approach Walkthrough
1. Build adjacency list `edges = collections.defaultdict(list)` mapping `u -> (v, w)`.
2. `minHeap = [(0, k)]`, `visit = set()`, `t = 0`.
3. While `minHeap`:
   - `w1, n1 = heapq.heappop(minHeap)`
   - If `n1 in visit`: continue
   - `visit.add(n1)`
   - `t = max(t, w1)`
   - For `n2, w2` in `edges[n1]`:
     - If `n2 not in visit`: `heapq.heappush(minHeap, (w1 + w2, n2))`
4. Return `t` if `len(visit) == n` else `-1`.

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq
import collections

class Solution:
    def networkDelayTime(self, times: list[list[int]], n: int, k: int) -> int:
        edges = collections.defaultdict(list)
        for u, v, w in times:
            edges[u].append((v, w))
            
        minHeap = [(0, k)]  # (time, node)
        visit = set()
        t = 0
        
        while minHeap:
            w1, n1 = heapq.heappop(minHeap)
            if n1 in visit:
                continue
            visit.add(n1)
            t = max(t, w1)
            
            for n2, w2 in edges[n1]:
                if n2 not in visit:
                    heapq.heappush(minHeap, (w1 + w2, n2))
                    
        return t if len(visit) == n else -1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(E log V) - Standard Dijkstra complexity.`
- **Space Complexity:** `O(V + E) - Graph representation and heap.`

---

## <a id="96-swim-in-rising-water"></a>96. Swim in Rising Water

- **Difficulty:** `Hard`
- **Pattern:** `Modified Dijkstra (Minimax Path)`
- **LeetCode Reference:** [LeetCode #778](https://leetcode.com/problems/swim-in-rising-water/)

### 1. Problem Statement
You are given an `n x n` integer matrix `grid` where each value `grid[i][j]` represents the elevation at that point `(i, j)`.

The rain starts to fall. At time `t`, the depth of the water everywhere is `t`. You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares is at most `t`.

Return the **least time** until you can reach the bottom right square `(n - 1, n - 1)` if you start at the top left square `(0, 0)`.

#### Examples:
**Example 1:**
```text
Input: grid = [[0,2],[1,3]]
Output: 3
Explanation: At time 3, you can swim from (0,0) through (1,0) to (1,1).
```

**Example 2:**
```text
Input: grid = [[0,1,2,3,4],[24,23,22,21,5],[12,13,14,15,16],[11,17,18,19,20],[10,9,8,7,6]]
Output: 16
Explanation: Shortest time path requires waiting until water level is 16.
```

#### Constraints:
- `n == grid.length == grid[i].length`
- `1 <= n <= 50`
- `0 <= grid[i][j] < n^2`
- `Each value in grid is unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Waiting for floodwaters to submerge mountain passes: the time to traverse any path is dictated by the highest mountain peak along that path (`max(curr_max, next_cell)`). Use Dijkstra's algorithm to explore lowest peak heights first.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use Dijkstra's algorithm with `minHeap = [[grid[0][0], 0, 0]]`.
- Hint 2: Pop `(max_elev, r, c)`. If `(r, c) == (N - 1, N - 1)`, return `max_elev`.
- Hint 3: Push neighbor `(max(max_elev, grid[nr][nc]), nr, nc)`.

### 4. Detailed Approach Walkthrough
1. `N = len(grid)`, `visit = set([(0, 0)])`.
2. `minHeap = [[grid[0][0], 0, 0]]`.
3. While `minHeap`:
   - `max_elev, r, c = heapq.heappop(minHeap)`
   - If `r == N - 1 and c == N - 1`: return `max_elev`
   - For `dr, dc` in `[[0, 1], [0, -1], [1, 0], [-1, 0]]`:
     - `nr, nc = r + dr, c + dc`
     - If `0 <= nr < N and 0 <= nc < N and (nr, nc) not in visit`:
       - `visit.add((nr, nc))`
       - `heapq.heappush(minHeap, [max(max_elev, grid[nr][nc]), nr, nc])`

### 5. Canonical NeetCode Python 3 Solution
```python
import heapq

class Solution:
    def swimInWater(self, grid: list[list[int]]) -> int:
        N = len(grid)
        visit = set()
        minHeap = [[grid[0][0], 0, 0]]  # (time/max_height, r, c)
        directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        
        visit.add((0, 0))
        while minHeap:
            t, r, c = heapq.heappop(minHeap)
            if r == N - 1 and c == N - 1:
                return t
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                if (0 <= nr < N and 0 <= nc < N and (nr, nc) not in visit):
                    visit.add((nr, nc))
                    heapq.heappush(minHeap, [max(t, grid[nr][nc]), nr, nc])
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N^2 log N) - N^2 cells processed in min-heap.`
- **Space Complexity:** `O(N^2) - Visited set and priority queue.`

---

## <a id="97-alien-dictionary"></a>97. Alien Dictionary

- **Difficulty:** `Hard`
- **Pattern:** `Topological Sort on Character Graph`
- **LeetCode Reference:** [LeetCode #269](https://neetcode.io/problems/foreign-dictionary)

### 1. Problem Statement
There is a new alien language that uses the English alphabet. However, the order among letters is unknown to you.

You are given a list of strings `words` from the alien language's dictionary, where the strings are **sorted lexicographically** by the rules of this new language.

Return a string of the unique letters in the new alien language sorted in **lexicographically increasing order** by the new language's rules. If there is no solution, return `""`. If there are multiple solutions, return any of them.

#### Examples:
**Example 1:**
```text
Input: words = ["wrt","wrf","er","ett","rftt"]
Output: "wertf"
Explanation: Lexicographical order deduced from adjacent word prefixes.
```

**Example 2:**
```text
Input: words = ["z","x"]
Output: "zx"
Explanation: 'z' comes before 'x'.
```

**Example 3:**
```text
Input: words = ["z","x","z"]
Output: ""
Explanation: Cycle detected: 'z' < 'x' and 'x' < 'z'.
```

#### Constraints:
- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i] consists of only lowercase English letters.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Deciphering an ancient alphabet: compare adjacent words in the dictionary. The very first differing character between `words[i]` and `words[i+1]` gives a directed order edge `c1 -> c2`. Run Topological Sort to find the alphabet order.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `w1` has `w2` as a prefix and `len(w1) > len(w2)` (e.g. `"abc"` before `"ab"`), it's an invalid dictionary: return `""`.
- Hint 2: Find the first differing character `w1[j] != w2[j]` and add directed edge `adj[w1[j]].add(w2[j])`.
- Hint 3: Run Topological Sort with cycle detection (using `visited` map where True = current path, False = completed).

### 4. Detailed Approach Walkthrough
1. `adj = {c: set() for w in words for c in w}`.
2. For `i` in range(`len(words) - 1`):
   - `w1, w2 = words[i], words[i + 1]`
   - `minLen = min(len(w1), len(w2))`
   - If `len(w1) > len(w2)` and `w1[:minLen] == w2[:minLen]`: return `""`
   - For `j` in range(`minLen`):
     - If `w1[j] != w2[j]`:
       - `adj[w1[j]].add(w2[j])`
       - break
3. `visited = {}`, `res = []`.
4. Define `dfs(c)`:
   - If `c in visited`: return `visited[c]`
   - `visited[c] = True` (in path)
   - For `nei` in `adj[c]`:
     - If `dfs(nei)`: return `True` (cycle detected)
   - `visited[c] = False`
   - `res.append(c)`
5. Run `dfs` on all chars. Return `"".join(res[::-1])`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def foreignDictionary(self, words: list[str]) -> str:
        adj = {c: set() for w in words for c in w}
        
        for i in range(len(words) - 1):
            w1, w2 = words[i], words[i + 1]
            minLen = min(len(w1), len(w2))
            if len(w1) > len(w2) and w1[:minLen] == w2[:minLen]:
                return ""
            for j in range(minLen):
                if w1[j] != w2[j]:
                    adj[w1[j]].add(w2[j])
                    break
                    
        visited = {}  # False = visited, True = in current path
        res = []
        
        def dfs(c):
            if c in visited:
                return visited[c]
            visited[c] = True
            for nei in adj[c]:
                if dfs(nei):
                    return True
            visited[c] = False
            res.append(c)
            
        for c in adj:
            if dfs(c):
                return ""
        return "".join(res[::-1])
```

### 6. Complexity Analysis
- **Time Complexity:** `O(C) - Where C is the total number of characters across all words in the input.`
- **Space Complexity:** `O(U + min(U^2, N)) - Where U is unique characters (<= 26).`

---

## <a id="98-cheapest-flights-within-k-stops"></a>98. Cheapest Flights Within K Stops

- **Difficulty:** `Medium`
- **Pattern:** `Bellman-Ford / BFS Level Relaxation`
- **LeetCode Reference:** [LeetCode #787](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

### 1. Problem Statement
There are `n` cities connected by some number of flights. You are given an array `flights` where `flights[i] = [fromi, toi, pricei]` indicates that there is a flight from city `fromi` to city `toi` with cost `pricei`.

You are also given three integers `src`, `dst`, and `k`, return the **cheapest price** from `src` to `dst` with at most `k` stops. If there is no such route, return `-1`.

#### Examples:
**Example 1:**
```text
Input: n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
Output: 700
Explanation: 0 -> 1 -> 3 with cost 100 + 600 = 700 (1 stop).
```

#### Constraints:
- `1 <= n <= 100`
- `0 <= flights.length <= (n * (n - 1) / 2)`
- `0 <= src, dst, k < n`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Bellman-Ford algorithm with `k + 1` edge relaxations: each iteration relaxes all flight edges using prices from the previous round (copied array) to ensure you do not use more than `k + 1` flights.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use Bellman-Ford algorithm relaxed exactly `k + 1` times.
- Hint 2: In each round, use `tmpPrices = prices.copy()` so that relaxing one edge does not cascade into multiple hops during the same round.

### 4. Detailed Approach Walkthrough
1. Initialize `prices = [float("inf")] * n`, `prices[src] = 0`.
2. Loop `k + 1` times:
   - `tmpPrices = prices.copy()`
   - For `s, d, p` in `flights`:
     - If `prices[s] == float("inf")`: continue
     - If `prices[s] + p < tmpPrices[d]`:
       - `tmpPrices[d] = prices[s] + p`
   - `prices = tmpPrices`
3. Return `prices[dst]` if `prices[dst] != float("inf")` else `-1`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findCheapestPrice(self, n: int, flights: list[list[int]], src: int, dst: int, k: int) -> int:
        prices = [float("inf")] * n
        prices[src] = 0
        
        for i in range(k + 1):
            tmpPrices = prices.copy()
            for s, d, p in flights:
                if prices[s] == float("inf"):
                    continue
                if prices[s] + p < tmpPrices[d]:
                    tmpPrices[d] = prices[s] + p
            prices = tmpPrices
            
        return prices[dst] if prices[dst] != float("inf") else -1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(K * E) - Where K is stops + 1 and E is number of flights.`
- **Space Complexity:** `O(N) - Arrays of size N.`

---
