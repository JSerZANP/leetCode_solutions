```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function (nums) {
  // choose a start O(n)
  // and just multiple O(n)
  // O(n^2) O(1)

  // A lot of duplicate calculation
  // e.g [2, 3, -2], [3, -2]
  // product [i, j] = Total product / [0, i - 1] / [j + 1, n-1]
  // Total Product O(n)
  // productUntil O(n) productSince O(n)
  // O(n), O(n)

  // for last item, it might be in the maxium range or not
  // if it is in it, then it the maxium range end at previous one
  // or maxium range until previous index

  // O(n), O(n)

  // we can further remove the mxium range until previous index
  // since we'll collect the result during the check
  // so we can always check the maxium end at index i

  // but there is negative numbers, so we need to track the minimum as well
  // turns out we only need to look at prevous index
  // so the dp array could be packed into 2 variables

  let max = -Infinity;
  let maxUntil = -Infinity;
  let minUntil = Infinity;

  for (let num of nums) {
    // pay attention to NOT update the values on the fly
    const currentMaxUntil = maxUntil;
    const currentMinUntil = minUntil;
    if (num == 0) {
      maxUntil = 0;
      minUntil = 0;
    } else if (num > 0) {
      maxUntil = currentMaxUntil > 0 ? currentMaxUntil * num : num;
      minUntil = currentMinUntil <= 0 ? currentMinUntil * num : num;
    } else {
      maxUntil = currentMinUntil <= 0 ? currentMinUntil * num : num;
      minUntil = currentMaxUntil > 0 ? currentMaxUntil * num : num;
    }

    max = Math.max(max, maxUntil);
  }

  return max;
};
```
