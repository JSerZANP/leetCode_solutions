
Here is a video explaining: https://www.youtube.com/watch?v=cjEB3juHSZg
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
 * @return {void} Do not return anything, modify root in-place instead.
 */

// O(dep) O(n)
var recoverTree = function(root) {
    // target the swapped nodes
    // BST inorder traversal on BST leads to an asc array
    // [1,2,3] => [3,2,1]
    // [1,2,3,4] => [1,3,2,4]
    // [1,2,3,4,5,6] => [5,2,3,4,1,6]
    // [6,2,3,4,5,1]
    // [1,2,4,3,5,6]
    // target the first swapped node where next one is smaller => first node
    // target the next sapped node, where prev one is bigger => the last
    
    // keep track of the previous node and compare
    
    let prev = null
    let first = null
    let second = null
    
    const walk = (node) => {
        if (node === null) return
        if (node.left) {
            walk(node.left)
        }
        
        if (prev?.val > node.val) {
            if (first === null) {
                first = prev    
            }
            
            second = node
        }
        
        prev = node
    
        if (node.right) {
            walk(node.right)
        }  
    }

    walk(root);

    [first.val, second.val] = [second.val, first.val]
    
};
```
