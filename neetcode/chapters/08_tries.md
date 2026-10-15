# Chapter: Tries

> Tries (Prefix Trees) represent string dictionaries where each node stores character branches, enabling lightning-fast O(L) prefix searches and dictionary lookups.

**Total Questions in Topic:** 3

---

## Quick Index

| # | Problem | Difficulty | Pattern | LeetCode |
|---|---|---|---|---|
| 61 | [Implement Trie (Prefix Tree)](#61-implement-trie-prefix-tree) | **Medium** | `Prefix Tree Node Implementation` | [#208](https://leetcode.com/problems/implement-trie-prefix-tree/) |
| 62 | [Design Add and Search Words Data Structure](#62-design-add-and-search-words-data-structure) | **Medium** | `Trie DFS with Wildcard Matching` | [#211](https://leetcode.com/problems/design-add-and-search-words-data-structure/) |
| 63 | [Word Search II](#63-word-search-ii) | **Hard** | `Trie + 2D Backtracking DFS` | [#212](https://leetcode.com/problems/word-search-ii/) |

---

## <a id="61-implement-trie-prefix-tree"></a>61. Implement Trie (Prefix Tree)

- **Difficulty:** `Medium`
- **Pattern:** `Prefix Tree Node Implementation`
- **LeetCode Reference:** [LeetCode #208](https://leetcode.com/problems/implement-trie-prefix-tree/)

### 1. Problem Statement
A **trie** (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the `Trie` class:
- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string `word` into the trie.
- `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

#### Examples:
**Example 1:**
```text
Input: ["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output: [null, null, true, false, true, null, true]
Explanation: Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
```

#### Constraints:
- `1 <= word.length, prefix.length <= 2000`
- `word and prefix consist only of lowercase English letters.`
- `At most 3 * 10^4 calls in total will be made to insert, search, and startsWith.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A predictive text tree: each node is a letter branch. Trailing down 'a' -> 'p' -> 'p' -> 'l' -> 'e' spells 'apple', and marking the final 'e' node with `endOfWord = True` differentiates full words from mere prefixes.

### 3. Step-by-Step Progressive Hints
- Hint 1: Define `TrieNode` having `children = {}` and `endOfWord = False`.
- Hint 2: In `insert`, traverse/create character nodes and set `curr.endOfWord = True` at the end.
- Hint 3: In `search`, return `curr.endOfWord` after traversing. In `startsWith`, return `True` if all prefix characters exist.

### 4. Detailed Approach Walkthrough
1. Define `TrieNode`: `self.children = {}`, `self.endOfWord = False`.
2. `insert(word)`: For each char `c`, if not in `curr.children`, create `TrieNode()`. Advance `curr = curr.children[c]`. Mark `curr.endOfWord = True`.
3. `search(word)`: Traverse chars; if `c` not in `curr.children`, return `False`. Return `curr.endOfWord`.
4. `startsWith(prefix)`: Traverse chars; if `c` not in `curr.children`, return `False`. Return `True`.

### 5. Canonical NeetCode Python 3 Solution
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.endOfWord = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        curr = self.root
        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
        curr.endOfWord = True

    def search(self, word: str) -> bool:
        curr = self.root
        for c in word:
            if c not in curr.children:
                return False
            curr = curr.children[c]
        return curr.endOfWord

    def startsWith(self, prefix: str) -> bool:
        curr = self.root
        for c in prefix:
            if c not in curr.children:
                return False
            curr = curr.children[c]
        return True
```

### 6. Complexity Analysis
- **Time Complexity:** `O(L) for insert, search, and startsWith (where L is length of word/prefix).`
- **Space Complexity:** `O(N * L) - Where N is number of words and L is average length.`

---

## <a id="62-design-add-and-search-words-data-structure"></a>62. Design Add and Search Words Data Structure

- **Difficulty:** `Medium`
- **Pattern:** `Trie DFS with Wildcard Matching`
- **LeetCode Reference:** [LeetCode #211](https://leetcode.com/problems/design-add-and-search-words-data-structure/)

### 1. Problem Statement
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:
- `WordDictionary()` Initializes the object.
- `void addWord(word)` Adds `word` to the data structure, it can be matched later.
- `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

#### Examples:
**Example 1:**
```text
Input: ["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output: [null,null,null,null,false,true,true,true]
Explanation: WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```

#### Constraints:
- `1 <= word.length <= 25`
- `word in addWord consists of lowercase English letters.`
- `word in search consist of '.' or lowercase English letters.`
- `At most 10^4 calls will be made to addWord and search.`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> A Trie lookup where the `'.'` character acts as a universal wildcard skeleton key: when encountering `'.'`, try searching down EVERY existing branch at that level.

### 3. Step-by-Step Progressive Hints
- Hint 1: Standard Trie insertion for `addWord`.
- Hint 2: For `search(word)`, use a recursive DFS helper `dfs(j, root)`.
- Hint 3: If `word[j] == '.'`, iterate over all children `for child in curr.children.values(): if dfs(j + 1, child): return True`.

### 4. Detailed Approach Walkthrough
1. Define `TrieNode` with `children = {}` and `word = False`.
2. `addWord(word)`: Standard trie insertion.
3. `search(word)`:
   - Define `dfs(j, root)`:
     - `curr = root`
     - For `i` from `j` to `len(word)`:
       - `c = word[i]`
       - If `c == "."`:
         - For `child` in `curr.children.values()`:
           - If `dfs(i + 1, child)`: return `True`
         - Return `False`
       - Else:
         - If `c` not in `curr.children`: return `False`
         - `curr = curr.children[c]`
     - Return `curr.word`
   - Return `dfs(0, self.root)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.word = False

class WordDictionary:
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word: str) -> None:
        curr = self.root
        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
        curr.word = True

    def search(self, word: str) -> bool:
        def dfs(j, root):
            curr = root
            for i in range(j, len(word)):
                c = word[i]
                if c == ".":
                    for child in curr.children.values():
                        if dfs(i + 1, child):
                            return True
                    return False
                else:
                    if c not in curr.children:
                        return False
                    curr = curr.children[c]
            return curr.word
            
        return dfs(0, self.root)
```

### 6. Complexity Analysis
- **Time Complexity:** `addWord: O(M) where M is word length; search: O(M) best case, O(26^M) worst case with multiple wildcards.`
- **Space Complexity:** `O(N * M) - Trie storage.`

---

## <a id="63-word-search-ii"></a>63. Word Search II

- **Difficulty:** `Hard`
- **Pattern:** `Trie + 2D Backtracking DFS`
- **LeetCode Reference:** [LeetCode #212](https://leetcode.com/problems/word-search-ii/)

### 1. Problem Statement
Given an `m x n` `board` of characters and a list of strings `words`, return *all words on the board*.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

#### Examples:
**Example 1:**
```text
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
Explanation: Both 'eat' and 'oath' can be constructed from adjacent board characters.
```

#### Constraints:
- `m == board.length, n == board[i].length`
- `1 <= m, n <= 12`
- `board[i][j] is a lowercase English letter.`
- `1 <= words.length <= 3 * 10^4`
- `1 <= words[i].length <= 10`

### 2. Intuitive Analogy & Mental Model
> 💡 **Mental Model:**
> Instead of running a separate search over the entire Boggle board for every single word in the dictionary (which causes massive duplicate work), load the entire dictionary into a Trie. As you walk across the board, you match all dictionary words simultaneously in a single coordinated exploration.

### 3. Step-by-Step Progressive Hints
- Hint 1: Build a Trie from all strings in `words`.
- Hint 2: Start DFS from every cell `(r, c)`. Only branch into neighbors if `board[r][c]` exists in the current Trie node's children.
- Hint 3: When a word is found, add it to `res`, set `node.isWord = False` (or prune the leaf node) to prevent duplicate output.

### 4. Detailed Approach Walkthrough
1. Insert all `words` into a Trie. Store `node.isWord = True` (or word string) at leaf.
2. Define `dfs(r, c, node, word)`:
   - Boundary check: if out of bounds or `(r, c)` in `visit` or `board[r][c]` not in `node.children`: return
   - Mark `visit.add((r, c))`
   - `node = node.children[board[r][c]]`
   - `word += board[r][c]`
   - If `node.isWord`: `res.add(word); node.isWord = False` (deduplicate)
   - Recurse in 4 directions: `(r+1, c), (r-1, c), (r, c+1), (r, c-1)`
   - Unmark `visit.remove((r, c))`
3. Iterate over all cells `(r, c)` and launch `dfs(r, c, root, "")`.
4. Return `list(res)`.

### 5. Canonical NeetCode Python 3 Solution
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.isWord = False
        
    def addWord(self, word):
        curr = self
        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
        self.isWord = True

class Solution:
    def findWords(self, board: list[list[str]], words: list[str]) -> list[str]:
        root = TrieNode()
        for w in words:
            root.addWord(w)
            
        ROWS, COLS = len(board), len(board[0])
        res, visit = set(), set()
        
        def dfs(r, c, node, word):
            if (r < 0 or c < 0 or 
                r == ROWS or c == COLS or
                (r, c) in visit or 
                board[r][c] not in node.children):
                return
                
            visit.add((r, c))
            node = node.children[board[r][c]]
            word += board[r][c]
            if node.isWord:
                res.add(word)
                node.isWord = False  # Avoid duplicate additions
                
            dfs(r + 1, c, node, word)
            dfs(r - 1, c, node, word)
            dfs(r, c + 1, node, word)
            dfs(r, c - 1, node, word)
            visit.remove((r, c))
            
        for r in range(ROWS):
            for c in range(COLS):
                dfs(r, c, root, "")
                
        return list(res)
```

### 6. Complexity Analysis
- **Time Complexity:** `O(ROWS * COLS * 4 * 3^(L-1)) - Where L is max word length.`
- **Space Complexity:** `O(N * L) - For storing all words in the Trie.`

---
