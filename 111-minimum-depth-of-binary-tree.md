A video explaining this: https://youtu.be/GFcKai8Ra8s

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
var minDepth = function(root) {
    
    if (!root) {
        return 0
    }
    
    const queue = [[root, 1]]
    
    while (queue.length > 0) {
        const [node, depth] = queue.shift()
        
        if (!node.left && !node.right) {
            return depth
        }
        
        if (node.left) {
            queue.push([node.left, depth + 1])
        }
        
        if (node.right) {
            queue.push([node.right, depth + 1])
        }
    }
};
```
