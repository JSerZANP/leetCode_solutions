```js
/**
 * @param {number} days
 * @param {number[][]} meetings
 * @return {number}
 */
var countDays = function (days, meetings) {
  // sor the meetings and merge them
  // then just collect in one pass
  meetings.sort((a, b) => a[0] - b[0]);
  const merged = [];
  let buffer = null;
  for (const meeting of meetings) {
    // meetings are sorted

    // if no overlap
    if (buffer == null) {
      buffer = meeting;
      continue;
    }
    if (buffer[1] < meeting[0]) {
      merged.push(buffer);
      buffer = meeting;
    } else {
      // overlap
      buffer[1] = Math.max(buffer[1], meeting[1]);
    }
  }
  if (buffer != null) {
    merged.push(buffer);
  }

  let result = 0;
  let prevMeetingEndDay = 0;
  for (const meeting of merged) {
    result += meeting[0] - prevMeetingEndDay - 1;
    prevMeetingEndDay = meeting[1];
  }
  result += days - prevMeetingEndDay;

  return result;
};
```
