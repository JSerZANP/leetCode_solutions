Here is me on youtube explaining it: https://youtu.be/q2P-gF7B4-w


```js
/**
 * @param {number[]} w
 */
var Solution = function(w) {
  this.sums = [0]
  // [0, 1)
  // [0, 1, 4) => [0, 1)  [1, 4)
  let sum = 0
  for (let weight of w) {
    sum += weight
    this.sums.push(sum)
  }
};

/**
 * @return {number}
 */
// O(log N)
// O(N)
Solution.prototype.pickIndex = function() {
  // Math.random() => [0, 1)
  // 1, 2, 3
  // 0 X [ 1, X3,X 6]
  // [0, 1) [1, 2, 3) [3, 4, 5, 6)
  // [0, 1, 3]
  // Math.random() * total length, Math.floor to get the interval index
  // Math.random() * 6
  // 0, 1, 2, 3, 4, 5
  
  // linear search, O(n)
  // binary search, O(log n)
  
  // what we need
  // a sum array => binary search
  
  const num = Math.floor(Math.random() * this.sums[this.sums.length - 1])
  
  // binary search [i, j]
  let i = 0
  let j = this.sums.length - 1
     
  // [0, 1, 3, 6] => 2
  // [1, 3, 6] => 4
  // [1, 3] => [3] => 
  while (i <= j) {
   const middle = Math.floor((i + j) / 2)
   if (this.sums[middle] === num) {
     return middle
   } else if (num < this.sums[middle]) {
     j = middle - 1
   } else {
     i = middle + 1
   }
  }
  
  // i is the inersetion index
  return j
};


//  [1,2, 3....] existence of n,    while(i <= j) return false as default
//  [1, 2, 3 . .] find insertion position of n, 
//       n in [i, i + 1),   while(j - i > 1)
//  [-Infinity, 1, 2, ...., Infinity]

/** 
 * Your Solution object will be instantiated and called as such:
 * var obj = new Solution(w)
 * var param_1 = obj.pickIndex()
 */
 ```
