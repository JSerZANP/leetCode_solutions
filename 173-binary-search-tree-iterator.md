Watch my video for this problem: https://youtu.be/Mr-PN0ljetw

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
 */
var BSTIterator = function(root) {
    // do in-order traversal
    // store the in-order form of tree in an array
    
    const walk = (node, arr) => {
      if (node === null) return arr
      if (node.left) walk(node.left, arr)
      arr.push(node)
      if (node.right) walk(node.right, arr)
      return arr
    }
    
    this.inorder = walk(root, [])
    this.current = -1 
};

/**
 * @return the next smallest number
 * @return {number}
 */
BSTIterator.prototype.next = function() {
    this.current += 1
    return this.inorder[this.current].val
};

/**
 * @return whether we have a next smallest number
 * @return {boolean}
 */
BSTIterator.prototype.hasNext = function() {
  if (this.current === this.inorder.length - 1) {
    return false
  }
  return true
};

/** 
 * Your BSTIterator object will be instantiated and called as such:
 * var obj = new BSTIterator(root)
 * var param_1 = obj.next()
 * var param_2 = obj.hasNext()
 */
```
