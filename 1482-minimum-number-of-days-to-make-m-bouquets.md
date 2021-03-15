Hear me explaining it on youtube: https://youtu.be/trCaAOCU25c

```js
/**
 * @param {number[]} bloomDay
 * @param {number} m
 * @param {number} k
 * @return {number}
 */

// O(2^n) O(nm)  => k = 1 special case
// 
// var minDays = function(bloomDay, m, k) {
//     // bloomEnd(i) = Math.max(boolmDay[i - k + 1, i])
//     // min(i, m)  minDays ending at i
//     //    =  Math.min(
//     //     Math.max(min(i - k, m - 1), bloomEnd(i)),
//     //     min(i - 1, m)
//     //   ) 
  
//     const bloomWaits = []
    
//     for (let i = k - 1; i < bloomDay.length; i++) {
//       bloomWaits[i] = Math.max(...bloomDay.slice(i - k + 1, i + 1))
//     }
    
//     // recursion + memoization
//     const cache = new Map()
//     const minDaysAt = (index, boukueCount) => {
//       if (index < boukueCount * k - 1) return Infinity
      
//       if (boukueCount === 0) return 0
      
//       const key = `${index}_${boukueCount}`
//       if (cache.has(key)) return cache.get(key)
//       const result = Math.min(
//         Math.max(bloomWaits[index], minDaysAt(index - k, boukueCount - 1)),
//         minDaysAt(index - 1, boukueCount)
//       )
      
//       cache.set(key, result)
//       return result
//     }
    
//     const result = minDaysAt(bloomWaits.length - 1, m)
//     return result === Infinity ? -1 : result
// }

// with Binary Search

// TIME:  O(NlogN)
// space: O(1)
var minDays = function(bloomDay, m, k) {
   if (m * k > bloomDay.length) return -1
   // we could wait long enough to create m bouque
   // the days are finite => binary search
  
   // 1. get max  O(n)
   // 2. binary search to check if we could O(logN)
   //        check:  O(N)
   
   // O(NlogN)
  
  
   const isPossible = (target) => {
     // count the bloomed flowers
     // OO  O  OOOOO  OOOO
     let bloomedCount = 0
     let countOfBouque = 0
     for (let day of bloomDay) {
       if (day <= target) {
         bloomedCount += 1
       } else {
         countOfBouque += Math.floor(bloomedCount / k)
         bloomedCount = 0
       }
     }
     // trailing flowers
     countOfBouque += Math.floor(bloomedCount / k)
     
     return countOfBouque >= m
   }
  
  
   let start = 1
   let end = Math.max(...bloomDay)
   
   while (start <= end) {
     const middle = Math.floor((start + end) / 2)
     if (isPossible(middle)) {
       end = middle - 1
     } else {
       start = middle + 1
     }
   }
  
   return start
}


```
