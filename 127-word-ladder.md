And here a video explaining this: https://youtu.be/pmImer7O3pM

```js
/**
 * @param {string} beginWord
 * @param {string} endWord
 * @param {string[]} wordList
 * @return {number}
 */

// n word, k letters
// Time: O(n^2)
// space: O(n^2)
var ladderLength = function (beginWord, endWord, wordList) {
  // 1. pre proces the wordList create a graph

  // O(k)
  const isTransformable = (word1, word2) => {
    // count the different letters
    let isDifferenceFound = false;
    for (let i = 0; i < word1.length; i++) {
      if (word1[i] !== word2[i]) {
        if (isDifferenceFound) {
          return false;
        }
        isDifferenceFound = true;
      }
    }

    return true;
  };

  // Map<string, Set<string>>
  // O(n^2) space
  const transformable = new Map();

  let isEndWordFound = wordList[wordList.length - 1] === endWord;

  // O(n^2) time
  for (let i = 0; i < wordList.length - 1; i++) {
    if (wordList[i] === endWord) isEndWordFound = true;
    for (let j = i + 1; j < wordList.length; j++) {
      if (isTransformable(wordList[i], wordList[j])) {
        if (transformable.has(wordList[i])) {
          transformable.get(wordList[i]).add(wordList[j]);
        } else {
          transformable.set(wordList[i], new Set([wordList[j]]));
        }

        if (transformable.has(wordList[j])) {
          transformable.get(wordList[j]).add(wordList[i]);
        } else {
          transformable.set(wordList[j], new Set([wordList[i]]));
        }
      }
    }
  }

  // a) return immediately if endWord is not in the list
  if (!isEndWordFound) return 0;
  // 2. BFS it backwords, check the path length for all the words from endEowrd

  // Map<word, steps>
  // O(n) space
  const stepsMap = new Map();

  // O(n) space
  const queue = [endWord];
  let steps = 1;

  // O(n^2) time
  while (queue.length > 0) {
    queue.push(null);
    let head;
    while ((head = queue.shift())) {
      stepsMap.set(head, steps);

      const nextWords = transformable.get(head);

      if (nextWords) {
        for (let next of nextWords) {
          if (!stepsMap.has(next)) {
            queue.push(next);
            stepsMap.set(next, 0);
          }
        }
      }
    }

    steps += 1;
  }

  // 3. match beginWord against all
  let result = Infinity;
  for (let [word, steps] of stepsMap) {
    if (isTransformable(word, beginWord)) {
      result = Math.min(result, steps + 1);
    }
  }

  return result === Infinity ? 0 : result;
};
```

Another try in 2024

```js
/**
 * @param {string} beginWord
 * @param {string} endWord
 * @param {string[]} wordList
 * @return {number}
 */
var ladderLength = function (beginWord, endWord, wordList) {
  // one mutation => count the indices where digits are different
  // shortest -> BFS

  // undirectional GRAPH
  // edge => only one mutation
  // we'll calculate the edges for startGene | bank

  // Map<string, Set<string>>
  const graph = new Map();

  const createEdge = (from, to) => {
    if (!graph.has(from)) {
      graph.set(from, new Set());
    }
    graph.get(from).add(to);
    if (!graph.has(to)) {
      graph.set(to, new Set());
    }
    graph.get(to).add(from);
  };

  for (let i = 0; i < wordList.length - 1; i++) {
    for (let j = i + 1; j < wordList.length; j++) {
      if (isMutation(wordList[i], wordList[j])) {
        createEdge(wordList[i], wordList[j]);
      }
    }
  }

  for (let i = 0; i < wordList.length; i++) {
    if (isMutation(wordList[i], beginWord)) {
      createEdge(wordList[i], beginWord);
    }
  }

  const queue = [beginWord];
  const visited = new Set();
  let steps = 1;

  while (queue.length > 0) {
    let count = queue.length;
    while (count > 0) {
      const head = queue.shift();
      if (head === endWord) {
        return steps;
      }

      if (!visited.has(head)) {
        visited.add(head);
        const nodes = graph.get(head);
        if (nodes != null) {
          nodes.forEach((word) => {
            queue.push(word);
          });
        }
      }

      count -= 1;
    }
    steps += 1;
  }

  return 0;
};

function isMutation(from, to) {
  let differences = 0;
  for (let i = 0; i < from.length; i++) {
    if (from[i] !== to[i]) {
      differences += 1;
    }
    if (differences > 1) {
      return false;
    }
  }
  return differences === 1;
}
```
