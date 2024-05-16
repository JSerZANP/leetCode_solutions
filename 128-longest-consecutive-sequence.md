```js
/**
 * @param {number[]} nums
 * @return {number}
 */
//  O(N) -> for each move we'll remove one item from the set
// O(N)
var longestConsecutive = function (nums) {
  // for each number
  // we can get the streak it belongs
  // by +1/-1
  const set = new Set(nums);
  let streak = 0;

  for (const num of nums) {
    set.delete(num);
    let start = num;
    let end = num;
    while (set.has(end + 1)) {
      end += 1;
      set.delete(end);
    }
    while (set.has(start - 1)) {
      start -= 1;
      set.delete(start);
    }

    streak = Math.max(streak, end - start + 1);
  }

  return streak;
};
```
