Watch my video on youtube for this problem: https://youtu.be/PYvqkhp5-48
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */

// Time: O(n)
// Space: worst O(n) for call stack
var diameterOfBinaryTree = function(root) {
    // return [diameter, height]
    const walk = (node) => {
        
        if (node === null) return [0, 0]
        const [leftDiameter, leftHeight] = walk(node.left)
        const [rightDiameter, rightHeight] = walk(node.right)
        
        return [
            Math.max(leftDiameter, rightDiameter, leftHeight + rightHeight),
            Math.max(leftHeight, rightHeight)  + 1
        ]
    }
    
    return walk(root)[0]
};
```
