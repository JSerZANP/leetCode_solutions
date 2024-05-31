Here is a video explaining this: https://youtu.be/g9RECnfohLE

```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// Time: O(n^2)
// space: O(n)
// var lengthOfLIS = function(nums) {
//   if (nums.length === 0) return 0
//   // 10,9,2,5,3,7,101,18

//   // optimal subarray, if 18 is in it
//   // LIS(i)
//   // LISEnd(I) is the longest incresing subarray length which end at i

//   // LISEND(i) = max {
//   //        LISTEND(j) + 1, j = 0 -> i - 1, if (nums[i] > nums[j])
//   //        -Infinity
//   // }

//   // LIS(i) = max { LISEND(I) }  i = 0 -> nums.length - 1

//   let result = 1

//   const LISEndAt = new Array(nums.length).fill(1)

//   for (let i = 1; i < nums.length; i++) {
//     LISEndAt[i] = Math.max(
//       1,
//       ...LISEndAt.slice(0, i).map((item, j) => {
//         return nums[i] > nums[j] ? item + 1 : 0
//       })
//     )

//     result = Math.max(LISEndAt[i], result)
//   }
//   return result
// }

var lengthOfLIS = function (nums) {
  if (nums.length === 0) return 0;
  // 10,9,2,5,3,7,101,18, 4, 19, 5 6 7,8

  // 2 3 4 5 6 7
  // 2 3 4 5 6
  // 2 3 4 5
  // 2 3 4
  // 2 3
  // 2

  //  2   10   11  5

  // 2
  // 2 5
  // 2 10 11

  // shorter optimozal subarray has a smaller ending

  // use a array to hold ending item at optimal subarray with length i
  const endings = [0, nums[0]];

  numLoop: for (let i = 1; i < nums.length; i++) {
    // binary search the right optimal length
    // binary search the insert position
    const num = nums[i];
    let start = 1;
    let end = endings.length - 1;

    while (start <= end) {
      const middle = Math.floor((start + end) / 2);
      if (endings[middle] === num) continue numLoop;

      if (endings[middle] > num) {
        end = middle - 1;
      } else {
        start = middle + 1;
      }
    }
    // start is the inserting position index
    // start means the length of the optimal
    const lengthOfOptimalSubArray = start;
    if (endings[lengthOfOptimalSubArray] === undefined) {
      endings[lengthOfOptimalSubArray] = num;
    } else {
      endings[lengthOfOptimalSubArray] = Math.min(
        endings[lengthOfOptimalSubArray],
        num
      );
    }
  }
  return endings.length - 1;
};
```

Another try at 2024

DP O(n^2)

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function (nums) {
  // suppose we've found the optima seq S at nums
  // if we add a new number
  // we actually need to check all the previous optimal seq ending at each index

  let max = 1;
  const longestUntil = new Array(nums.length).fill(1);

  for (let i = 1; i < nums.length; i++) {
    for (j = 0; j < i; j++) {
      if (nums[j] < nums[i]) {
        longestUntil[i] = Math.max(longestUntil[i], longestUntil[j] + 1);
        max = Math.max(max, longestUntil[i]);
      }
    }
  }
  return max;
};
```

Improved O(n logN)

```js
var lengthOfLIS = function (nums) {
  // 10
  // 10, 9 => 9
  // 9, 2 => 2
  // 2, 5 => candidate
  // 2, 5 3 => do we choose 3? for this case , yes, every thing that is larger than 5 also > 3
  // but if 2 8 9 10 3 4    11
  // 2 8 9 10 vs 3 => what we do?
  // we are not sure if there is going to be a better candidate seq
  // so we need to search and store a new se
  // [2 8 9 10] [ 2, 3, 4]
  // once there is a new number that is larget than both ends
  // then these could be merged again
  // what if there are more smaller end?
  // 2 8 9 10 5 6 3
  // [2 8 9 10] [2 5 6] [2 3]
  // it seems that we can actually use one array to hold them.
  // for the 2nd array, if somehow it reach 4 elements, and it is smaller ends, and the 1st seq should be removed
  // [2 8 9 10] 5 =>
  // [2 5 9 10]
  // [2 5 6 10]
  // [2 3 6 10]
  // current candidate only be dismissed when there is a new candidate shows up and has a smaller end.
  // so we can just replace it in the candidates array

  // start with [0, nums[0]]
  // for each round we search the insertion index
  // compare with the last item, if larger just push
  // if there is => replace it
  // if not => insert it

  // [10]
  // 9, => 0 [9]
  // 2, => [2]
  // [2, 5]
  // [2, 3, 7, 101]
  // [2, 3, 18, 101]

  let seq = [nums[0]];

  for (let j = 1; j < nums.length; j++) {
    const num = nums[j];
    if (num > seq.at(-1)) {
      seq.push(num);
    } else {
      const index = getInsertionIndex(seq, num);
      seq[index] = num;
    }
  }
  return seq.length;
};

function getInsertionIndex(list, item) {
  let i = 0;
  let j = list.length - 1;
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    if (list[m] === item) {
      return m;
    } else if (list[m] < item) {
      i = m + 1;
    } else {
      j = m - 1;
    }
  }

  // when  it stops i is the insertion index

  return i;
}
```
