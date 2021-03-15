Here is me explaining it on youtube: https://youtu.be/gm-x2JHB2DQ
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
 * @param {number} target
 * @return {number}
 */

// Time: O(log N) worst O(N)
// Space: O(1)
var closestValue = function(root, target) {
    // binary search target
    // update closest value along the path
  
    let result = Infinity
    
    let node = root
    
    while (node !== null) {
      if (node.val === target) {
        result = target
        break
      }
      
      if (Math.abs(node.val - target) < Math.abs(result - target)) {
        result = node.val
      }
      
      if (target > node.val) {
        node = node.right
      } else {
        node = node.left
      }
    }
    
    return result
};
```
