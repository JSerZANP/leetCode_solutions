Youtube video explaining this: https://youtu.be/kONcHqWCmBo

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
// Time: n!
var permute = function (nums) {
  const result = [];

  const walk = (temp, rest) => {
    if (rest.length === 0) {
      result.push(temp);
      return;
    }

    for (let i = 0; i < rest.length; i++) {
      const newRest = rest.slice(0);
      newRest.splice(i, 1);
      walk(temp.concat(rest[i]), newRest);
    }
  };

  walk([], nums);

  return result;
};
```

Another try in 2024

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function (nums) {
  // for each pick we choose an item from the nums
  // use a set to pevent duplicate
  const result = [];
  const pick = (temp, set, rest) => {
    if (rest.size === 0) {
      result.push(temp);
    } else {
      // be careful that the manipulating of set on the fly
      // affects the for loop
      for (const item of [...rest]) {
        if (!set.has(item)) {
          set.add(item);
          rest.delete(item);
          pick([...temp, item], set, rest);
          set.delete(item);
          rest.add(item);
        }
      }
    }
  };
  pick([], new Set(), new Set(nums));
  return result;
};
```
