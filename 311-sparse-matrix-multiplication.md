Here is me explaining it on youtube: https://youtu.be/pyFSfIRSJ68


```js
/**
 * @param {number[][]} A
 * @param {number[][]} B
 * @return {number[][]}
 */
var multiply = function(A, B) {
    // A - m * n
    // B - n * p
    // Ab => m * p
    // Time: O(mnp)
    // Space: O(1)
  
    
    // improve by crushing the matrix
    // [1 1 2 2 2 2 3 3 3 4]
    // [[0, 1], [2, 2], [7, 3],[8,4]]
  
    // [1, 0, 0],  Map([0, 1])
    // [7, 0. 0],  Map([0, 7])
  
    const m = A.length
    
    if (m === 0) return []
  
    const n = A[0].length
    const p = B[0].length
    
    // create the result
    const result = new Array(m).fill(0).map(_ => new Array(p).fill(0))
    
    
    // Space: O(mn + np) worst
    // crush the matrix into more concise foremat
    const crushedA = new Array(m).fill(0).map(_ => new Map())
    const crushedB = new Array(p).fill(0).map(_ => new Map())
    
    // O(mn)
    for (let i = 0; i < m; i++) {
      for (let j = 0; j < n; j++) {
        if (A[i][j] !== 0) {
          crushedA[i].set(j, A[i][j])
        }
      }
    }
    
    // O(np)
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < p; j++) {
        if (B[i][j] !== 0) {
          crushedB[j].set(i, B[i][j])
        }
      }
    }
  
    // Map<index, number>
    const mapMultiply = (mapA, mapB) => {
      if (mapA.size === 0 || mapB.size === 0) return 0
      
      let sum = 0
      let first = mapA
      let second = mapB
      if (mapA.size > mapB.size) {
        first = mapB
        second = mapA
      }
      
      for (let [index, num] of first) {
        if (second.has(index)) {
          sum += num * second.get(index)
        }
      }
      return sum
    }
    
    // O(mpn * alpha) worst is O(mpn) 
    for (let i = 0; i < m; i++) {
      for (let j = 0; j < p; j++) {
        result[i][j] = mapMultiply(crushedA[i], crushedB[j])
      }
    }
  
    return result
};















```
