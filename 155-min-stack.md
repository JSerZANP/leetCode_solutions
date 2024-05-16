```js
var MinStack = function () {
  // Map, Set, Array
  this.stack = [];
  this.minStack = [];
};

/**
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function (val) {
  this.stack.push(val);
  if (this.minStack.length === 0) {
    this.minStack.push(val);
  } else {
    this.minStack.push(Math.min(this.minStack.at(-1), val));
  }
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function () {
  // all are fine
  this.stack.pop();
  this.minStack.pop();
};

/**
 * @return {number}
 */
MinStack.prototype.top = function () {
  return this.stack.at(-1);
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function () {
  // min
  // when to update minimum?
  // if to update when pop, we need to know next minimum
  // it means we need a sorted data structure?
  // or we can just store the next minimum because
  // the popping of the list is just one direction.
  return this.minStack.at(-1);
};

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(val)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```
