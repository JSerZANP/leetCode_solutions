Here me explaining it on youtube: https://youtu.be/6c-ut2FijYo


```js
/**
 * Initialize your data structure here.
 */
var MyQueue = function() {
  // []
  // [1]
  // [1,2]
  // [1,2,3]
  // [1,2,3,4],  [ ]  => we cannot get 1 directly, but 4
  // [ ],    [4,3,2,1]
  // could use 2 stacks, one is for push, one is for pop
  
  this.pushStack = []
  this.popStack = []
};

/**
 * Push element x to the back of queue. 
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function(x) {
  this.pushStack.push(x)
};


MyQueue.prototype._transfer = function() {
  while(this.pushStack.length > 0) {
    this.popStack.push(this.pushStack.pop())
  }
}

/**
 * Removes the element from in front of queue and returns that element.
 * @return {number}
 */
MyQueue.prototype.pop = function() {
  if (this.empty()) return null
  
  if (this.popStack.length === 0) {
    this._transfer()
  }
  
  return this.popStack.pop()
};

/**
 * Get the front element.
 * @return {number}
 */
MyQueue.prototype.peek = function() {
  if (this.empty()) return null
  
  if (this.popStack.length === 0) {
    this._transfer()
  }
  
  return this.popStack[this.popStack.length - 1]
};

/**
 * Returns whether the queue is empty.
 * @return {boolean}
 */
MyQueue.prototype.empty = function() {
  return this.pushStack.length === 0 && this.popStack.length === 0
};

/** 
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
 ```
