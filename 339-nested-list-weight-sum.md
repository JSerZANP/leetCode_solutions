A video explaining this https://youtu.be/yKVw8bDsiaM

```js
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * function NestedInteger() {
 *
 *     Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     @return {boolean}
 *     this.isInteger = function() {
 *         ...
 *     };
 *
 *     Return the single integer that this NestedInteger holds, if it holds a single integer
 *     Return null if this NestedInteger holds a nested list
 *     @return {integer}
 *     this.getInteger = function() {
 *         ...
 *     };
 *
 *     Set this NestedInteger to hold a single integer equal to value.
 *     @return {void}
 *     this.setInteger = function(value) {
 *         ...
 *     };
 *
 *     Set this NestedInteger to hold a nested list and adds a nested integer elem to it.
 *     @return {void}
 *     this.add = function(elem) {
 *         ...
 *     };
 *
 *     Return the nested list that this NestedInteger holds, if it holds a nested list
 *     Return null if this NestedInteger holds a single integer
 *     @return {NestedInteger[]}
 *     this.getList = function() {
 *         ...
 *     };
 * };
 */
/**
 * @param {NestedInteger[]} nestedList
 * @return {number}
 */

// Time: O(n)
// Space: worst O(n)
// var depthSum = function(nestedList) {
//     // [[1,1],2,[1,1]]   => 1
//     const getSum = (arr, depth) => {
//       let sum = 0
//       for (let item of arr) {
//         if (item.isInteger()) {
//           sum += item.getInteger() * depth
//         } else {
//           sum += getSum(item.getList(), depth + 1)
//         }
//       }
//       return sum
//     }
    
//     return getSum(nestedList, 1)
// };


// BFS
// Time: O(n)
// Space: O(n)
var depthSum = function(nestedList) {
    const queue = nestedList.slice(0)
    let sum = 0
    
    let depth = 1
    
    while (queue.length > 0) {
      let count = queue.length
      while (count > 0) {
        
        const head = queue.shift()
        
        if (head.isInteger()) {
          sum += head.getInteger() * depth
        } else {
          const list = head.getList()
          queue.push(...list)
        }
        
        count -= 1
      }
      
      depth += 1
    }
  
    return sum
};






















```
