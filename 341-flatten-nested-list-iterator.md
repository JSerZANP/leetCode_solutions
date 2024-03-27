```js
/**
 * @constructor
 * @param {NestedInteger[]} nestedList
 */
var NestedIterator = function (nestedList) {
  this.stack = [];
  this.flatten(nestedList);
};

/**
 * @this NestedIterator
 * @returns {boolean}
 */
NestedIterator.prototype.hasNext = function () {
  return this.stack.length > 0;
};

NestedIterator.prototype.flatten = function (nestedList) {
  const queue = [nestedList];
  while (queue.length > 0) {
    const top = queue.pop();
    if (Array.isArray(top)) {
      queue.push(...top);
    } else if (top.isInteger()) {
      this.stack.push(top.getInteger());
    } else {
      queue.push(...top.getList());
    }
  }
};

/**
 * @this NestedIterator
 * @returns {integer}
 */
NestedIterator.prototype.next = function () {
  return this.stack.pop();
};

/**
 * Your NestedIterator will be called like this:
 * var i = new NestedIterator(nestedList), a = [];
 * while (i.hasNext()) a.push(i.next());
 */
```
