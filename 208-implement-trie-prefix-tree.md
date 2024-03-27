```js
class TrieNode {
  constructor(val) {
    this.val;
    this.children = new Map(); // // Map<string | symbol, TrieNode | null>
  }
  static EOW = Symbol();
}

var Trie = function () {
  this.head = new TrieNode("");
};

/**
 * @param {string} word
 * @return {void}
 */
Trie.prototype.insert = function (word) {
  // for each letter
  // search the node, or create a new one.
  // add special Symbol() as the ending
  let p = this.head;
  for (const char of word) {
    if (!p.children.has(char)) {
      p.children.set(char, new TrieNode(char));
    }
    p = p.children.get(char);
  }
  // and EOF
  p.children.set(TrieNode.EOW, null);
};

/**
 * @param {string} word
 * @return {boolean}
 */
Trie.prototype.search = function (word) {
  let p = this.head;
  for (const char of word) {
    p = p.children.get(char);
    if (p == null) {
      return false;
    }
  }
  return p.children.has(TrieNode.EOW);
};

/**
 * @param {string} prefix
 * @return {boolean}
 */
Trie.prototype.startsWith = function (prefix) {
  let p = this.head;
  for (const char of prefix) {
    p = p.children.get(char);
    if (p == null) {
      return false;
    }
  }
  return true;
};

/**
 * Your Trie object will be instantiated and called as such:
 * var obj = new Trie()
 * obj.insert(word)
 * var param_2 = obj.search(word)
 * var param_3 = obj.startsWith(prefix)
 */
```
