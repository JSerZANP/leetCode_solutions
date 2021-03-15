Hear me explaining it on youtube: https://youtu.be/iz7j7eA1gTc


```js
/**
 * @param {number[]} houses
 * @param {number[][]} cost
 * @param {number} m
 * @param {number} n
 * @param {number} target
 * @return {number}
 */

// memoization


//            (0, -1, t)
//     (1, 1, k - 1) (1, 2, k - 1)  ... (1, n, k - 1)  => n
// (2, 1, k - 1)  (2, 2, k - 2) .. (2, n, k - 2)
// .....
// (2, 1, k - 2)  (2, 2, k - 2) ... (2, n, k - 1)    =>  n ^ 2
// without memoization  => 1 + n + n^2 + n^M => O(n^m) upper bound

// with memoization
// 1
// n * 1
// n * 2
// n * 3
// ...  [   ]
//        [   ]
//           [  ]
// n * m

// Time: O(n * m ^ 2)  => O(n * m * k)

// Space: O(m * n * k)
var minCost = function(houses, cost, m, n, target) {
    // 0 0 0 0 0
    // 1 x 0 0 0  create target - 1 neighborhoods from index = 1
    //   1 0 0 0  create target - 1 neighborhoods from index = 2
    //   2 0 0 0  create target - 2 neighborhoods from index = 2
    const cache = new Map()
    const paint = (houseIndex, prevColor, neighborhoods) => {
      if (neighborhoods < 0) return Infinity
      
      const key = `${houseIndex}_${prevColor}_${neighborhoods}`
      
      if (cache.has(key)) {
        return cache.get(key)
      }
      if (houseIndex === m) {
        return neighborhoods === 0 ? 0 : Infinity
      }  
      
      const originColor = houses[houseIndex]
      
      let min = Infinity
      if (originColor === 0) {
        for (let i = 1; i <= n; i++) {
          const possibleMinCost = paint(
            houseIndex + 1, 
            i, 
            i === prevColor ? neighborhoods : neighborhoods - 1) + cost[houseIndex][i - 1]
          
          min = Math.min(min, possibleMinCost)
        }
      } else if (originColor === prevColor) {
        min = Math.min(min, paint(houseIndex + 1, originColor, neighborhoods))
      } else {
        min = Math.min(min, paint(houseIndex + 1, originColor, neighborhoods - 1))
      }
      
      cache.set(key, min)
      return min
    }
    
    const result = paint(0, -1, target)
    return result === Infinity ? -1 : result
};
```
