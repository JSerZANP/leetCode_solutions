```js
/**
 * @param {number[][]} points
 * @return {number}
 */
var findMinArrowShots = function (points) {
  // [   ]
  ///  [ ]
  //       [       ]
  //          [        ]

  // after sorting it
  // we can actually merge interval by choosing the narrow one
  // [    ]
  //   [ ]
  // for above case, when the 2nd one is shot, the 1st is shot too
  // so it is equal this
  //   [ ]
  // For blow
  // [    ]
  //   [    ]
  // equals to
  //   [  ]
  // because if the 3rd one is
  // [    ]
  //   [    ]
  //     [   ]
  // then we can narrow it further
  // [    ]
  //   [    ]
  //       [   ]
  // then the first must shot, meaning we should shot the 2nd as well.
  // the problem comes, how many times we need ot flush the buffer
  // while merging the intervals
  points.sort((a, b) => a[0] - b[0]);
  let buffer = null;
  let count = 0;
  for (const interval of points) {
    if (buffer == null) {
      buffer = interval;
    } else {
      if (interval[0] > buffer[1]) {
        // shoot
        count += 1;
        buffer = interval;
      } else {
        buffer[0] = Math.max(buffer[0], interval[0]);
        buffer[1] = Math.min(buffer[1], interval[1]);
      }
    }
  }
  if (buffer != null) {
    count += 1;
  }
  return count;
};
```
