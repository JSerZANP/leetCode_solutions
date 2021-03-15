
Here is a video explaining it: https://youtu.be/TF_8mA6jw7A


```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    // [7 1 5 3 6 4 8]
  
    // Array<max profit ending at i>
    // Array<max profit start at i>
  
    const maxProfitFromLeftAt = new Array(prices.length).fill(0)
    const maxProfitFromRightAt = new Array(prices.length + 1).fill(0)
    
    let minPrice = prices[0]
    for (let i = 1; i < prices.length; i++) {
      const price = prices[i]
      if (price < minPrice) {
        minPrice = price
      }
      
      const profit = price - minPrice
      maxProfitFromLeftAt[i] = Math.max(maxProfitFromLeftAt[i - 1], profit)
    }
    
  
    let result = prices.length > 0 ? maxProfitFromLeftAt[prices.length - 1] : 0
    
    let maxPrice = prices[prices.length - 1]
    for (let i = prices.length - 2; i > 0; i--) {
      const price = prices[i]
      if (price > maxPrice) {
        maxPrice = price
      }
      
      const profit = maxPrice - price
      const maxProfit = Math.max(maxProfitFromRightAt[i + 1], profit)
      maxProfitFromRightAt[i] = maxProfit
      
      
      result = Math.max(result, maxProfit + maxProfitFromLeftAt[i - 1])
    }
  
  
    return result
};
```
