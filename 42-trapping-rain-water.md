## 1. easy to understand - pre calculate the borders

Youtube video explaining this: https://youtu.be/LyuDZSNHn48

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function (height) {
  const maxFromLeft = new Array(height.length).fill(0);
  const maxFromRight = new Array(height.length).fill(0);

  let max = 0;
  for (let i = 0; i < height.length; i++) {
    max = Math.max(height[i], max);
    maxFromLeft[i] = max;
  }

  max = 0;
  for (let i = height.length - 1; i > -1; i--) {
    max = Math.max(height[i], max);
    maxFromRight[i] = max;
  }

  let maxWater = 0;
  for (let i = 0; i < height.length; i++) {
    const boundary = Math.min(maxFromLeft[i], maxFromRight[i]);
    maxWater += boundary - height[i];
  }

  return maxWater;
};
```

## 2. one pass - tear down the borders from both sides

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function (height) {
  // observations
  // 1. only low can trap water
  // 2. water is decided the by lower border
  // 3. if we think there is only two borders at the beginning
  //   only the border in between that are taller can make a difference

  // it means water[i, j] = watter[m, n] + the watters on both side
  // we only need to find the meaningful borders

  // [0,1,0,2,1,0,1,3,2,1,2,1]
  // 0 -> not border
  //    1                   1
  //       they can trap watter
  //      we need to find the border that is taller
  //      0 watter, because we start from the smaller, it trap 1
  //       2 new border
  //                      2
  //                3 new border

  // every time we choose the smaller outer border is because
  // it will be the short border no matter if there is taller border or not

  let i = 0;
  let j = height.length - 1;
  let water = 0;
  let borderLeft = height[i];
  let borderRight = height[j];
  while (i <= j) {
    if (borderLeft <= borderRight) {
      // trap water until new border
      if (height[i] <= borderLeft) {
        water += borderLeft - height[i];
      }
      borderLeft = Math.max(borderLeft, height[i]);
      i += 1;
    } else {
      // trap water until new border
      if (height[j] <= borderRight) {
        water += borderRight - height[j];
      }
      borderRight = Math.max(borderRight, height[j]);
      j -= 1;
    }
  }
  // when i, j meats, there is no water? no there is water
  return water;
};
```
