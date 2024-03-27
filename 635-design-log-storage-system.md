```js
var LogSystem = function () {
  // time string could be compared directly.
  // we can sort the logs by timestamp
  // use binary search to find the index

  // sort we can use quick sort
  // or insertion sort?
  // both will be O(nlogn)

  this.logs = [];
  this.ids = new Map();
};

/**
 * @param {number} id
 * @param {string} timestamp
 * @return {void}
 */
LogSystem.prototype.put = function (id, timestamp) {
  if (!this.ids.has(id)) {
    this.ids.set(id, new Set());
  }

  if (!this.ids.get(id).has(timestamp)) {
    this.ids.get(id).add(timestamp);
    this.logs.push([id, timestamp]);
    this.logs.sort((a, b) => {
      if (a[1] === b[1]) return 1;
      return a[1] < b[1] ? -1 : 1;
    });
  }
};

/**
 * @param {string} start
 * @param {string} end
 * @param {string} granularity
 * @return {number[]}
 */
const indexOfGranularity = "Year:Month:Day:Hour:Minute:Second"
  .split(":")
  .reduce((result, item, index) => {
    result[item] = index;
    return result;
  }, {});
LogSystem.prototype.retrieve = function (start, end, granularity) {
  const compare = (t1, t2) => {
    if (t1 === t2) return 0;
    let segs1 = t1.split(":");
    let segs2 = t2.split(":");
    for (let i = 0; i <= indexOfGranularity[granularity]; i++) {
      if (segs1[i] > segs2[i]) {
        return 1;
      } else if (segs1[i] < segs2[i]) {
        return -1;
      }
    }
    return 0;
  };

  // binary search the start => the first item >= start
  // binary search the end => the last item <= end
  const startIndex = this.logs.findIndex(
    (item) => compare(item[1], start) >= 0
  );
  const endIndex = this.logs.findLastIndex(
    (item) => compare(item[1], end) <= 0
  );
  if (startIndex === -1) return [];
  if (endIndex === -1) return [];

  return this.logs.slice(startIndex, endIndex + 1).map((item) => item[0]);
};

/**
 * Your LogSystem object will be instantiated and called as such:
 * var obj = new LogSystem()
 * obj.put(id,timestamp)
 * var param_2 = obj.retrieve(start,end,granularity)
 */
```
