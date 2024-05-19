A video explaining this: https://youtu.be/4phx7g8QXVM

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
// Time: O(logN)
// Space: O(1)
var search = function (nums, target) {
  if (nums.length === 0) return -1;

  // [S1...Sk] [Sk+1...Sn]  1<= k <=n,   S1 > Sn
  let i = 0;
  let j = nums.length - 1;

  while (i <= j) {
    const middle = Math.floor((i + j) / 2);

    if (nums[middle] === target) {
      return middle;
    } else if (target < nums[middle]) {
      // S[j] < S[i] <= S[middle]
      // S[middle] <= S[j] < S[i]
      if (nums[middle] >= nums[i]) {
        if (target >= nums[i]) {
          j = middle - 1;
        } else {
          i = middle + 1;
        }
      } else {
        j = middle - 1;
      }
    } else {
      // S[j] < S[i] <= S[middle]
      // S[middle] <= S[j] < S[i]
      if (nums[middle] >= nums[i]) {
        i = middle + 1;
      } else {
        if (target > nums[j]) {
          j = middle - 1;
        } else {
          i = middle + 1;
        }
      }
    }
  }

  return -1;
};
```

Another try in 2024

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {
  // [     m    ] [  ]
  // [  ] [ m        ]

  // when we choose a mid
  // it might falls into the left bracket or the right bracket

  // when the target is bigger than mid
  // then we check if target might be on the left
  // pattern 1 => right hafl
  // pattern 2 => need further to check if it is bigger than right

  // when target is smaler
  // pattern 1 => need further to check if it is smaller than left
  // pattern 2 => left half

  let i = 0;
  let j = nums.length - 1;
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    if (nums[m] === target) {
      return m;
    }

    const bracketForMid = nums[m] > nums[j] ? "left" : "right";
    if (target > nums[m]) {
      if (bracketForMid === "left") {
        i = m + 1;
      } else {
        if (target > nums[j]) {
          j = m - 1;
        } else {
          i = m + 1;
        }
      }
    } else {
      if (bracketForMid === "left") {
        if (target < nums[i]) {
          i = m + 1;
        } else {
          j = m - 1;
        }
      } else {
        j = m - 1;
      }
    }
  }
  return -1;
};
```
