```js
var TweetCounts = function () {
  this.map = new Map();
};

/**
 * @param {string} tweetName
 * @param {number} time
 * @return {void}
 */
TweetCounts.prototype.recordTweet = function (tweetName, time) {
  if (!this.map.has(tweetName)) {
    this.map.set(tweetName, new Map());
  }
  const timeMap = this.map.get(tweetName);
  timeMap.set(time, timeMap.has(time) ? timeMap.get(time) + 1 : 1);
};

/**
 * @param {string} freq
 * @param {string} tweetName
 * @param {number} startTime
 * @param {number} endTime
 * @return {number[]}
 */
TweetCounts.prototype.getTweetCountsPerFrequency = function (
  freq,
  tweetName,
  startTime,
  endTime
) {
  const timeMap = this.map.get(tweetName);
  const step = getStep(freq);
  const recoredTimes = timeMap ? [...timeMap?.keys()] : [];
  const result = [];
  while (startTime <= endTime) {
    const matchedRecoredTimes = recoredTimes.filter(
      (time) =>
        time >= startTime && time <= Math.min(endTime, startTime + step - 1)
    );
    const count = matchedRecoredTimes.reduce((result, time) => {
      return result + timeMap.get(time);
    }, 0);
    result.push(count);
    startTime += step;
  }
  return result;
};

function getStep(freq) {
  if (freq === "minute") {
    return 60;
  }
  if (freq === "hour") {
    return 60 * 60;
  }
  if (freq === "day") {
    return 60 * 60 * 24;
  }
  throw new Error("unknow freq " + freq);
}

/**
 * Your TweetCounts object will be instantiated and called as such:
 * var obj = new TweetCounts()
 * obj.recordTweet(tweetName,time)
 * var param_2 = obj.getTweetCountsPerFrequency(freq,tweetName,startTime,endTime)
 */
```
