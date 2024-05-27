```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number[][]}
 */
var kSmallestPairs = function (nums1, nums2, k) {
  // we can find all the pairs and sort
  // pairs = mn
  // sort O(mn log(mn)) O(n)

  // but sort doesn't take advantage of the fact that both arry are already sorted

  // if one of the array has only 1 item
  // [a1, b1, c1, d1] [a2]
  // [a1 + a2, b1 + a2, c1 + a2, d1 + a2] => [l1, l2, l3, l4]

  // now if we have two items
  // // [a1, b1, c1, d1] [a2, b2]
  // we have extra pairs of [a1 + b2, b1 + b2, c1 + b2, d1 + b2] => [m1, m2, m3, m4]
  // we see that l1 < m1 , l2 < m2, l3 < m3, l4 < m4
  // but l2, m1 we don't know which is bigger

  // since the sum arrays are sorted as well, we can do merge sort

  // m , n
  // the problem becomes the m lists of item n to merge
  // we can user merge sort, two at a time
  // for each item they are to be merge logM times
  // so time: O(mnlogM), space O(mn)

  // this is still not efficient because we don't need to sort all of the items
  // we only want k of them.

  // is there a way we can return only k items without sorting the rest?
  // [1,7,11] [2,4,6]
  // obviously the smallest is [1, 2]
  // the next must be [1, 4] or [2, 7] => [1, 4]
  // the next must be [1, 6] or [2, 7] => [1, 6], 1 is gone
  // the next must be [2, 7]
  // [2, 11] [7, 4]
  // [2, 11] [7, 6], [4, 11]

  // so every turn we choose a pair, we can determine the candidates
  // and we can just sort them, they are already sorted.
  // we can use a priority queue to hold the candidates
  // every round we push item in the pq and poll out

  // push/poll logK
  // k element KlogK
  const pq = new PriorityQueue({
    compare(a, b) {
      const sumA = nums1[a[0]] + nums2[a[1]];
      const sumB = nums1[b[0]] + nums2[b[1]];
      if (sumA < sumB) {
        return -1;
        // attention to the sub ordering
      } else if (sumA === sumB) {
        if (nums1[a[0]] === nums1[b[0]]) {
          return nums2[a[1]] - nums2[b[1]];
        } else if (a[0] < b[0]) {
          return -1;
        } else {
          return 1;
        }
      } else {
        return 1;
      }
    },
  });

  pq.enqueue([0, 0]);
  const candidates = new Set();
  let result = [];
  candidates.add(`0_0`);

  while (pq.size() > 0) {
    const head = pq.dequeue();
    result.push([nums1[head[0]], nums2[head[1]]]);
    if (result.length === k) return result;

    // push the next candidate if we want more
    if (head[0] + 1 < nums1.length) {
      const key = `${head[0] + 1}_${head[1]}`;
      if (!candidates.has(key)) {
        candidates.add(key);
        pq.enqueue([head[0] + 1, head[1]]);
      }
    }
    if (head[1] + 1 < nums2.length) {
      const key = `${head[0]}_${head[1] + 1}`;
      if (!candidates.has(key)) {
        candidates.add(key);
        pq.enqueue([head[0], head[1] + 1]);
      }
    }
  }
};
```
