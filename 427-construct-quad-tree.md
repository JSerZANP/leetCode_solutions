```js
/**
 * // Definition for a QuadTree node.
 * function Node(val,isLeaf,topLeft,topRight,bottomLeft,bottomRight) {
 *    this.val = val;
 *    this.isLeaf = isLeaf;
 *    this.topLeft = topLeft;
 *    this.topRight = topRight;
 *    this.bottomLeft = bottomLeft;
 *    this.bottomRight = bottomRight;
 * };
 */

/**
 * @param {number[][]} grid
 * @return {Node}
 */
var construct = function (grid) {
  // map reduce?
  // for a grid defined by (x, y, size)
  // we can divide it into 4 areas
  // then create 4 nodes from them

  // divide and conquer
  // until size === 1
  // then it is very easy.

  const impl = (x, y, size) => {
    if (size === 1) {
      return new Node(grid[x][y], 1);
    }

    const subGridSize = size / 2;

    const topLeft = impl(x, y, size / 2);
    const topRight = impl(x, y + size / 2, size / 2);
    const bottomLeft = impl(x + size / 2, y, size / 2);
    const bottomRight = impl(x + size / 2, y + size / 2, size / 2);
    if (
      topRight.val === topLeft.val &&
      bottomLeft.val === topLeft.val &&
      bottomRight.val === topLeft.val
    ) {
      return new Node(topLeft.val, 1);
    }
    // attention here needs to be not 0 nor 1
    return new Node(NaN, 0, topLeft, topRight, bottomLeft, bottomRight);
  };

  const result = impl(0, 0, grid.length);
  return result;
};
```
