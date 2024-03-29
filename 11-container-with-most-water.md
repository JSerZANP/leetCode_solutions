A video explaining this: https://youtu.be/ObUUdpIk3hM

## 1.

```js
/**
 * @param {number[]} height
 * @return {number}
 */

// brute force
// O(n^2)
var maxArea = function (height) {
  let max = 0;

  for (let i = 0; i < height.length - 1; i++) {
    for (let j = i + 1; j < height.length; j++) {
      max = Math.max(max, (j - i) * Math.min(height[i], height[j]));
    }
  }

  return max;
};
```

## 2 two cursors 1

```js
// /**
//  * @param {number[]} height
//  * @return {number}
//  */
var maxArea = function (height) {
  if (height.length === 0) return 0;
  // suppose we have fine the most water
  // if means we can remove the border outside the range because they are short
  // suppose we have an initial border of two.
  // now if we insert borders inside, then it only matters if it is larger than the shorter border
  // so it is safe now to remove borders on the shorter side

  // [1,8,6,2,5,4,8,3,7]
  // [1               7]  candidate
  //    [8            7]. candidate
  //.   [8        8] candiate
  // done

  let i = 0;
  let j = height.length - 1;
  let max = 0;
  // for each move
  while (i < j) {
    max = Math.max(max, Math.min(height[i], height[j]) * (j - i));
    if (height[i] < height[j]) {
      i += 1;
    } else {
      j -= 1;
    }
  }
  return max;
};
```

## 3 two cursors 2

```js
// two cursors
// O(N)

var maxArea = function (height) {
  let max = 0;

  let i = 0;
  let j = height.length - 1;

  while (i < j) {
    max = Math.max(max, (j - i) * Math.min(height[i], height[j]));

    // try to move the cursors
    if (height[i] < height[j]) {
      // move i to the next bigger border
      let k = i + 1;
      while (height[k] <= height[i]) {
        k += 1;
      }

      i = k;
    } else {
      let k = j - 1;
      while (height[k] <= height[j]) {
        k -= 1;
      }

      j = k;
    }
  }

  return max;
};
```
