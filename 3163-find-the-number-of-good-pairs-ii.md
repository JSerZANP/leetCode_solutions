```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number}
 */

// O(mn) TLE => O(n^2)
// var numberOfPairs = function(nums1, nums2, k) {
//     let result = 0
//     nums1.forEach((a) => {
//         nums2.forEach((b) => {
//             if (b * k !== 0 && a % (b * k) === 0) {
//                 result += 1
//             }
//         })
//     })
//     return result
// };

var numberOfPairs = function (nums1, nums2, k) {
  // if we think divisible => 1, k => 1
  // it'll be a search problem and use a Set => O(n)

  // divisbable a / b => the factors b * x = a
  // if we spread a by its factors
  // factor array of nums1 => O(n) + O(n * sqrt(n)) , space upper boundary: O(sqrt(10^5))

  const factorList = nums1.map(getFactor);
  const nums2Map = new Map();
  for (const num of nums2) {
    nums2Map.set(num * k, (nums2Map.get(num * k) ?? 0) + 1);
  }
  let result = 0;
  for (const factors of factorList) {
    factors.forEach((factor) => {
      if (nums2Map.has(factor)) {
        result += nums2Map.get(factor);
      }
    });
  }
  return result;
};

function getFactor(num) {
  const result = [];
  let i = 1;
  while (i ** 2 <= num) {
    if (num % i === 0) {
      result.push(i);
      result.push(num / i);
    }
    i += 1;
  }
  return new Set(result);
}
```

Maybe we don't need to dedup first?

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number}
 */

// O(mn) TLE => O(n^2)
// var numberOfPairs = function(nums1, nums2, k) {
//     let result = 0
//     nums1.forEach((a) => {
//         nums2.forEach((b) => {
//             if (b * k !== 0 && a % (b * k) === 0) {
//                 result += 1
//             }
//         })
//     })
//     return result
// };

var numberOfPairs = function (nums1, nums2, k) {
  // if we think divisible => 1, k => 1
  // it'll be a search problem and use a Set => O(n)

  // divisbable a / b => the factors b * x = a
  // if we spread a by its factors
  // factor array of nums1 => O(n) + O(n * sqrt(n)) , space upper boundary: O(sqrt(10^5))

  const nums2Map = new Map();
  for (const num of nums2) {
    nums2Map.set(num * k, (nums2Map.get(num * k) ?? 0) + 1);
  }
  let result = 0;
  for (const num of nums1) {
    for (let i = 1; i ** 2 <= num; i++) {
      if (num % i === 0) {
        if (nums2Map.has(i)) {
          result += nums2Map.get(i);
        }
        const j = num / i;
        if (j !== i && nums2Map.has(j)) {
          result += nums2Map.get(j);
        }
      }
    }
  }

  return result;
};
```
