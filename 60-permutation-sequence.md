
A video explaining this: https://youtu.be/LQXcCbTOE_c


```js
/**
 * @param {number} n
 * @param {number} k
 * @return {string}
 */

// Back Tracking (Naive) 
// Time: O(k)??
// Space: O(n)?
// var getPermutation = function(n, k) {
//     let result
//     let count = 0
    
//     const walk = (temp, rest) => {
//       if (rest.length === 0) {
//         count += 1
        
//         if (count === k) {
//           result = temp.join('')
//           return 1
//         }
//       }
      
//       for (let i = 0; i < rest.length; i++) {
//         const newRest = rest.slice(0)
//         newRest.splice(i, 1)
//         const resultWalk = walk(temp.concat(rest[i]), newRest)
//         if (resultWalk) {
//           return 1
//         }
//       }
      
//       return 0
//     }
    
//     // generate the nums
//     // O(n)
//     const nums = []
//     while (n >= 1) {
//       nums.unshift(n);
//       n -= 1
//     }
    
//     walk([], nums)
  
//     return result
// };


// improve by avoding unncessarry generating
// jump the steps


// decide each digit from left to right

// Time: O(n)
// Space: O(n)
var getPermutation = function(n, k) {
  // firt , get the fac array 
  const fac = [1, 1, 2]
  for (let i = 3; i <= n; i++) {
    fac.push(fac[i - 1] * i)
  }
  // means there would be fac[n] possibilities for n-digit

  // get all the digits
  // O(n)
  const nums = []
  while (n >= 1) {
    nums.unshift(n)
    n -= 1
  }
  
  const result = []
  
  // what is the first digit of k-th possiblity?
  // for each didgit, there would be fac[n - 1] possibility
  
  // considering k = 1, and n = 2
  // it should be ceil - 1
  // <=1 => 0
  // 1 <= 2 => 1
  // O(n)
  while (nums.length > 0) {
    // get the first digit
    const index = Math.ceil(k / fac[nums.length - 1]) - 1;
    // update k by removing the possibilities
    k -= index * fac[nums.length - 1]
    
    result.push(nums[index])
    nums.splice(index, 1)
  }
  
  return result.join('')
}








```
