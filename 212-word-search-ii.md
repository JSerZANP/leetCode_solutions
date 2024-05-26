Trie + dfs

```js
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (let char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }
    node.isEnd = true;
  }

  search(word) {
    let node = this.root;
    for (let char of word) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return node.isEnd;
  }
}

var findWords = function (board, words) {
  const result = [];
  const trie = new Trie();

  // Build the trie from words list
  for (let word of words) {
    trie.insert(word);
  }

  const dfs = (node, i, j, path) => {
    if (node.isEnd) {
      result.push(path);
      node.isEnd = false; // Mark as visited to avoid duplicates
    }

    if (i < 0 || i >= board.length || j < 0 || j >= board[0].length) return;

    const char = board[i][j];
    if (!node.children[char]) return;

    board[i][j] = "#"; // Mark current cell as visited

    dfs(node.children[char], i + 1, j, path + char);
    dfs(node.children[char], i - 1, j, path + char);
    dfs(node.children[char], i, j + 1, path + char);
    dfs(node.children[char], i, j - 1, path + char);

    board[i][j] = char; // Backtrack
  };

  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[0].length; j++) {
      dfs(trie.root, i, j, "");
    }
  }

  return result;
};
```

Another try in 2024

```js
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (let char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }
    node.isEnd = true;
  }

  search(word) {
    let node = this.root;
    for (let char of word) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return node.isEnd;
  }
}

// N*N, M words on length K
var findWords = function (board, words) {
  // different from problem 57
  // there are multiple words
  // but the basic idea is the same
  // we can tweak it into
  // we try to match all the words at index i
  // for example, we start from t, we search all the words which starts with t
  // then we try to match a, search all words whose 2nd word is a
  // so we actually need to do a prefix search
  // by calculating a Trie tree for all the words

  // O(KM) O(KM)
  const trie = new Trie();
  for (const word of words) {
    trie.insert(word);
  }

  const rows = board.length;
  if (rows === 0) return false;
  const cols = board[0].length;
  if (cols === 0) return false;

  const result = new Set();
  // just search all possible positions
  // keep a cursor of the letters in word
  let nextTrieNode = trie.root;

  // O(k)
  const visited = new Array(rows)
    .fill(0)
    .map((_) => new Array(cols).fill(false));

  let prefix = [];

  // O(3^k * N^2)
  // O(4*3^(K - 1) * N^2) might be better?
  const tryMatch = (i, j) => {
    if (nextTrieNode == null) {
      return;
    }
    if (i < 0 || i >= rows || j < 0 || j >= cols) {
      return;
    }
    if (visited[i][j]) {
      return;
    }
    // console.log(i, j, board[i][j], Object.keys(nextTrieNode.children))

    if (!(board[i][j] in nextTrieNode.children)) {
      // console.log('not in the children, return')
      return;
    }

    // matched
    visited[i][j] = true;
    prefix.push(board[i][j]);

    const prevNode = nextTrieNode;
    nextTrieNode = nextTrieNode.children[board[i][j]];

    if (nextTrieNode.isEnd) {
      result.add(prefix.join(""));
    }

    tryMatch(i + 1, j);
    tryMatch(i - 1, j);
    tryMatch(i, j + 1);
    tryMatch(i, j - 1);

    nextTrieNode = prevNode;
    visited[i][j] = false;
    prefix.pop();
  };

  // O(N^2)
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      tryMatch(i, j);
    }
  }
  return [...result];
};
```
