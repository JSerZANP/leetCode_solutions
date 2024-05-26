```js
/**
 * @param {number[]} tickets
 * @param {number} k
 * @return {number}
 */
var timeRequiredToBuy = function (tickets, k) {
  // since it goes level by level
  // it basically means
  // the sum of all numbers <= n - 1
  // and the count of number >= n but before k

  // so we can just calculate the sum in one pass
  let result = 0;
  for (let i = 0; i < tickets.length; i++) {
    if (tickets[i] >= tickets[k]) {
      if (i <= k) {
        result += tickets[k];
      } else {
        result += tickets[k] - 1;
      }
    } else {
      result += tickets[i];
    }
  }
  return result;
};
```
