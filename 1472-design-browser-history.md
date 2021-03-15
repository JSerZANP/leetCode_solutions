Hear me expalaining it on youtube: https://youtu.be/FcXFVLyjU0k

```js
/**
 * @param {string} homepage
 */
var BrowserHistory = function(homepage) {
    // [1]
    // [1,2]
    // [1,2,3]
    // [1,2(o), 3]
    // [1,2, 4(0)]
    
    this.histories = [homepage]
    this.currentIndex = 0
};

/** 
 * @param {string} url
 * @return {void}
 */
BrowserHistory.prototype.visit = function(url) {
  this.histories.length = this.currentIndex + 1
  this.histories.push(url)
  this.currentIndex += 1
};

/** 
 * @param {number} steps
 * @return {string}
 */
BrowserHistory.prototype.back = function(steps) {
  const newIndex = Math.max(0, this.currentIndex - steps)
  this.currentIndex = newIndex
  return this.histories[newIndex]
};

/** 
 * @param {number} steps
 * @return {string}
 */
BrowserHistory.prototype.forward = function(steps) {
  const newIndex = Math.min(this.histories.length - 1, this.currentIndex + steps)
  this.currentIndex = newIndex
  return this.histories[newIndex]
};

/** 
 * Your BrowserHistory object will be instantiated and called as such:
 * var obj = new BrowserHistory(homepage)
 * obj.visit(url)
 * var param_2 = obj.back(steps)
 * var param_3 = obj.forward(steps)
 */
```
