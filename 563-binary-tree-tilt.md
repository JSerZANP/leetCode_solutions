Youtube video explaining this: https://youtu.be/n7iOrbGF4_g
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
var findTilt = function(root) {
    const getTiltAndSum = (node) => {
        
        if (node === null) {
            return [0, 0]
        }
        const rightTiltAndSum = getTiltAndSum(node.right)
        const leftTiltAndSum = getTiltAndSum(node.left)
        
        return [Math.abs(rightTiltAndSum[1] - leftTiltAndSum[1]) + rightTiltAndSum[0] + leftTiltAndSum[0], rightTiltAndSum[1] + leftTiltAndSum[1] + node.val]
    }
    
    return getTiltAndSum(root)[0]
};
```
