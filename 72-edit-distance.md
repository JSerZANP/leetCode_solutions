A video explaining this
https://youtu.be/2491mTTAHaM

```js
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */

// non tail Recursion with Memorizing
// Time:  m x n
// Space: m x n + max(m, n)
// easy to understand
var minDistance = function (word1, word2) {
  // h o r s X
  //     r o O

  // f(i, j)
  // X === O  just ignore both.  f(i - 1, j - 1)
  // X !== O  then  min OF
  //     delete X     f(i - 1, j) + 1
  //     replace      f(i - 1, j - 1) + 1
  //     insert O     f(i, j - 1) + 1
  const cache = Array(word1.length + 1)
    .fill(0)
    .map((_) => Array(word2.length + 1).fill(-1));

  const min = (i, j) => {
    if (cache[i + 1][j + 1] > -1) {
      return cache[i + 1][j + 1];
    }

    if (i < 0) return j + 1;
    if (j < 0) return i + 1;

    if (word1[i] === word2[j]) {
      cache[i + 1][j + 1] = min(i - 1, j - 1);
    } else {
      cache[i + 1][j + 1] =
        Math.min(min(i - 1, j), min(i - 1, j - 1), min(i, j - 1)) + 1;
    }

    return cache[i + 1][j + 1];
  };

  return min(word1.length - 1, word2.length - 1);
};
```

```js
// Iteration, reversed version of Recursion
// DP
var minDistance = function (word1, word2) {
  // dp[i][j] means word1[0, i] transformed to word2[0, j]
  const dp = Array(word1.length + 1)
    .fill(0)
    .map((_) => Array(word2.length + 1).fill(-1));
  // firs initialize the 0 cases
  for (let i = 0; i < dp.length; i++) {
    dp[i][0] = i;
  }

  for (let j = 0; j < dp[0].length; j++) {
    dp[0][j] = j;
  }

  // bottom up of recursion
  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      if (word1[i - 1] === word2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1];
      } else {
        dp[i][j] = Math.min(
          dp[i - 1][j - 1] + 1,
          dp[i - 1][j] + 1,
          dp[i][j - 1] + 1
        );
      }
    }
  }

  return dp[word1.length][word2.length];
};
```

Another try in 2024

```js
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function (word1, word2) {
  // horse => ros
  // first we need to align the length
  // 2 deletions

  // but which should we delete?

  // look at first letter - h
  // h is not r, there a few posibilities
  // insert r at the beginning, then "horse" => "os"
  // delete h" => "orse" => os"
  // replace, then better just replace it with "r" => "orse" => "os"
  // if both are same, then another chance is do nothing

  // recursion i, j

  const len1 = word1.length;
  const len2 = word2.length;
  if (len1 === 0) return len2;
  if (len2 === 0) return len1;

  const cache = new Array(len1).fill(0).map((_) => new Array(len2).fill(-1));

  const minDistanceFrom = (i, j) => {
    if (i === len1) return len2 - 1 - j + 1;
    if (j === len2) return len1 - 1 - i + 1;
    if (cache[i][j] >= 0) return cache[i][j];
    // do nothing                    // delete                    // insertion
    const min = Math.min(
      minDistanceFrom(i + 1, j + 1) + (word1[i] === word2[j] ? 0 : 1),
      minDistanceFrom(i + 1, j) + 1,
      minDistanceFrom(i, j + 1) + 1
    );
    cache[i][j] = min;
    return min;
  };

  return minDistanceFrom(0, 0);

  // every i, j pair is processed and cached
  // so O(mn), O(mn)
};
```
