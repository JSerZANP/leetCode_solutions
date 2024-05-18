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
var BSTIterator = function (root) {
  // do in-order traversal
  // store the in-order form of tree in an array

  const walk = (node, arr) => {
    if (node === null) return arr;
    if (node.left) walk(node.left, arr);
    arr.push(node);
    if (node.right) walk(node.right, arr);
    return arr;
  };

  this.inorder = walk(root, []);
  this.current = -1;
};

/**
 * @return the next smallest number
 * @return {number}
 */
BSTIterator.prototype.next = function () {
  this.current += 1;
  return this.inorder[this.current].val;
};

/**
 * @return whether we have a next smallest number
 * @return {boolean}
 */
BSTIterator.prototype.hasNext = function () {
  if (this.current === this.inorder.length - 1) {
    return false;
  }
  return true;
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * var obj = new BSTIterator(root)
 * var param_1 = obj.next()
 * var param_2 = obj.hasNext()
 */
```

Another try, use generator

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
var BSTIterator = function (root) {
  function* dfs(node) {
    const stack = [root];
    while (stack.length > 0) {
      const top = stack.pop();
      // a node needs to be popped twice
      // in order to tell the difference
      // we need to duplicate the node when it is pushed again
      if (stack.at(-1) === top) {
        // the second time it is processed
        stack.pop();
        yield top.val;
        continue;
      }

      // leaf node
      if (top.left == null && top.right == null) {
        yield top.val;
        continue;
      }

      // if no left
      if (top.right) {
        stack.push(top.right);
      }

      if (top.left) {
        stack.push(top);
        stack.push(top);
        stack.push(top.left);
      } else {
        yield top.val;
      }
    }
  }
  this.gen = dfs(root);
  this.nextValue = this.gen.next();
};

/**
 * @return {number}
 */
BSTIterator.prototype.next = function () {
  const nextValue = this.nextValue;
  this.nextValue = this.gen.next();
  return nextValue.value;
};

/**
 * @return {boolean}
 */
BSTIterator.prototype.hasNext = function () {
  return !this.nextValue.done;
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * var obj = new BSTIterator(root)
 * var param_1 = obj.next()
 * var param_2 = obj.hasNext()
 */
```
