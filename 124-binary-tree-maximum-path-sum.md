Here is the video for this problem: https://youtu.be/tZrhPNubBJk
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */

// Time: O(n)
// Time: O(n)
// var maxPathSum = function(root) {
    
//     // return [max, maxConnected]
//     const walk = (node) => {
//       if (node === null) return [-Infinity, -Infinity]
      
//       const [maxLeft, maxLeftConnected] = walk(node.left)
//       const [maxRight, maxRightConnected] = walk(node.right)
      
//       const maxConnected = Math.max(
//         node.val,
//         node.val + maxLeftConnected,
//         node.val + maxRightConnected
//         )
      
//       const max = Math.max(
//         maxLeft,
//         maxRight,
//         maxConnected,
//         node.val + maxLeftConnected + maxRightConnected
//       )
      
//       return [max, maxConnected]
//     }
    
//     return walk(root)[0]
// };


// Time: O(n)
// Space: O(n)
// var maxPathSum = function(root) {
    
//     let max = -Infinity
    
//     // return [max, maxConnected]
//     const walk = (node) => {
//       if (node === null) return -Infinity
      
//       const maxLeftConnected = walk(node.left)
//       const maxRightConnected = walk(node.right)
      
//       const maxConnected = Math.max(
//         node.val,
//         node.val + maxLeftConnected,
//         node.val + maxRightConnected
//         )
      
//       max = Math.max(
//         max,
//         maxConnected,
//         maxLeftConnected,
//         maxRightConnected,
//         node.val + maxLeftConnected + maxRightConnected
//       )
      
//       return maxConnected
//     }
    
//     walk(root)
//     return max
// };

var maxPathSum = function(root) {

  let max = -Infinity
  
  const walk = (node) => {
    if (node === null) return -Infinity
    
    const maxLeft = walk(node.left)
    const maxRight = walk(node.right)
    
    const maxConnected = Math.max(
      node.val,
      maxLeft + node.val,
      maxRight + node.val
      )
      
    max = Math.max(
      max,
      maxLeft,
      maxRight,
      maxConnected,
      node.val + maxLeft + maxRight
      )
      
    return maxConnected
  }
  walk(root)
  return max
}
```
