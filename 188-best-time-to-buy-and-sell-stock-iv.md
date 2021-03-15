
Me explaining it on youtube: https://youtu.be/ryj_4Tygxy4


```js
/**
 * @param {number} k
 * @param {number[]} prices
 * @return {number}
 */

var maxProfitForInfinite = function(prices) {
    // point Buy => soon to go up, next is bigger
    // point Sell => soon to go down, next is smaller
     
    //  [1, 5, 5, 6] =>  [1, 5, 6] => [1, 6]
    //  [1, 5, 3, 6] => [1, 5], [3, 6] => 
  
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


// Time: O(MN)
// Space: O(2N) => O(N)
var maxProfit = function(k, prices) {
    if (prices.length === 0) return 0
    // [3,2,6,5,0,3]  k
  
    if (k > prices.length / 2) return maxProfitForInfinite(prices)
  
    // A[k][i]  end at index i, should be equal to 
    //     max {
    //        A[k][i - 1],
    //        max {
    //           j = 0 -> i - 1, A[k - 1][j - 1] + A[i] - A[j]
    //        }
    //     }
    
    let dp = new Array(prices.length).fill(0)
    let prevUpdated = 0
    
    for (let t = 1; t <= k; t++) {
      let minPrice = Infinity
      for (let i = 0; i < prices.length; i++) {
        minPrice = Math.min(minPrice, prices[i] - (i > 0 ? prevUpdated : 0))
        prevUpdated = dp[i]
        dp[i] = Math.max((i > 0 ? dp[i - 1] : 0), prices[i] - minPrice)
      }
    
    }
    
    return dp[prices.length - 1]
};
```
