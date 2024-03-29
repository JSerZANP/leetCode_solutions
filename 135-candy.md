```js
/**
 * @param {number[]} ratings
 * @return {number}
 */
var candy = function (ratings) {
  // [1,0,2]
  // [1,0,1]

  // [0, 1, 1]

  // [1, 2, 5, 4]

  // [1, 1, ]

  // [0, 1, 2, 3, 4, 2, 1, 3, 10, 9,8,6, 7, 8, 5, 4, 3, 2, 1]

  //  1, 2, 3, 4, 5, 2, 1, 2, 4, 3, 2,1, 2, 3, 2, 1

  // some obversations
  // 1. 1 candy is enough for child at low
  // 2. child in the upward slope, candy is decided by how far they are fro the previous low
  // 3. child in the downward slope, candy is decided by how far they are to the next low
  // 4. child at the high, candy is to be the bigger of left and right + 1

  // if we go up, we can just add candies by prev + 1
  // if we go down we will go the next low and calculatet the candies directly. Previous high needs to be updated if needed.
  // so we only need to know the indices of high and lows.

  // what if ratings are the same?  there will be consecutive highs and lows, need to skip the actions
  // there could be >=2 lows but there are maximum 2 highs
  // because we check lows first. if >=3 same ratings, the ones in between are treated as lows

  let len = ratings.length;
  const candies = new Array(len).fill(0);

  let prevHigh = -1;
  let prevLow = -1;
  for (let i = 0; i < len; i++) {
    // skip consecutive lows
    if (isLow(i)) {
      candies[i] = 1;

      if (i > 0 && !isLow(i - 1)) {
        if (prevHigh > -1) {
          // we can update the candies to prevHigh
          for (let j = i - 1; j >= prevHigh; j--) {
            candies[j] = Math.max(i - j + 1, candies[j]);
          }
        }
      }

      prevLow = i;
    }

    if (isHigh(i)) {
      if (i > 0 && !isHigh(i - 1)) {
        // we can update the candies from prevLow
        if (prevLow > -1) {
          for (let j = prevLow + 1; j <= i; j++) {
            candies[j] = Math.max(j - prevLow + 1, candies[j]);
          }
        }
      }

      prevHigh = i;
    }
  }

  // this result in multiple lows
  function isLow(i) {
    if (i > 0 && ratings[i] > ratings[i - 1]) return false;
    if (i < len - 1 && ratings[i] > ratings[i + 1]) return false;
    return true;
  }

  function isHigh(i) {
    if (i > 0 && ratings[i] < ratings[i - 1]) return false;
    if (i < len - 1 && ratings[i] < ratings[i + 1]) return false;
    return true;
  }

  const totalCandies = candies.reduce((result, count) => {
    return result + count;
  }, 0);
  return totalCandies;
};
```
