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
