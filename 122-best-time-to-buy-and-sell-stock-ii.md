Here is my video of explaining it: https://youtu.be/2AhTLGxptlA


```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    // point Buy => soon to go up, next is bigger
    // point Sell => soon to go down, next is smaller
  
  
    let profit = 0
    
    for (let i = 0; i < prices.length; i++) {
      // if it the point Buy, we search next to the point sell
      if (i === 0 || prices[i + 1] > prices[i]) {
        // this is a point to buy
        // search for the point sell, it might be itself
        let j = i
        while (prices[j + 1] >= prices[j]) {
          j += 1
        }
        
        // i j might be the same, skip
        if (j > i) {
          profit += prices[j] - prices[i]
        }
        
        i = j
      }
    }
  
    return profit
};
```
