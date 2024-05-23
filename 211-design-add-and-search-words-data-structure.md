Here is me explaining this on youtube: https://youtu.be/rl2zOKcDWLQ

```js
/**
 * Initialize your data structure here.
 */
// trie?
/**
        root
    a            b
  b   p         a  u
  o    p        g   s
         l           s
        e  i          $
             c
               a
                 t
                 */

class Node {
  constructor(char) {
    this.char = char;
    this.next = new Map(); // Map<string, Node>
  }
}

var WordDictionary = function () {
  this.root = new Node("^");
};

/**
 * Adds a word into the data structure.
 * @param {string} word
 * @return {void}
 */
WordDictionary.prototype.addWord = function (word) {
  let layer = this.root.next;
  for (let i = 0; i < word.length; i++) {
    const char = word[i];

    if (!layer.has(char)) {
      layer.set(char, new Node(char));
    }
    layer = layer.get(char).next;
  }

  layer.set("$", 1);
};

/**
 * Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
 * @param {string} word
 * @return {boolean}
 */
WordDictionary.prototype.search = function (word) {
  // BFS
  const queue = [this.root.next]; // Array<Map<string, Node>>

  for (let i = 0; i < word.length; i++) {
    const char = word[i];
    queue.push(null);
    let head;
    while ((head = queue.shift())) {
      if (char === ".") {
        for (let [key, node] of head) {
          if (key !== "$") {
            queue.push(node.next);
          }
        }
      } else {
        if (head.has(char)) {
          queue.push(head.get(char).next);
        }
      }
    }

    if (queue.length === 0) {
      break;
    }
  }

  if (queue.length > 0) {
    for (let nextMap of queue) {
      if (nextMap.has("$")) {
        return true;
      }
    }
  }

  return false;
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * var obj = new WordDictionary()
 * obj.addWord(word)
 * var param_2 = obj.search(word)
 */
```

Another try in 2024

```js
class TrieNode {
  constructor(val) {
    this.val = val;
    this.children = new Map();
  }
}

var WordDictionary = function () {
  this.root = new TrieNode(null);
};

WordDictionary.EOW = Symbol();

/**
 * @param {string} word
 * @return {void}
 */
WordDictionary.prototype.addWord = function (word) {
  let p = this.root;
  for (const char of word) {
    if (!p.children.has(char)) {
      p.children.set(char, new TrieNode(char));
    }
    p = p.children.get(char);
  }
  p.children.set(WordDictionary.EOW, true);
};

/**
 * @param {string} word
 * @return {boolean}
 */
WordDictionary.prototype.search = function (word) {
  return this.searchImpl(word, this.root);
};

WordDictionary.prototype.searchImpl = function (word, start) {
  let p = start;
  for (let i = 0; i < word.length; i++) {
    const char = word[i];
    if (char === ".") {
      // any children will match
      for (const [key, value] of p.children.entries()) {
        if (
          typeof key === "string" &&
          this.searchImpl(word.slice(i + 1), value)
        ) {
          return true;
        }
      }
      return false;
    } else {
      if (!p.children.has(char)) {
        return false;
      }
      p = p.children.get(char);
    }
  }
  return p.children.has(WordDictionary.EOW);
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * var obj = new WordDictionary()
 * obj.addWord(word)
 * var param_2 = obj.search(word)
 */
```
