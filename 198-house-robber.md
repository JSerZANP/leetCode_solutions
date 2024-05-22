```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function (nums) {
  // sum of sub list without consecutive number
  // suppose [a, b, c] are the result
  // for any number, it could be in the list or not
  // look at the last item
  // Max = Max{ last item chosen, last item not chosen}
  // Max{last item chosen} = Max{prev item not chosen}
  // Max{last item not chosen} = Max{prev item chosen, prev item not chosen}

  // max sum that ends at index
  const maxChosen = new Array(nums.length).fill(0);
  const maxNotChosen = new Array(nums.length).fill(0);
  let max = 0;

  for (let i = 0; i < nums.length; i++) {
    maxChosen[i] = (maxNotChosen[i - 1] ?? 0) + nums[i];
    maxNotChosen[i] = Math.max(maxNotChosen[i - 1] ?? 0, maxChosen[i - 1] ?? 0);
    max = Math.max(max, maxChosen[i], maxNotChosen[i]);
  }

  return max;
};
```
