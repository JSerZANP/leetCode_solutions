Me explaining it on youtube: https://youtu.be/YauS1CuAP2Q

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
 * @param {number} L
 * @param {number} R
 * @return {number}
 */
var rangeSumBST = function(root, L, R) {
    if (root === null) return 0
    // brute force
    // O(N)
   
    //     10
    //   5    15
    // 3   7     18
    
    // return sum to a range []
    const walk = (node, min, max) => {
      if (node === null) return 0
      
      let sumLeft = 0
      let sumRight = 0
      
      if (node.val > min) {
        sumLeft = walk(node.left, min, max)
      }
      
      if (node.val < max) {
        sumRight = walk(node.right, min, max)
      }
      
      let sum = sumLeft + sumRight
      
      if (node.val >= min && node.val <= max) {
        sum += node.val
      }
      
      return sum
    }
    
    return walk(root, L, R)
};
```
