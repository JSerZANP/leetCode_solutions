Me explaining this on youtube: https://youtu.be/F9DhnbNB9LM


```js
/**
 * @param {number} capacity
 */
var LRUCache = function(capacity) {
    // 1, 2
    // 2, 1
    // [2, ] 1, 3
    // [1, ] 3, 4
  
  
     // [1, 2, 3]
  
     // 1. search for the 2, O(n), or store the index directly to the map O(1)
     // 2. splice it O(n)
     // 3. push at the end O(1)
     // O(n)
  
     // head <-> 1 <-> 2 <-> 3 <-> 4 <-> 2
     // 1. search the node from Map<key, [node, val]> O(1)
     // 2. splice it, O(1)
     // 3. move to the end, O(1) by remembering last node. 
      
      // use two-way linked list + pointer to last node.
      
  
    // use a Map<key, value>
    // Map in JS keeps the order
    this.capacity = capacity
    this.map = new Map()
};

/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function(key) {
    if (this.map.has(key)) {
      const val = this.map.get(key)
      this.map.delete(key)
      this.map.set(key, val)
      return val
    } else {
      return -1
    }
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function(key, value) {
    // if key exist, update
    const prevVal = this.get(key)
    if (prevVal === -1) {
      if (this.map.size === this.capacity) {
        for (let [firstKey] of this.map) {
          this.map.delete(firstKey)
          break
        }
      }
      
    }
    this.map.set(key, value)
};

/** 
 * Your LRUCache object will be instantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */
 ```
