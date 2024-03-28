Here is my video explaining it: https://youtu.be/l15PJ62EhSk

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  // buy at min, sell at max,  max is after min
  // to buy at i, search sell at j cost n -i
  // O(n ^ 2)

  // loop through the price
  // keep track of the min
  // get profit at each index, collect the max

  let minPrice = prices[0];

  let maxProfit = 0;

  for (let price of prices) {
    if (price < minPrice) {
      minPrice = price;
    }

    // best profit selling at this price
    const profit = Math.max(price - minPrice, 0);
    maxProfit = Math.max(maxProfit, profit);
  }

  return maxProfit;
};
```
