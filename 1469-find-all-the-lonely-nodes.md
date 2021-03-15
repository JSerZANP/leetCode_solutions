Here is me explaining this on youtube: https://youtu.be/t6zmAgkpbws

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
 * @return {number[]}
 */
// Time: O(n)
// Space: O(1)
// var getLonelyNodes = function(root) {
//     if (root === null) return []
  
//     // walk on each node collect the lonely children
//     const walk = (node, lonelyNodes) => {
      
//       if (node.left !== null) {
//         if (node.right === null) {
//           lonelyNodes.push(node.left.val)
//         }
//         walk(node.left, lonelyNodes)
//       }
      
//       if (node.right !== null) {
//         if (node.left === null) {
//           lonelyNodes.push(node.right.val)
//         }
//         walk(node.right, lonelyNodes)
//       }
//     }
    
//     const lonelyNodes = []
//     walk(root, lonelyNodes)
//     return lonelyNodes
// };

var getLonelyNodes = function(root) {
  if (root === null) return []
  
  const lonelyNodes = []
  const queue = [root]
  
  while (queue.length > 0) {
    const head = queue.shift()
    if (head.left !== null) {
      if (head.right === null) {
        lonelyNodes.push(head.left.val)
      }
      queue.push(head.left)
    }

    if (head.right !== null) {
      if (head.left === null) {
        lonelyNodes.push(head.right.val)
      }
      queue.push(head.right)
    }
  }
  
  return lonelyNodes
}
```
