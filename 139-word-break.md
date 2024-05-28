Me explaining this on youtube:
https://youtu.be/9acEbeVOqQ0

## 1. naive backtracking

```js
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */

// naive backtracking
// N M
// worst case   T(k) = O(1) for K <= 0, T(1) => K
// T(N) = T(N-1) + T(N - 2) + T(N- 3)  + T(N - M)
//      ~ T(N-1) + T(N - 2) + T(1) + c
//      ~ 2T(N - 1)
// O(2 ^ N)
// Space: call stack, worst O(N)
var wordBreak = function (s, wordDict) {
  // return is we could go down to last character from i
  const walk = (i) => {
    if (i > s.length - 1) return true;
    let isMatched = false;
    for (let word of wordDict) {
      const length = word.length;
      if (s.slice(i, i + length) === word) {
        const nextMatched = walk(i + length);
        if (nextMatched) {
          isMatched = true;
          break;
        }
      }
    }

    return isMatched;
  };

  return walk(0);
};
```

## 2. memoization

```js
// Time: O(N ^ 2)
// Space: O(N)
var wordBreak = function (s, wordDict) {
  // return is we could go down to last character from i
  const cache = new Map();

  const walk = (i) => {
    if (cache.has(i)) return cache.get(i);

    if (i > s.length - 1) return true;
    let isMatched = false;
    for (let word of wordDict) {
      const length = word.length;
      if (s.slice(i, i + length) === word) {
        const nextMatched = walk(i + length);
        if (nextMatched) {
          isMatched = true;
          break;
        }
      }
    }

    cache.set(i, isMatched);
    return isMatched;
  };

  return walk(0);
};
```

## 3. DP with searching on wordDict

```js
// Time: O(N * M)
// Space: O(N)
var wordBreak1 = function (s, wordDict) {
  const canMatchAt = [];

  for (let i = 0; i < s.length; i++) {
    let isMatched = false;
    for (let word of wordDict) {
      const length = word.length;
      const prevMatched = i - length < 0 ? true : canMatchAt[i - length];
      if (prevMatched && s.slice(i - length + 1, i + 1) === word) {
        isMatched = true;
        break;
      }
    }

    canMatchAt[i] = isMatched;
  }

  return canMatchAt[s.length - 1];
};
```

## 4. DP based on substring from s

```js
// Time: O(N ^ 2)
// Space: O(N + M)
var wordBreak2 = function (s, wordDict) {
  const canMatchAt = [];
  const dictMap = new Set(wordDict);

  for (let i = 0; i < s.length; i++) {
    let isMatched = false;
    for (let k = i; k >= 0; k--) {
      const word = s.slice(k, i + 1);
      const prevMatched = k - 1 < 0 ? true : canMatchAt[k - 1];

      if (prevMatched && dictMap.has(word)) {
        isMatched = true;
        break;
      }
    }

    canMatchAt[i] = isMatched;
  }

  return canMatchAt[s.length - 1];
};
```

## 5. choose above one based on input

```js
var wordBreak = function (s, wordDict) {
  if (wordDict.length < s.length) {
    return wordBreak1(s, wordDict);
  } else {
    return wordBreak2(s, wordDict);
  }
};
```

## 6. ?

```js
var wordBreak = function (s, wordDict) {
  const canMatchEndAt = new Array(s.length).fill(false);

  for (let i = 0; i < s.length; i++) {
    if (i === 0 || canMatchEndAt[i - 1]) {
      for (let word of wordDict) {
        const wordLen = word.length;
        if (canMatchEndAt[i + wordLen - 1]) continue;

        const subStr = s.slice(i, i + wordLen);
        if (subStr === word) {
          canMatchEndAt[i + wordLen - 1] = true;
        }
      }
    }
  }
  return canMatchEndAt[s.length - 1];
};
```

Another try in 2024, using prefix tree.

Potentially every index we'll check it once. O(N \* N)

```js
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function (s, wordDict) {
  // try at each index
  // try match the word and use recursion
  const trie = new Trie();
  for (const word of wordDict) {
    trie.insert(word);
  }

  const cache = new Map();
  const tryMatch = (i) => {
    if (cache.has(i)) return cache.get(i);
    if (i === s.length) {
      cache.set(i, true);
      return true;
    }
    // check all substrings and check if there is a word in the dict
    // lee
    // l
    /// le
    // lee

    // we actually need a prefix tree
    // for each j, we check if there is a prefix in the dict
    // if it, it is a possible break point, otherwise stop
    let buffer = "";
    let p = trie.root;
    for (let j = i; j < s.length; j++) {
      // check if there is a word in the trie tree
      if (p.children.has(s[j])) {
        p = p.children.get(s[j]);
        // it means p is the end of a wor
        if (p.children.has(Trie.EOW)) {
          if (tryMatch(j + 1)) {
            cache.set(i, true);

            return true;
          }
        }
      } else {
        break;
      }
    }
    cache.set(i, false);
    return false;
  };

  return tryMatch(0);
};

class TrieNode {
  constructor(val) {
    this.val = val;
    /** @type Map<string, TrieNode> */
    this.children = new Map();
  }
}

var Trie = function () {
  this.root = new TrieNode(-1);
};

Trie.EOW = Symbol();

/**
 * @param {string} word
 * @return {void}
 */
Trie.prototype.insert = function (word) {
  // insert a word in the Trie
  // add a ending identifier
  let p = this.root;
  for (const char of word) {
    if (!p.children.has(char)) {
      p.children.set(char, new TrieNode(char));
    }
    p = p.children.get(char);
  }
  // p stops at the node of last char
  p.children.set(Trie.EOW, true);
};

/**
 * @param {string} word
 * @return {boolean}
 */
Trie.prototype.search = function (word) {
  // trverse the characters
  // check EOW
  let p = this.root;
  for (const char of word) {
    if (!p.children.has(char)) {
      return false;
    }
    p = p.children.get(char);
  }
  // p stops at the node of last character
  return p.children.has(Trie.EOW);
};

/**
 * @param {string} prefix
 * @return {boolean}
 */
Trie.prototype.startsWith = function (prefix) {
  // trverse the characters
  // check EOW
  let p = this.root;
  for (const char of prefix) {
    if (!p.children.has(char)) {
      return false;
    }
    p = p.children.get(char);
  }
  // p stops at the node of last character
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
