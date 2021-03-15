Me explaining on youtube: https://youtu.be/1BQmZSAhh-4

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
 * @return {boolean}
 */

// Time: O(n)
// space: worst O(n), avg, O(lgN)
// var isSymmetric = function(root) {
//     const check = (node1, node2) => {
//       if (node1 === null && node2 === null) return true
//       if (node1 !== null && node2 === null) return false
//       if (node1 === null && node2 !== null) return false
//       if (node1.val !== node2.val) return false
//       if (!check(node1.left, node2.right)) return false
//       return check(node1.right, node2.left)
//     }
    
//     return check(root, root)
// };

// get each layer and check them
var isSymmetric = function(root) {
    if (root === null) return true
    // BFS
    const queue = [root]
    
    
    const isEqual = (node1, node2) => {
      if (node1 === null && node2 === null) return true
      if (node1 !== null && node2 === null) return false
      if (node1 === null && node2 !== null) return false
      if (node1.val !== node2.val) return false
      return true
    }
    
    while (queue.length > 0) {
      // check if queue is symmetric or not
      let i = 0
      let j = queue.length - 1
      while (i < j) {
        if (!isEqual(queue[i], queue[j])) {
          return false
        }
        i += 1
        j -= 1
      }
      
      // push the next layer
      let count = queue.length
      while (count > 0) {
        const head = queue.shift()
        if (head !== null) {
          queue.push(head.left)
          queue.push(head.right)
        }
        
        count -= 1
      }
    }
  
    return true
};




```
