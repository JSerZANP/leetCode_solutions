
Here is my video explaining it: https://youtu.be/YUo_iuIgyyU

```js
/**
 * Initialize your data structure here.
 */
var RandomizedSet = function() {
    // Set -> insert O(1)  remove O(1),  getRandom x
    // Array -> getRandom() O(1)  insert O(1) remove O(N)
  
    // use Array,  but try to improve removal to O(1)
    // use extra Map to help
  
    // [1, 2, 3, 4]
    // use Map to store index, Map<Num, index>
    // swap node with the rare, pop at O(1)
  
    this.nums = []
    this.indexes = new Map()
};

/**
 * Inserts a value to the set. Returns true if the set did not already contain the specified element. 
 * @param {number} val
 * @return {boolean}
 */
RandomizedSet.prototype.insert = function(val) {
    if (this.indexes.get(val) !== undefined) return false
  
    const index = this.nums.length
    this.nums.push(val)
    this.indexes.set(val, index)
  
    return true
};

/**
 * Removes a value from the set. Returns true if the set contained the specified element. 
 * @param {number} val
 * @return {boolean}
 */
RandomizedSet.prototype.remove = function(val) {
    const index = this.indexes.get(val)
    if (index === undefined) return false
    // swap
    const length = this.nums.length
    const lastNum = this.nums[length - 1]
    this.nums[index] = lastNum
    this.nums[length - 1] = val
    this.nums.pop()

    this.indexes.set(lastNum, index)
    this.indexes.delete(val)
    return true
};

/**
 * Get a random element from the set.
 * @return {number}
 */
RandomizedSet.prototype.getRandom = function() {
    const index = Math.floor(Math.random() * this.nums.length)
    return this.nums[index]
};

/** 
 * Your RandomizedSet object will be instantiated and called as such:
 * var obj = new RandomizedSet()
 * var param_1 = obj.insert(val)
 * var param_2 = obj.remove(val)
 * var param_3 = obj.getRandom()
 */
```
