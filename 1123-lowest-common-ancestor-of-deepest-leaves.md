me explaining this on youtube: https://youtu.be/mnNKUC7gOd8


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
 * @return {TreeNode}
 */

/*

      1       0
    2   3     1
   4          2
    
    
*/

// Time: O(n)
// Space: worst call stack O(n)
var lcaDeepestLeaves = function(root) {
    
    // [height of leaf node, node]
    let result = [0, root]
    
    //  return depth (how many layers of node the tree has)
    const walk = (node, depth) => {
        
        if (node === null) return 0
        
        const leftHeight = walk(node.left, depth + 1)
        const rightHeight = walk(node.right, depth + 1)
        
        // it is a possible candiate
        if (leftHeight === rightHeight) {
            // compare the depth of leaf node
            const depthOfLeafNode = depth + leftHeight
            if (depthOfLeafNode >= result[0]) {
                result[0] = depthOfLeafNode
                result[1] = node
            }
        }
        return Math.max(leftHeight, rightHeight) + 1
    }
    
    walk(root, 0)
    
    return result[1]
    
};






```
