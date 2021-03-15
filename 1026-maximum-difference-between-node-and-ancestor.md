me explaining on youtube: https://youtu.be/qMkVK0Ipbs8

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
// Space: worst O(n)
// var maxAncestorDiff = function(root) {
//     let result = 0
    
//     // (node, [max, min])
//     const walk = (node, [max, min]) => {
//         if (node === null) return
//         result = Math.max(Math.abs(max - node.val), Math.abs(min - node.val), result)
        
//         const newMax = Math.max(max, node.val)
//         const newMin = Math.min(min, node.val)
//         walk(node.left, [newMax, newMin])
//         walk(node.right, [newMax, newMin])
//     }
    
//     walk(root, [root.val, root.val])
    
//     return result
// };


// iteration with BFS

// Time: O(n)
// Space: O(n/2) => O(n)
// var maxAncestorDiff = function(root) {
//     let result = 0
    
//     const queue = [[root, root.val, root.val]]
    
//     let head
//     while (head = queue.shift()) {
//         const [node, max, min] = head
//         result = Math.max(Math.abs(max - node.val), Math.abs(min - node.val), result)
        
//         const newMax = Math.max(max, node.val)
//         const newMin = Math.min(min, node.val)
//         if (node.left) {
//             queue.push([node.left, newMax, newMin])
//         }
//         if (node.right) {
//             queue.push([node.right, newMax, newMin])
//         }
//     }
    
//     return result
// };

// DFS iteration
var maxAncestorDiff = function(root) {
    let result = 0
    
    const stack = []
    
    const push = ([node, max, min]) => {
        stack.push([node, max, min])
        const newMax = Math.max(max, node.val)
        const newMin = Math.min(min, node.val)
        
        if (node.left) {
            push([node.left, newMax, newMin])
        }
    }
    
    push([root, root.val, root.val])
    
    let top
    while(top = stack.pop()) {
        const [node, max, min] = top
        result = Math.max(Math.abs(max - node.val), Math.abs(min - node.val), result)
        if (node.right) {
            const newMax = Math.max(max, node.val)
            const newMin = Math.min(min, node.val)
            push([node.right, newMax, newMin])
        }
    }
    
    return result
};

```
