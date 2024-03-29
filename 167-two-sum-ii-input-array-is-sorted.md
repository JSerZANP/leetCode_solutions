## 1. Map

```js
// /**
//  * @param {number[]} numbers
//  * @param {number} target
//  * @return {number[]}
//  */
var twoSum = function (numbers, target) {
  const map = new Map();

  for (let i = 0; i < numbers.length; i++) {
    if (map.has(target - numbers[i])) {
      return [i + 1, map.get(target - numbers[i]) + 1].sort((a, b) => a - b);
    }
    map.set(numbers[i], i);
  }
};
```

## 2. Narrow the border

```js
// we didn't take a adavantage of the info "sorted"
// suppose we have i, j, if the sum is smaller, then we need to move i, j to the right
// if bigger we have to move to the left
// the widest range would be 0 j
// so if we start from both ends, if smaller, move i to right, if bigger, move j to the left

var twoSum = function (numbers, target) {
  let i = 0;
  let j = numbers.length - 1;
  // no i <= j because we cannot use the same index
  while (i < j) {
    const sum = numbers[i] + numbers[j];
    if (sum === target) {
      return [i + 1, j + 1];
    } else if (sum < target) {
      i += 1;
    } else {
      j -= 1;
    }
  }
};
```
