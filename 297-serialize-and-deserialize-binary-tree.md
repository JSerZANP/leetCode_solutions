A video explaining this: https://youtu.be/BdYiijeQ680

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */

/**
 * Encodes a tree to a single string.
 *
 * @param {TreeNode} root
 * @return {string}
 */
var serialize = function(root) {
    const result = []
    
    const walk = (node) => {
        if (node === null) {
            result.push(null)
            return
        } else {
            result.push(node.val)
        }
        
        walk(node.left)
        walk(node.right)
    }
    
    walk(root)
    
    return JSON.stringify(result)
};

/**
 * Decodes your encoded data to tree.
 *
 * @param {string} data
 * @return {TreeNode}
 */
var deserialize = function(data) {
    if (!data) {
        return null
    }
    
    const arr = JSON.parse(data)
    
    if (arr.length === 0 || arr[0] === null) {
        return null
    }
    
    const build = () => {
        const item = arr.shift()
        if (item === null) {
            return null
        }
        const node = new TreeNode(item)
        node.left = build()
        node.right = build()
        return node
    }
    
    const root = build(0)
    
    return root
};

/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */
 ```
