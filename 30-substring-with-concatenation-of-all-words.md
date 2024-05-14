Youtube video explaining this: https://youtu.be/UV-hD94ytL4

```js
/**
 * @param {string} s
 * @param {string[]} words
 * @return {number[]}
 */
var findSubstring = function (s, words) {
  // BF s.length = N, words count M, word length K
  // for index O(N) try to match the words for the string
  // O(N * N)
  // keeping track of a word set O(k*M)
  // an index is valid when the set becomes empty

  // barfoothefoobarman
  // bar foo
  //  arf
  //   rfo
  //    foo thex
  //     oot
  //        the

  // it means one we fail to match a word at index i
  // then we don't need to search the start from i either
  // whether an index is a good word start => this could be cached or precal
  // O(n * k)

  // then we can start with good word start indices
  // and use sliding window by count.

  // use an array to hold the word index for each index. nullable
  // and the problem becomes
  // [-1,0,-1, -1, 1, -1, -1, 2,-1]
  // to find a contiguous subarray which hold unique indices.

  // sliding window problem ?
  // O(N)

  const wordAt = new Array(s.length).fill(null);
  const wordSet = new Map();
  for (const word of words) {
    wordSet.set(word, (wordSet.get(word) ?? 0) + 1);
  }
  const wordLength = words[0].length;
  for (let i = 0; i < s.length; i++) {
    const word = s.slice(i, i + wordLength);
    if (wordSet.has(word)) {
      wordAt[i] = word;
    }
  }

  const result = [];
  for (let i = 0; i < s.length; i++) {
    const newWordSet = new Map(wordSet);
    let start = i;
    while (start < s.length) {
      if (wordAt[start] == null) {
        break;
      }

      // already used
      if (!newWordSet.has(wordAt[start])) {
        break;
      }

      const newCount = newWordSet.get(wordAt[start]) - 1;
      if (newCount === 0) {
        newWordSet.delete(wordAt[start]);
      } else {
        newWordSet.set(wordAt[start], newCount);
      }

      if (newWordSet.size === 0) {
        result.push(i);
        break;
      }

      start += wordLength;
    }
  }

  return result;
};
```
