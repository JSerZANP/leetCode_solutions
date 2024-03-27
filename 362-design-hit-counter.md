```js
var HitCounter = function () {
  // use a sliding window to keep track of the hit count in the last 5 minutes
  // since the timestamp i monotonic
  // we only need to maintain 5 items in an array

  this.buffer = [];
  this.count = 0;
};

/**
 * @param {number} timestamp
 * @return {void}
 */
HitCounter.prototype.hit = function (timestamp) {
  const buffer = this.buffer;
  if (buffer.length === 0) {
    buffer.push([timestamp, 1]);
    this.count = 1;
  } else if (timestamp === buffer[buffer.length - 1][0]) {
    buffer[buffer.length - 1][1] += 1;
    this.count += 1;
  } else {
    this.shift(timestamp);
    buffer.push([timestamp, 1]);
    this.count += 1;
  }
};

HitCounter.prototype.shift = function (timestamp) {
  const buffer = this.buffer;
  while (buffer.length > 0 && buffer[0][0] <= timestamp - 300) {
    this.count -= buffer[0][1];
    buffer.shift();
  }
};

/**
 * @param {number} timestamp
 * @return {number}
 */
HitCounter.prototype.getHits = function (timestamp) {
  this.shift(timestamp);
  return this.count;
};

/**
 * Your HitCounter object will be instantiated and called as such:
 * var obj = new HitCounter()
 * obj.hit(timestamp)
 * var param_2 = obj.getHits(timestamp)
 */
```
