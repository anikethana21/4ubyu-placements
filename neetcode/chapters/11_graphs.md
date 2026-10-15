# Chapter: Graphs

> Graph algorithms navigate interconnected nodes via Adjacency Lists and Matrix grids using Depth-First Search (DFS), Breadth-First Search (BFS), Topological Sort, and Union-Find.

**Total Questions in Topic:** 13

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 80 | [Number of Islands](#80-number-of-islands) | **Medium** | `Connected Components BFS / DFS` | [#200](https://leetcode.com/problems/number-of-islands/) |
| 81 | [Clone Graph](#81-clone-graph) | **Medium** | `DFS Node Hash Map Cloning` | [#133](https://leetcode.com/problems/clone-graph/) |
| 82 | [Max Area of Island](#82-max-area-of-island) | **Medium** | `Grid DFS Flood Fill Counting` | [#695](https://leetcode.com/problems/max-area-of-island/) |
| 83 | [Pacific Atlantic Water Flow](#83-pacific-atlantic-water-flow) | **Medium** | `Reverse DFS from Ocean Borders` | [#417](https://leetcode.com/problems/pacific-atlantic-water-flow/) |
| 84 | [Surrounded Regions](#84-surrounded-regions) | **Medium** | `Border Flood Fill / Un-capture Marking` | [#130](https://leetcode.com/problems/surrounded-regions/) |
| 85 | [Rotting Oranges](#85-rotting-oranges) | **Medium** | `Multi-Source BFS` | [#994](https://leetcode.com/problems/rotting-oranges/) |
| 86 | [Walls and Gates (Islands and Treasure)](#86-walls-and-gates-islands-and-treasure) | **Medium** | `Multi-Source BFS Distance Propagation` | [#286](https://neetcode.io/problems/islands-and-treasure) |
| 87 | [Course Schedule](#87-course-schedule) | **Medium** | `Topological Sort / Cycle Detection (Kahn's or DFS)` | [#207](https://leetcode.com/problems/course-schedule/) |
| 88 | [Course Schedule II](#88-course-schedule-ii) | **Medium** | `Topological Sort (Postorder DFS)` | [#210](https://leetcode.com/problems/course-schedule-ii/) |
| 89 | [Redundant Connection](#89-redundant-connection) | **Medium** | `Union-Find (Disjoint Set Union)` | [#684](https://leetcode.com/problems/redundant-connection/) |
| 90 | [Number of Connected Components in an Undirected Graph](#90-number-of-connected-components-in-an-undirected-graph) | **Medium** | `Union-Find Component Counting` | [#323](https://neetcode.io/problems/count-connected-components) |
| 91 | [Graph Valid Tree](#91-graph-valid-tree) | **Medium** | `Tree Invariant (Cycle-Free & Fully Connected)` | [#261](https://neetcode.io/problems/valid-tree) |
| 92 | [Word Ladder](#92-word-ladder) | **Hard** | `BFS Shortest Path on Generic Patterns` | [#127](https://leetcode.com/problems/word-ladder/) |

---

## <a id="80-number-of-islands"></a>80. Number of Islands

- **Difficulty:** `Medium`
- **Pattern:** `Connected Components BFS / DFS`
- **LeetCode Reference:** [LeetCode #200](https://leetcode.com/problems/number-of-islands/)

### 1. Problem Statement
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

#### Examples:
**Example 1:**
```text
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
Explanation: All connected 1s form a single contiguous landmass.
```

**Example 2:**
```text
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
Explanation: 3 distinct islands.
```

#### Constraints:
- `m == grid.length, n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j] is '0' or '1'.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Spilling ink on graph paper: each unvisited '1' is the ignition point of a new island. You drop flood fill ink (BFS/DFS) to soak and mark every connected land tile of that entire island before counting the next one.

### 3. Step-by-Step Progressive Hints
- Hint 1: Iterate through every cell `(r, c)` in the grid.
- Hint 2: If `grid[r][c] == "1"` and `(r, c)` not in `visited`, increment `islands += 1` and run BFS/DFS to visit all connected land cells.
- Hint 3: In BFS, use a queue and check 4 directional neighbors: `(r+1,c), (r-1,c), (r,c+1), (r,c-1)`.

### 4. Detailed Approach Walkthrough
1. If `not grid`: return 0.
2. `ROWS, COLS = len(grid), len(grid[0])`, `visited = set()`, `islands = 0`.
3. Helper `bfs(r, c)`:
   - `q = deque([(r, c)])`, `visited.add((r, c))`
   - While `q`:
     - `row, col = q.popleft()`
     - For `dr, dc` in `[(1,0), (-1,0), (0,1), (0,-1)]`:
       - `nr, nc = row + dr, col + dc`
       - If `0 <= nr < ROWS` and `0 <= nc < COLS` and `grid[nr][nc] == "1"` and `(nr, nc)` not in `visited`:
         - `q.append((nr, nc))`
         - `visited.add((nr, nc))`
4. For `r` in range(ROWS), for `c` in range(COLS):
   - If `grid[r][c] == "1"` and `(r, c)` not in `visited`:
     - `bfs(r, c)`
     - `islands += 1`
5. Return `islands`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def numIslands(self, grid: list[list[str]]) -> int:
        if not grid:
            return 0
            
        ROWS, COLS = len(grid), len(grid[0])
        visited = set()
        islands = 0
        
        def bfs(r, c):
            q = collections.deque()
            visited.add((r, c))
            q.append((r, c))
            
            while q:
                row, col = q.popleft()
                directions = [[1, 0], [-1, 0], [0, 1], [0, -1]]
                for dr, dc in directions:
                    nr, nc = row + dr, col + dc
                    if (0 <= nr < ROWS and 0 <= nc < COLS and 
                        grid[nr][nc] == "1" and (nr, nc) not in visited):
                        q.append((nr, nc))
                        visited.add((nr, nc))
                        
        for r in range(ROWS):
            for c in range(COLS):
                if grid[r][c] == "1" and (r, c) not in visited:
                    bfs(r, c)
                    islands += 1
                    
        return islands
```

### 6. Complexity Analysis
- **Time Complexity:** `O(M * N) - Each cell is visited a constant number of times.`
- **Space Complexity:** `O(M * N) - To maintain visited set and BFS queue.`

---

## <a id="81-clone-graph"></a>81. Clone Graph

- **Difficulty:** `Medium`
- **Pattern:** `DFS Node Hash Map Cloning`
- **LeetCode Reference:** [LeetCode #133](https://leetcode.com/problems/clone-graph/)

### 1. Problem Statement
Given a reference of a node in a **connected** undirected graph. Return a **deep copy** (clone) of the graph.

Each node in the graph contains a value (`int`) and a list (`List[Node]`) of its neighbors.

#### Examples:
**Example 1:**
```text
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
Explanation: 4 nodes connected in a cycle, deep copied identically.
```

#### Constraints:
- `The number of nodes in the graph is in the range [0, 100].`
- `1 <= Node.val <= 100`
- `Node.val is unique for each node.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Creating exact duplicate wax replicas of historical figures connected in a social network. Keep a logbook `old_node -> clone_node`. If you meet someone whose clone has already been sculpted, connect the wax hands without re-sculpting.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use a hash map `oldToNew = {}` mapping original nodes to their cloned copies.
- Hint 2: If a node is already in `oldToNew`, return its clone `oldToNew[node]` immediately.
- Hint 3: Otherwise, create `copy = Node(node.val)`, store in `oldToNew[node] = copy`, and populate `copy.neighbors` recursively.

### 4. Detailed Approach Walkthrough
1. Initialize `oldToNew = {}`.
2. Define `dfs(node)`:
   - If `node in oldToNew`: return `oldToNew[node]`
   - `copy = Node(node.val)`
   - `oldToNew[node] = copy`
   - For `nei` in `node.neighbors`:
     - `copy.neighbors.append(dfs(nei))`
   - Return `copy`
3. Return `dfs(node)` if `node` else `None`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        oldToNew = {}
        
        def dfs(node):
            if node in oldToNew:
                return oldToNew[node]
                
            copy = Node(node.val)
            oldToNew[node] = copy
            for nei in node.neighbors:
                copy.neighbors.append(dfs(nei))
            return copy
            
        return dfs(node) if node else None
```

### 6. Complexity Analysis
- **Time Complexity:** `O(V + E) - Where V is vertices and E is edges.`
- **Space Complexity:** `O(V) - Hash map storing clones and recursion stack.`

---

## <a id="82-max-area-of-island"></a>82. Max Area of Island

- **Difficulty:** `Medium`
- **Pattern:** `Grid DFS Flood Fill Counting`
- **LeetCode Reference:** [LeetCode #695](https://leetcode.com/problems/max-area-of-island/)

### 1. Problem Statement
You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected **4-directionally** (horizontal or vertical).

The **area** of an island is the number of cells with a value `1` in the island.

Return the **maximum area** of an island in `grid`. If there is no island, return `0`.

#### Examples:
**Example 1:**
```text
Input: grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output: 6
Explanation: The largest island has area 6.
```

#### Constraints:
- `m == grid.length, n == grid[i].length`
- `1 <= m, n <= 50`
- `grid[i][j] is either 0 or 1.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Counting land area of disconnected archipelagos: at each cell, recursive DFS returns `1 + sum(dfs(neighbors))` while marking visited land cells.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use DFS to compute the area of each connected component of 1s.
- Hint 2: When visiting cell `(r, c)`, mark it visited, return `1 + dfs(up) + dfs(down) + dfs(left) + dfs(right)`.

### 4. Detailed Approach Walkthrough
1. `ROWS, COLS = len(grid), len(grid[0])`, `visit = set()`, `area = 0`.
2. Define `dfs(r, c)`:
   - If `r < 0 or r >= ROWS or c < 0 or c >= COLS or grid[r][c] == 0 or (r, c) in visit`: return 0
   - `visit.add((r, c))`
   - Return `1 + dfs(r + 1, c) + dfs(r - 1, c) + dfs(r, c + 1) + dfs(r, c - 1)`
3. For `r` in range(ROWS), for `c` in range(COLS):
   - `area = max(area, dfs(r, c))`
4. Return `area`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def maxAreaOfIsland(self, grid: list[list[int]]) -> int:
        ROWS, COLS = len(grid), len(grid[0])
        visit = set()
        
        def dfs(r, c):
            if (r < 0 or r == ROWS or 
                c < 0 or c == COLS or 
                grid[r][c] == 0 or (r, c) in visit):
                return 0
                
            visit.add((r, c))
            return (1 + dfs(r + 1, c) +
                        dfs(r - 1, c) +
                        dfs(r, c + 1) +
                        dfs(r, c - 1))
                        
        area = 0
        for r in range(ROWS):
            for c in range(COLS):
                area = max(area, dfs(r, c))
        return area
```

### 6. Complexity Analysis
- **Time Complexity:** `O(ROWS * COLS) - Each cell visited once.`
- **Space Complexity:** `O(ROWS * COLS) - Visited set and DFS stack.`

---

## <a id="83-pacific-atlantic-water-flow"></a>83. Pacific Atlantic Water Flow

- **Difficulty:** `Medium`
- **Pattern:** `Reverse DFS from Ocean Borders`
- **LeetCode Reference:** [LeetCode #417](https://leetcode.com/problems/pacific-atlantic-water-flow/)

### 1. Problem Statement
There is an `m x n` rectangular island that borders both the **Pacific Ocean** and **Atlantic Ocean**. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

Water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is **less than or equal to** the current cell's height. Water can flow into an ocean from any cell adjacent to that ocean.

Return a 2D list of grid coordinates `result` where `result[i] = [ri, ci]` denotes that rain water can flow from cell `(ri, ci)` to **both** the Pacific and Atlantic oceans.

#### Examples:
**Example 1:**
```text
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
Explanation: Cells whose rainwater can flow to both Pacific and Atlantic oceans.
```

#### Constraints:
- `m == heights.length, n == heights[r].length`
- `1 <= m, n <= 200`
- `0 <= heights[r][c] <= 10^5`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Instead of checking every single inland mountain to see if water flows down to both oceans (causing massive redundant work), reverse the direction: imagine ocean water rising uphill from the Pacific border into `pac` set, and rising uphill from Atlantic border into `atl` set. The intersection `pac & atl` are the cells connected to both.

### 3. Step-by-Step Progressive Hints
- Hint 1: Start DFS from the borders of both oceans and flow 'uphill' (`heights[neighbor] >= heights[current]`).
- Hint 2: Maintain `pac = set()` and `atl = set()`.
- Hint 3: Return all `[r, c]` where `(r, c) in pac and (r, c) in atl`.

### 4. Detailed Approach Walkthrough
1. `ROWS, COLS = len(heights), len(heights[0])`.
2. `pac, atl = set(), set()`.
3. Define `dfs(r, c, visit, prevHeight)`:
   - If `(r, c) in visit` or out of bounds or `heights[r][c] < prevHeight`: return
   - `visit.add((r, c))`
   - Recurse in 4 directions with `prevHeight = heights[r][c]`.
4. Call `dfs` along top/bottom rows and left/right columns.
5. Return `list(pac & atl)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def pacificAtlantic(self, heights: list[list[int]]) -> list[list[int]]:
        ROWS, COLS = len(heights), len(heights[0])
        pac, atl = set(), set()
        
        def dfs(r, c, visit, prevHeight):
            if ((r, c) in visit or 
                r < 0 or c < 0 or r == ROWS or c == COLS or 
                heights[r][c] < prevHeight):
                return
                
            visit.add((r, c))
            dfs(r + 1, c, visit, heights[r][c])
            dfs(r - 1, c, visit, heights[r][c])
            dfs(r, c + 1, visit, heights[r][c])
            dfs(r, c - 1, visit, heights[r][c])
            
        for c in range(COLS):
            dfs(0, c, pac, heights[0][c])
            dfs(ROWS - 1, c, atl, heights[ROWS - 1][c])
            
        for r in range(ROWS):
            dfs(r, 0, pac, heights[r][0])
            dfs(r, COLS - 1, atl, heights[r][COLS - 1])
            
        res = []
        for r in range(ROWS):
            for c in range(COLS):
                if (r, c) in pac and (r, c) in atl:
                    res.append([r, c])
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(M * N) - Each cell is visited at most twice.`
- **Space Complexity:** `O(M * N) - For storing coordinates in hash sets.`

---

## <a id="84-surrounded-regions"></a>84. Surrounded Regions

- **Difficulty:** `Medium`
- **Pattern:** `Border Flood Fill / Un-capture Marking`
- **LeetCode Reference:** [LeetCode #130](https://leetcode.com/problems/surrounded-regions/)

### 1. Problem Statement
Given an `m x n` matrix `board` containing `'X'` and `'O'`, **capture all regions** that are 4-directionally surrounded by `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

#### Examples:
**Example 1:**
```text
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: All interior 'O's are captured. The 'O' at (3, 1) touches the border so it cannot be captured.
```

#### Constraints:
- `m == board.length, n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j] is 'X' or 'O'.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Rescuing troops on a perimeter: any `'O'` that connects directly or indirectly to the outer boundary walls is immune from being captured. Mark immune border `'O'`s as `'T'` (temporary safe), flip all remaining surrounded interior `'O'`s to `'X'`, then restore `'T'` back to `'O'`.

### 3. Step-by-Step Progressive Hints
- Hint 1: Any 'O' on the border and any 'O' connected to it CANNOT be captured.
- Hint 2: Step 1: Run DFS from all border 'O's, marking them temporarily as 'T'.
- Hint 3: Step 2: Iterate over the entire board: turn remaining 'O' into 'X', and turn 'T' back into 'O'.

### 4. Detailed Approach Walkthrough
1. `ROWS, COLS = len(board), len(board[0])`.
2. Define `capture(r, c)`: if out of bounds or `board[r][c] != "O"`: return. Set `board[r][c] = "T"`. Recurse 4 directions.
3. Run `capture` on all border cells `(r, c)` where `board[r][c] == "O"`.
4. Traverse entire board:
   - If `board[r][c] == "O"`: `board[r][c] = "X"` (captured)
   - If `board[r][c] == "T"`: `board[r][c] = "O"` (restored safe)

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def solve(self, board: list[list[str]]) -> None:
        ROWS, COLS = len(board), len(board[0])
        
        def capture(r, c):
            if (r < 0 or c < 0 or r == ROWS or c == COLS or board[r][c] != "O"):
                return
            board[r][c] = "T"
            capture(r + 1, c)
            capture(r - 1, c)
            capture(r, c + 1)
            capture(r, c - 1)
            
        # 1. (DFS) Capture unsurrounded regions (border O's -> T)
        for r in range(ROWS):
            for c in range(COLS):
                if (board[r][c] == "O" and (r in [0, ROWS - 1] or c in [0, COLS - 1])):
                    capture(r, c)
                    
        # 2. Capture surrounded regions (O -> X, T -> O)
        for r in range(ROWS):
            for c in range(COLS):
                if board[r][c] == "O":
                    board[r][c] = "X"
                elif board[r][c] == "T":
                    board[r][c] = "O"
```

### 6. Complexity Analysis
- **Time Complexity:** `O(ROWS * COLS) - Linear grid passes.`
- **Space Complexity:** `O(ROWS * COLS) - DFS stack depth.`

---

## <a id="85-rotting-oranges"></a>85. Rotting Oranges

- **Difficulty:** `Medium`
- **Pattern:** `Multi-Source BFS`
- **LeetCode Reference:** [LeetCode #994](https://leetcode.com/problems/rotting-oranges/)

### 1. Problem Statement
You are given an `m x n` grid where each cell can have one of three values:
- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return the **minimum number of minutes** that must elapse until no cell has a fresh orange. If this is impossible, return `-1`.

#### Examples:
**Example 1:**
```text
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
Explanation: Rot spreads simultaneously from rotten oranges in 4 minutes.
```

**Example 2:**
```text
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation: Orange at bottom-left corner can never rot.
```

#### Constraints:
- `m == grid.length, n == grid[i].length`
- `1 <= m, n <= 10`
- `grid[i][j] is 0, 1, or 2.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Multi-origin fire spreading across dry grass: all fires ignite at Minute 0 and spread outwards level-by-level simultaneously in concentric BFS waves.

### 3. Step-by-Step Progressive Hints
- Hint 1: Count initial `fresh` oranges and push all rotten oranges `(r, c)` into a queue `q`.
- Hint 2: Use Multi-Source BFS. At each minute step, pop all current rotten oranges, rot their fresh 4-directional neighbors, decrement `fresh`, and enqueue new rotten oranges.
- Hint 3: Return `time` if `fresh == 0` else `-1`.

### 4. Detailed Approach Walkthrough
1. `q = collections.deque()`, `time, fresh = 0, 0`.
2. Count `fresh` and enqueue all `(r, c)` where `grid[r][c] == 2`.
3. While `q` and `fresh > 0`:
   - For `_` in range(`len(q)`):
     - `r, c = q.popleft()`
     - For `dr, dc` in `[[0, 1], [0, -1], [1, 0], [-1, 0]]`:
       - `row, col = r + dr, c + dc`
       - If `0 <= row < ROWS and 0 <= col < COLS and grid[row][col] == 1`:
         - `grid[row][col] = 2`
         - `q.append((row, col))`
         - `fresh -= 1`
   - `time += 1`
4. Return `time` if `fresh == 0` else `-1`.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def orangesRotting(self, grid: list[list[int]]) -> int:
        q = collections.deque()
        time, fresh = 0, 0
        ROWS, COLS = len(grid), len(grid[0])
        
        for r in range(ROWS):
            for c in range(COLS):
                if grid[r][c] == 1:
                    fresh += 1
                if grid[r][c] == 2:
                    q.append((r, c))
                    
        directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        while q and fresh > 0:
            for i in range(len(q)):
                r, c = q.popleft()
                for dr, dc in directions:
                    row, col = r + dr, c + dc
                    if (0 <= row < ROWS and 0 <= col < COLS and grid[row][col] == 1):
                        grid[row][col] = 2
                        q.append((row, col))
                        fresh -= 1
            time += 1
            
        return time if fresh == 0 else -1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(M * N) - Every cell is processed at most once.`
- **Space Complexity:** `O(M * N) - Queue stores at most M * N cells.`

---

## <a id="86-walls-and-gates-islands-and-treasure"></a>86. Walls and Gates (Islands and Treasure)

- **Difficulty:** `Medium`
- **Pattern:** `Multi-Source BFS Distance Propagation`
- **LeetCode Reference:** [LeetCode #286](https://neetcode.io/problems/islands-and-treasure)

### 1. Problem Statement
You are given an `m x n` grid `grid` initialized with these possible values:
- `-1` - A water cell / obstacle that can not be traversed.
- `0` - A treasure chest / gate.
- `INF` (`2147483647`) - An empty land cell.

Fill each empty land cell with the distance to its **nearest treasure chest**. If it is impossible to reach a treasure chest, it should be filled with `INF`.

#### Examples:
**Example 1:**
```text
Input: grid = [
  [2147483647,-1,0,2147483647],
  [2147483647,2147483647,2147483647,-1],
  [2147483647,-1,2147483647,-1],
  [0,-1,2147483647,2147483647]
]
Output: [
  [3,-1,0,1],
  [2,2,1,-1],
  [1,-1,2,-1],
  [0,-1,3,4]
]
Explanation: Grid filled with shortest distance steps to nearest gate (0).
```

#### Constraints:
- `m == grid.length, n == grid[i].length`
- `1 <= m, n <= 250`
- `grid[i][j] is -1, 0, or 2147483647.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Starting broadcast signals from all radio towers (gates / value 0) simultaneously: at Distance 1, all adjacent empty rooms are filled with 1; at Distance 2, their adjacent empty rooms are filled with 2, guaranteeing shortest path distances.

### 3. Step-by-Step Progressive Hints
- Hint 1: Enqueue all gates `(r, c)` where `grid[r][c] == 0` into a BFS queue.
- Hint 2: For each popped cell, check 4 neighbors. If neighbor is `INF`, update `grid[nr][nc] = grid[r][c] + 1` and enqueue.

### 4. Detailed Approach Walkthrough
1. `ROWS, COLS = len(grid), len(grid[0])`, `visit = set()`, `q = deque()`.
2. For `r` in range(ROWS), for `c` in range(COLS):
   - If `grid[r][c] == 0`: `q.append((r, c))`, `visit.add((r, c))`
3. `dist = 0`.
4. While `q`:
   - For `_` in range(`len(q)`):
     - `r, c = q.popleft()`
     - `grid[r][c] = dist`
     - For `dr, dc` in `[[1,0], [-1,0], [0,1], [0,-1]]`:
       - `nr, nc = r + dr, c + dc`
       - If `0 <= nr < ROWS and 0 <= nc < COLS and (nr, nc) not in visit and grid[nr][nc] != -1`:
         - `visit.add((nr, nc))`
         - `q.append((nr, nc))`
   - `dist += 1`

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def islandsAndTreasure(self, grid: list[list[int]]) -> None:
        ROWS, COLS = len(grid), len(grid[0])
        visit = set()
        q = collections.deque()
        
        for r in range(ROWS):
            for c in range(COLS):
                if grid[r][c] == 0:
                    q.append((r, c))
                    visit.add((r, c))
                    
        dist = 0
        while q:
            for i in range(len(q)):
                r, c = q.popleft()
                grid[r][c] = dist
                for dr, dc in [[1, 0], [-1, 0], [0, 1], [0, -1]]:
                    nr, nc = r + dr, c + dc
                    if (0 <= nr < ROWS and 0 <= nc < COLS and 
                        (nr, nc) not in visit and grid[nr][nc] != -1):
                        visit.add((nr, nc))
                        q.append((nr, nc))
            dist += 1
```

### 6. Complexity Analysis
- **Time Complexity:** `O(M * N) - Each cell is visited at most once.`
- **Space Complexity:** `O(M * N) - For BFS queue and visited set.`

---

## <a id="87-course-schedule"></a>87. Course Schedule

- **Difficulty:** `Medium`
- **Pattern:** `Topological Sort / Cycle Detection (Kahn's or DFS)`
- **LeetCode Reference:** [LeetCode #207](https://leetcode.com/problems/course-schedule/)

### 1. Problem Statement
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [a_i, b_i]` indicates that you **must** take course `b_i` first if you want to take course `a_i`.

Return `true` if you can finish all courses. Otherwise, return `false`.

#### Examples:
**Example 1:**
```text
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: Take course 0 first, then take course 1.
```

**Example 2:**
```text
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: Circular dependency: course 1 needs 0 and course 0 needs 1.
```

#### Constraints:
- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `All prerequisite pairs are unique.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> University degree prerequisite map: if Course A requires Course B, Course B requires Course C, and Course C requires Course A, a circular dependency cycle traps you, making graduation impossible.

### 3. Step-by-Step Progressive Hints
- Hint 1: Build an adjacency list mapping `crs -> list of prerequisites`.
- Hint 2: Use DFS with a `visiting` set (detecting cycles in current path) and a `visited` set (completed valid branches).
- Hint 3: If `crs in visiting`, a cycle exists (return False). If `preMap[crs] == []`, return True.

### 4. Detailed Approach Walkthrough
1. Build `preMap = {i: [] for i in range(numCourses)}`.
2. Populate prerequisites: `preMap[crs].append(pre)`.
3. `visiting = set()` (tracks nodes in current DFS branch).
4. Define `dfs(crs)`:
   - If `crs in visiting`: return `False` (cycle detected)
   - If `preMap[crs] == []`: return `True` (already verified)
   - `visiting.add(crs)`
   - For `pre` in `preMap[crs]`:
     - If not `dfs(pre)`: return `False`
   - `visiting.remove(crs)`
   - `preMap[crs] = []` (memoize completion)
   - Return `True`
5. For `c` in range(numCourses): if not `dfs(c)`: return `False`.
6. Return `True`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: list[list[int]]) -> bool:
        preMap = {i: [] for i in range(numCourses)}
        for crs, pre in prerequisites:
            preMap[crs].append(pre)
            
        visiting = set()
        
        def dfs(crs):
            if crs in visiting:
                return False
            if preMap[crs] == []:
                return True
                
            visiting.add(crs)
            for pre in preMap[crs]:
                if not dfs(pre):
                    return False
            visiting.remove(crs)
            preMap[crs] = []
            return True
            
        for crs in range(numCourses):
            if not dfs(crs):
                return False
        return True
```

### 6. Complexity Analysis
- **Time Complexity:** `O(V + E) - Where V is numCourses and E is prerequisites.`
- **Space Complexity:** `O(V + E) - Adjacency map and recursion stack.`

---

## <a id="88-course-schedule-ii"></a>88. Course Schedule II

- **Difficulty:** `Medium`
- **Pattern:** `Topological Sort (Postorder DFS)`
- **LeetCode Reference:** [LeetCode #210](https://leetcode.com/problems/course-schedule-ii/)

### 1. Problem Statement
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`.

Return the **ordering of courses** you should take to finish all courses. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return an **empty array**.

#### Examples:
**Example 1:**
```text
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
Explanation: Valid course order: 0 -> 1 -> 2 -> 3 or 0 -> 2 -> 1 -> 3.
```

#### Constraints:
- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= numCourses * (numCourses - 1)`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Building a valid course schedule: after taking all prerequisite classes for Course X, Course X can be finalized and added to your graduation transcript (`output.append(crs)`).

### 3. Step-by-Step Progressive Hints
- Hint 1: Use three states per node: unvisited, visiting (in current recursion path), and visited (fully explored).
- Hint 2: When a course and all its prerequisites are completed without cycles, append it to `output`.

### 4. Detailed Approach Walkthrough
1. Build `prereq = {c: [] for c in range(numCourses)}`.
2. `output = []`, `visit = set()`, `cycle = set()`.
3. Define `dfs(crs)`:
   - If `crs in cycle`: return `False`
   - If `crs in visit`: return `True`
   - `cycle.add(crs)`
   - For `pre` in `prereq[crs]`:
     - If not `dfs(pre)`: return `False`
   - `cycle.remove(crs)`
   - `visit.add(crs)`
   - `output.append(crs)`
   - Return `True`
4. For `c` in range(numCourses): if not `dfs(c)`: return `[]`.
5. Return `output`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: list[list[int]]) -> list[int]:
        prereq = {c: [] for c in range(numCourses)}
        for crs, pre in prerequisites:
            prereq[crs].append(pre)
            
        output = []
        visit, cycle = set(), set()
        
        def dfs(crs):
            if crs in cycle:
                return False
            if crs in visit:
                return True
                
            cycle.add(crs)
            for pre in prereq[crs]:
                if not dfs(pre):
                    return False
            cycle.remove(crs)
            visit.add(crs)
            output.append(crs)
            return True
            
        for c in range(numCourses):
            if not dfs(c):
                return []
        return output
```

### 6. Complexity Analysis
- **Time Complexity:** `O(V + E) - Topological sort visiting all nodes and edges once.`
- **Space Complexity:** `O(V + E) - Adjacency map and output array.`

---

## <a id="89-redundant-connection"></a>89. Redundant Connection

- **Difficulty:** `Medium`
- **Pattern:** `Union-Find (Disjoint Set Union)`
- **LeetCode Reference:** [LeetCode #684](https://leetcode.com/problems/redundant-connection/)

### 1. Problem Statement
In this problem, a tree is an **undirected graph** that is connected and has no cycles.

You are given a graph that started as a tree with `n` nodes labeled from `1` to `n`, with one additional edge added. The added edge has two different vertices chosen from `1` to `n`, and was not an edge that already existed.

Return an edge that can be removed so that the resulting graph is a tree of `n` nodes. If there are multiple answers, return the answer that occurs last in the input.

#### Examples:
**Example 1:**
```text
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
Explanation: Edge [2, 3] creates a cycle.
```

**Example 2:**
```text
Input: edges = [[1,2],[2,3],[3,4],[1,4],[1,5]]
Output: [1,4]
Explanation: Edge [1, 4] creates a cycle.
```

#### Constraints:
- `n == edges.length`
- `3 <= n <= 1000`
- `edges[i].length == 2`
- `1 <= ui < vi <= n`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Building a road network between isolated cities: every time you construct a new road between City A and City B, you check if they are already connected in the same road network (`find(A) == find(B)`). If they already belong to the same component, this new road is redundant and creates a loop.

### 3. Step-by-Step Progressive Hints
- Hint 1: Use Union-Find with path compression and union by rank.
- Hint 2: For each edge `[u, v]`, if `union(u, v)` returns False (meaning `u` and `v` already share the same parent root), return `[u, v]` immediately.

### 4. Detailed Approach Walkthrough
1. Initialize `parent = [i for i in range(len(edges) + 1)]`, `rank = [1] * (len(edges) + 1)`.
2. Helper `find(n)`: recursively find root parent with path compression `parent[n] = find(parent[n])`.
3. Helper `union(n1, n2)`:
   - `p1, p2 = find(n1), find(n2)`
   - If `p1 == p2`: return `False` (already connected)
   - Union by rank: attach smaller tree to larger tree
   - Return `True`
4. For `n1, n2` in `edges`:
   - If not `union(n1, n2)`: return `[n1, n2]`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def findRedundantConnection(self, edges: list[list[int]]) -> list[int]:
        parent = [i for i in range(len(edges) + 1)]
        rank = [1] * (len(edges) + 1)
        
        def find(n):
            p = parent[n]
            while p != parent[p]:
                parent[p] = parent[parent[p]]  # Path compression
                p = parent[p]
            return p
            
        def union(n1, n2):
            p1, p2 = find(n1), find(n2)
            if p1 == p2:
                return False
                
            if rank[p1] > rank[p2]:
                parent[p2] = p1
                rank[p1] += rank[p2]
            else:
                parent[p1] = p2
                rank[p2] += rank[p1]
            return True
            
        for n1, n2 in edges:
            if not union(n1, n2):
                return [n1, n2]
        return []
```

### 6. Complexity Analysis
- **Time Complexity:** `O(N * α(N)) ≈ O(N) - Nearly linear time using Disjoint Set Union.`
- **Space Complexity:** `O(N) - Parent and rank arrays.`

---

## <a id="90-number-of-connected-components-in-an-undirected-graph"></a>90. Number of Connected Components in an Undirected Graph

- **Difficulty:** `Medium`
- **Pattern:** `Union-Find Component Counting`
- **LeetCode Reference:** [LeetCode #323](https://neetcode.io/problems/count-connected-components)

### 1. Problem Statement
There is an undirected graph with `n` nodes. You are given an integer `n` and an array `edges` where `edges[i] = [ai, bi]` indicates that there is an edge between `ai` and `bi` in the graph.

Return the **total number of connected components** in the graph.

#### Examples:
**Example 1:**
```text
Input: n = 5, edges = [[0,1],[1,2],[3,4]]
Output: 2
Explanation: Components: {0, 1, 2} and {3, 4}.
```

**Example 2:**
```text
Input: n = 5, edges = [[0,1],[1,2],[2,3],[3,4]]
Output: 1
Explanation: Single connected component containing all 5 nodes.
```

#### Constraints:
- `1 <= n <= 2000`
- `1 <= edges.length <= 5000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Starting with `n` isolated islands: every time a bridge successfully merges two previously disconnected islands, the total count of distinct island clusters decreases by 1 (`res -= 1`).

### 3. Step-by-Step Progressive Hints
- Hint 1: Start with `res = n` isolated components.
- Hint 2: For each edge `[u, v]`, if `union(u, v)` successfully merges two different components, decrement `res -= 1`.

### 4. Detailed Approach Walkthrough
1. Initialize `parent = [i for i in range(n)]`, `rank = [1] * n`, `res = n`.
2. In `union(n1, n2)`:
   - `p1, p2 = find(n1), find(n2)`
   - If `p1 == p2`: return 0
   - Merge roots, update rank, return 1.
3. For `n1, n2` in `edges`:
   - `res -= union(n1, n2)`
4. Return `res`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def countComponents(self, n: int, edges: list[list[int]]) -> int:
        parent = [i for i in range(n)]
        rank = [1] * n
        
        def find(n1):
            res = n1
            while res != parent[res]:
                parent[res] = parent[parent[res]]
                res = parent[res]
            return res
            
        def union(n1, n2):
            p1, p2 = find(n1), find(n2)
            if p1 == p2:
                return 0
            if rank[p2] > rank[p1]:
                parent[p1] = p2
                rank[p2] += rank[p1]
            else:
                parent[p2] = p1
                rank[p1] += rank[p2]
            return 1
            
        res = n
        for n1, n2 in edges:
            res -= union(n1, n2)
        return res
```

### 6. Complexity Analysis
- **Time Complexity:** `O(V + E * α(V)) ≈ O(V + E).`
- **Space Complexity:** `O(V) - Parent and rank arrays.`

---

## <a id="91-graph-valid-tree"></a>91. Graph Valid Tree

- **Difficulty:** `Medium`
- **Pattern:** `Tree Invariant (Cycle-Free & Fully Connected)`
- **LeetCode Reference:** [LeetCode #261](https://neetcode.io/problems/valid-tree)

### 1. Problem Statement
Given `n` nodes labeled from `0` to `n - 1` and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a **valid tree**.

#### Examples:
**Example 1:**
```text
Input: n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]
Output: true
Explanation: Graph is connected and contains no cycles (4 edges, 5 nodes).
```

**Example 2:**
```text
Input: n = 5, edges = [[0,1],[1,2],[2,3],[1,3],[1,4]]
Output: false
Explanation: Contains cycle [1,2,3].
```

#### Constraints:
- `1 <= n <= 2000`
- `0 <= edges.length <= 5000`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A valid tree of `n` nodes must satisfy two strict criteria: 1) It has NO cycles. 2) All `n` nodes are connected into a single component. (Equivalently, it must have exactly `n - 1` edges without cycles).

### 3. Step-by-Step Progressive Hints
- Hint 1: If `len(edges) != n - 1`, return False immediately.
- Hint 2: Use DFS from node 0 tracking `prev` parent node to avoid trivial undirected backtracking.
- Hint 3: Return `len(visit) == n` and no cycles detected.

### 4. Detailed Approach Walkthrough
1. If `len(edges) != n - 1`: return `False` (quick check for tree edge count).
2. Build adjacency list `adj = {i: [] for i in range(n)}`.
3. `visit = set()`.
4. Define `dfs(i, prev)`:
   - If `i in visit`: return `False` (cycle)
   - `visit.add(i)`
   - For `j` in `adj[i]`:
     - If `j == prev`: continue
     - If not `dfs(j, i)`: return `False`
   - Return `True`
5. Return `dfs(0, -1) and len(visit) == n`.

### 5. Canonical NeetCode Python 3 Solution
```python
class Solution:
    def validTree(self, n: int, edges: list[list[int]]) -> bool:
        if not n:
            return True
        if len(edges) != n - 1:
            return False
            
        adj = {i: [] for i in range(n)}
        for n1, n2 in edges:
            adj[n1].append(n2)
            adj[n2].append(n1)
            
        visit = set()
        
        def dfs(i, prev):
            if i in visit:
                return False
            visit.add(i)
            for j in adj[i]:
                if j == prev:
                    continue
                if not dfs(j, i):
                    return False
            return True
            
        return dfs(0, -1) and len(visit) == n
```

### 6. Complexity Analysis
- **Time Complexity:** `O(V + E) - Linear traversal over graph.`
- **Space Complexity:** `O(V + E) - Adjacency list and visited set.`

---

## <a id="92-word-ladder"></a>92. Word Ladder

- **Difficulty:** `Hard`
- **Pattern:** `BFS Shortest Path on Generic Patterns`
- **LeetCode Reference:** [LeetCode #127](https://leetcode.com/problems/word-ladder/)

### 1. Problem Statement
A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:
- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
- `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return the **number of words** in the **shortest transformation sequence** from `beginWord` to `endWord`, or `0` if no such sequence exists.

#### Examples:
**Example 1:**
```text
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: Shortest transformation: "hit" -> "hot" -> "dot" -> "dog" -> "cog" (5 words).
```

**Example 2:**
```text
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: endWord "cog" is not in wordList.
```

#### Constraints:
- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `beginWord != endWord`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Navigating a word maze where each door changes 1 letter: instead of comparing all word pairs in O(N^2), group words by wildcard patterns (e.g. `"*ot"` matches `"hot"`, `"dot"`, `"lot"`). Then run BFS for the shortest path.

### 3. Step-by-Step Progressive Hints
- Hint 1: If `endWord` not in `wordList`, return 0.
- Hint 2: Create a pattern adjacency map: e.g. for `"hot"`, patterns are `"*ot"`, `"h*t"`, `"ho*"`.
- Hint 3: Run standard BFS starting from `beginWord`. Level count starts at 1 and increments each BFS step.

### 4. Detailed Approach Walkthrough
1. If `endWord not in wordList`: return 0.
2. `nei = collections.defaultdict(list)`.
3. Add `beginWord` to `wordList`.
4. For `word` in `wordList`:
   - For `j` in range(len(word)):
     - `pattern = word[:j] + "*" + word[j+1:]`
     - `nei[pattern].append(word)`
5. `visit = set([beginWord])`, `q = deque([beginWord])`, `res = 1`.
6. While `q`:
   - For `_` in range(len(q)):
     - `word = q.popleft()`
     - If `word == endWord`: return `res`
     - For `j` in range(len(word)):
       - `pattern = word[:j] + "*" + word[j+1:]`
       - For `neiWord` in `nei[pattern]`:
         - If `neiWord not in visit`:
           - `visit.add(neiWord)`
           - `q.append(neiWord)`
   - `res += 1`
7. Return 0.

### 5. Canonical NeetCode Python 3 Solution
```python
import collections

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: list[str]) -> int:
        if endWord not in wordList:
            return 0
            
        nei = collections.defaultdict(list)
        wordList.append(beginWord)
        for word in wordList:
            for j in range(len(word)):
                pattern = word[:j] + "*" + word[j + 1:]
                nei[pattern].append(word)
                
        visit = set([beginWord])
        q = collections.deque([beginWord])
        res = 1
        
        while q:
            for i in range(len(q)):
                word = q.popleft()
                if word == endWord:
                    return res
                for j in range(len(word)):
                    pattern = word[:j] + "*" + word[j + 1:]
                    for neiWord in nei[pattern]:
                        if neiWord not in visit:
                            visit.add(neiWord)
                            q.append(neiWord)
            res += 1
        return 0
```

### 6. Complexity Analysis
- **Time Complexity:** `O(M^2 * N) - Where M is word length and N is total words in wordList.`
- **Space Complexity:** `O(M^2 * N) - Pattern dictionary and BFS queue.`

---
