Here is my video explaining it : https://youtu.be/nei1-vf2WmU

```js
/**
 * Initialize your data structure here.
 */
var Logger = function() {
    // Map<message, time>
    this.printed = new Map()
};

/**
 * Returns true if the message should be printed in the given timestamp, otherwise returns false.
        If this method returns false, the message will not be printed.
        The timestamp is in seconds granularity. 
 * @param {number} timestamp 
 * @param {string} message
 * @return {boolean}
 */
Logger.prototype.shouldPrintMessage = function(timestamp, message) {
    if (this.printed.has(message)) {
      const last = this.printed.get(message)
      if (timestamp - last < 10) {
        return false
      }
    }
  
    this.printed.set(message, timestamp)
    return true
};

/** 
 * Your Logger object will be instantiated and called as such:
 * var obj = new Logger()
 * var param_1 = obj.shouldPrintMessage(timestamp,message)
 */
 ```
