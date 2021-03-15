Here is my video explaining: https://youtu.be/ku2EKgqMp0M

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

// recursion
// Time: O(n)
// spaceL O(height of the tree)
// var minDiffInBST = function(root) {
//     //   4         a
//     // 2  6     b      c
    
//     // b < a < c, minimunm must be [b, a], [a, c]
    
//     // if root node is in the optimal result, it must be
//     // [biggest left, root], [root, smallest right]
    
//     let result = Infinity
//     // return [min, max]
//     const walk = (node) => {
        
//         if (node === null) {
//             return [Infinity, -Infinity]
//         }
        
        
//         const [minLeft, maxLeft] = walk(node.left)
//         const [minRight, maxRight] = walk(node.right)
        
//         result = Math.min(
//             result, 
//             Math.abs(maxLeft - node.val),
//             Math.abs(minRight - node.val)
//         )
        
//         return [Math.min(minLeft, node.val), Math.max(maxRight, node.val)]
//     }
    
//     walk(root)
    
//     return result
// };

// in-order traversal
var minDiffInBST = function(root) {
    // 1 2 3 4 6
    let result = Infinity
    let prev = Infinity
    // return [min, max]
    const walk = (node) => {
        if (node.left) walk(node.left)
        result = Math.min(result, Math.abs(prev - node.val))
        prev = node.val
        if (node.right) walk(node.right)
    }
    
    walk(root)
    
    return result
};
```
