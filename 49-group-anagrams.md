Youtube video explaining this: https://youtu.be/LINRCoEoyFM

```js
/**
 * @param {string[]} strs
 * @return {string[][]}
 */

// Sort the strings first
// k letters N words
// Time: O(N * k * logk)
// Space: O(N)
// var groupAnagrams = function(strs) {
//     const result = new Map()

//     for (let str of strs) {
//       const sorted = str.split('').sort().join('')
//       if (result.has(sorted)) {
//         result.get(sorted).push(str)
//       } else {
//         result.set(sorted, [str])
//       }
//     }

//     return Array.from(result.values())
// };

// counting the existence of letters
// Time: O(N * k) ?
// Space: O(N + 26)
var groupAnagrams = function (strs) {
  const result = new Map();

  for (let str of strs) {
    const count = Array(26).fill(0);
    for (let i = 0; i < str.length; i++) {
      count[str.charCodeAt(i) - 97] += 1;
    }
    const somewhatHash = count.join("|"); // 20000001000000005
    if (result.has(somewhatHash)) {
      result.get(somewhatHash).push(str);
    } else {
      result.set(somewhatHash, [str]);
    }
  }

  return Array.from(result.values());
};
```
