## 1. naive counting

O(n) O(n)

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
// O(n), O(n)
// var majorityElement = function(nums) {
//     // count it?
//     let count = new Map()
//     for (const num of nums) {
//         const c = count.get(num) ?? 0
//         if (c + 1 >= nums.length / 2) {
//             return num
//         }
//         count.set(num, c + 1)
//     }
// };
```

## 2. O(1) space approach by removing elements by pairs

```js
// for a majority element
// if we remove one majority and one minority, then the majority is still the majority element
// if we remove one minority and one minority, then majority is still the majority element.
// so as long as we remove two differnt elements, then majority won't change!
// 2 => candidate
// 2 => 2 * 2
// 1 => different, remove a pair 2 * 1
// 1 => differnet , remove a pair null
// 1 => 1 * 1
// 2 => different, remove a pair null
// 2 => 2
// so 2 is the majority

// what if [2, 2, 3, 3, 2, 3,3]
// 2 *1
// 2 * 2
// 2 * 1
// null
// 2 * 1
// null
var majorityElement = function (nums) {
  let candidate = nums[0];
  let count = 1;
  for (let i = 1; i < nums.length; i++) {
    if (count === 0) {
      candidate = nums[i];
      count = 1;
    } else {
      if (nums[i] === candidate) {
        count += 1;
      } else {
        count -= 1;
      }
    }
  }
  return candidate;
};
```
