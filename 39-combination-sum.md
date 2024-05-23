An explaining video: https://youtu.be/zagXJO34FMQ

```js
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function (candidates, target) {
  // Brute Force => 2^n

  candidates.sort((a, b) => a - b);

  const result = [];
  // Back Tracking
  const walk = (sum, index, temp) => {
    // check if it satisify the condition
    if (sum >= target) {
      if (sum === target) {
        result.push(temp);
      }
      return true;
    }

    // if not, we could add more numbers in it
    for (let i = index; i < candidates.length; i++) {
      const num = candidates[i];

      const shouldTerminate = walk(sum + num, i, temp.concat(num));
      if (shouldTerminate) {
        break;
      }
    }

    return false;
  };

  walk(0, 0, []);

  return result;
};
```

Another try in 2024

```js
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function (candidates, target) {
  // sort the candiates
  // the it is a tree traversal program DFS
  // stop when the same if larger
  candidates.sort((a, b) => a - b);
  const result = [];
  const path = [];
  let sum = 0;

  const walk = (from) => {
    // for each step
    path.push(candidates[from]);
    sum += candidates[from];
    if (sum === target) {
      result.push(path.slice(0));
    }
    if (sum < target) {
      for (let i = from; i < candidates.length; i++) {
        walk(i);
      }
    }
    path.pop();
    sum -= candidates[from];
  };

  for (let i = 0; i < candidates.length; i++) {
    walk(i);
  }
  return result;
};
```
