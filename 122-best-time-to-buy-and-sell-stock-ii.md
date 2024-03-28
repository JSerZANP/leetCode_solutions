Here is my video of explaining it: https://youtu.be/2AhTLGxptlA

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  // point Buy => soon to go up, next is bigger
  // point Sell => soon to go down, next is smaller

  let profit = 0;

  for (let i = 0; i < prices.length; i++) {
    // if it the point Buy, we search next to the point sell
    if (i === 0 || prices[i + 1] > prices[i]) {
      // this is a point to buy
      // search for the point sell, it might be itself
      let j = i;
      while (prices[j + 1] >= prices[j]) {
        j += 1;
      }

      // i j might be the same, skip
      if (j > i) {
        profit += prices[j] - prices[i];
      }

      i = j;
    }
  }

  return profit;
};
```

since we can sell immediately, following code is simpler

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  // basically get all the profit from 2 consecutive increasing price

  // if a price is larger than previous one collect the profit
  // otherise do nothing
  let profit = 0;
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] > prices[i - 1]) {
      profit += prices[i] - prices[i - 1];
    }
  }
  return profit;
};
```
