
Here is my video of explaining this: https://youtu.be/sfc0BjiMbI8


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
 * @return {boolean}
 */
// Time: O(n)
// space: O(n) call stack
// var isValidBST = function(root) {
//     const walk = (node) => {
//         if (node === null) return [true, Infinity, -Infinity]
//         const [isLeftValid, minOfLeft, maxOfLeft] = walk(node.left)
//         const [isRightValid, minOfRight, maxOfRight] = walk(node.right)
        
//         return [isLeftValid && isRightValid && maxOfLeft < node.val && minOfRight > node.val,
//                 Math.min(minOfLeft, node.val), Math.max(maxOfRight, node.val)]
//     }
    
//     return walk(root)[0]
// };

// same as above
// var isValidBST = function(root) {
//     const walk = (node, min, max) => {
//         if (node === null) return true
//         const isLeftValid = walk(node.left, min, Math.min(node.val, max))
//         const isRightValid = walk(node.right, Math.max(node.val, min), max)
        
//         return isLeftValid && isRightValid && node.val < max && node.val > min
//     }
    
//     return walk(root, -Infinity, Infinity)
// };


// Iteration
// Time: O(n)
// Space: worst O(n/2) = O(n)
// var isValidBST = function(root) {
    
//     const stack = [[root, -Infinity, Infinity]]
    
//     let top
//     while (top = stack.pop()) {
//         const [node, min, max] = top
//         if (node === null) continue
//         if (node.val >= max || node.val <= min) return false
        
//         if (node.left) {
//             stack.push([node.left, min, Math.min(node.val, max)])
//         }
        
//         if (node.right) {
//             stack.push([node.right, Math.max(node.val, min), max])
//         }
//     }
    
//     return true
// };

// use in-order traversal => must lead to an asc array
// Time: O(n)
// Space: worst O(n)
var isValidBST = function(root) {
    const stack = [ ] 
    
    const push = (node) => {
        while(node) {
            stack.push(node)
            node = node.left
        }
    }
    
    let prev = -Infinity
    const collect = () => {
        let top
        while (top = stack.pop()) {
            if (top.val <= prev) return false
            prev = top.val
            if (top.right) {
                push(top.right)
            }
        }
        return true
    }
    
    push(root)
    return collect()
}
```
