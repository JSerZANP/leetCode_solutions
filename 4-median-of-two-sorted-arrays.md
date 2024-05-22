```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function (nums1, nums2) {
  // choose the number of median m1, and m2
  // the real median might be m1, or [m1, m1 + 1]

  // our goal is the search the m3 from the list
  // it is not get median anymore
  // [  ]  [  ]
  // binary search
  // [ A1 ] [m1 A2]
  //      [ B1 ] [m2  B2 ]

  // if k >= half the length
  // we can safely drop A1
  // if k < half of the length, we can safely drop b2

  // until there is only one element in both array

  // for the drop, we can just maintain a final range

  const size = nums1.length + nums2.length;
  const median = Math.floor((size - 1) / 2);

  if (size % 2 === 1) {
    if (nums1.length === 0) return nums2[median];
    if (nums2.length === 0) return nums1[median];
    return getKthNumber(nums1, nums2, median);
  } else {
    if (nums1.length === 0) return (nums2[median] + nums2[median + 1]) / 2;
    if (nums2.length === 0) return (nums1[median] + nums1[median + 1]) / 2;

    const left = getKthNumber(nums1, nums2, median);
    const right = getKthNumber(nums1, nums2, median + 1);
    return (left + right) / 2;
  }
};

function getKthNumber(nums1, nums2, k) {
  let range1 = [0, nums1.length - 1];
  let range2 = [0, nums2.length - 1];

  // is this solid?
  // what if there is only 1 element
  // / [ m1 ]
  //      [ B1 ] [m2  B2 ]
  // can we remove the m1?
  // no [1, 4] [3] for this, we cannot remove right half 3, because there is none
  while (k > 0 && range1[1] - range1[0] > 0 && range2[1] - range2[0] > 0) {
    const median1 = Math.floor((range1[0] + range1[1]) / 2);
    const median2 = Math.floor((range2[0] + range2[1]) / 2);

    // check if k should be on the larger half or smaller half
    // median1 are put on the left
    // so that we can split even when there is only two numbers

    const leftCount1 = median1 - range1[0] + 1;
    const leftCount2 = median2 - range2[0] + 1;
    const rightCount1 = range1[1] - median1;
    const rightCount2 = range2[1] - median2;
    if (k + 1 > leftCount1 + leftCount2) {
      if (nums1[median1] <= nums2[median2]) {
        range1[0] = median1 + 1;
        k -= leftCount1;
      } else {
        range2[0] = median2 + 1;
        k -= leftCount2;
      }
    } else {
      if (nums1[median1] <= nums2[median2]) {
        range2[1] = median2;
      } else {
        range1[1] = median1;
      }
    }
  }

  if (k === 0) {
    return Math.min(nums1[range1[0]], nums2[range2[0]]);
  }

  // in the end one of the ranges will be one item
  if (range1[1] === range1[0]) {
    const index = getIndex(nums2, range2, nums1[range1[0]]);
    // there is going to be a new num at index
    // if inserted after, then it's fine
    if (k + range2[0] < index) {
      return nums2[k + range2[0]];
      // if inserted at the right position, then use the smaller one
    } else if (k + range2[0] === index) {
      return nums1[range1[1]];
      // if inserted before the position
    } else {
      return nums2[k + range2[0] - 1];
    }
  }

  if (range2[1] === range2[0]) {
    const index = getIndex(nums1, range1, nums2[range2[0]]);
    // there is going to be a new num at index
    if (k + range1[0] < index) {
      return nums1[k + range1[0]];
    } else if (k + range1[0] === index) {
      return nums2[range2[1]];
    } else {
      return nums1[k + range1[0] - 1];
    }
  }
}

function getIndex(nums, range, num) {
  let i = range[0];
  let j = range[1];
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    if (nums[m] === num) {
      return m;
    } else if (nums[m] < num) {
      i = m + 1;
    } else {
      j = m - 1;
    }
  }

  // when stops, i should be the index of num
  return i;
}
```
