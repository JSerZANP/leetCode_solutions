## 1. BF

```js
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
// BFL O(n^2)
// var canCompleteCircuit = function(gas, cost) {
//     outer: for (let i = 0; i < gas.length; i++) {
//         // try from index
//         let start = i
//         let tank = gas[start]
//         while (true) {
//             if (tank >= cost[start]) {
//                 const next = (start + 1) % gas.length
//                 tank = tank - cost[start] + gas[next]
//                 start  = next
//             } else {
//                 continue outer;
//             }

//             if (start === i) {
//                 return i
//             }
//         }
//     }
//     return -1
// };
```

## 2. avoid duplicate checks

```js
// there a repeated check from one gas station to next
// but with differeng gas amount

// if we start from a station, following is the gas profit
// [-2, -2, -2, 3, 3]

// if they cannot add up to >= 0, then it cannot be completed
// if they can, then definite we can start with the first
// positive. and we can start check from there

var canCompleteCircuit = function (gas, cost) {
  let len = gas.length;
  let sum = 0;
  let profit = [];
  for (let i = 0; i < gas.length; i++) {
    sum += gas[i];
    profit.push(gas[i] - cost[i]);
  }

  if (sum < 0) return -1;

  // we can loop through each index
  // we accumulative the sum
  // once it becomes negative we skip all of them
  // [ 1, -3, 1, -2, 3 ]
  // 1
  // -2,
  // 1
  // -1
  // 3
  // 4
  // 1
  for (let start = 0; start < len; start++) {
    let i = start;
    let tank = profit[start];
    while (tank >= 0) {
      const next = (i + 1) % len;
      tank += profit[next];
      i = next;
      if (i === start && tank >= 0) {
        return start;
      }
    }
    // if not found, tank is negative
    if (i < start) {
      return -1;
    }

    start = i;
  }

  return -1;
};
```

Another try

```js
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
var canCompleteCircuit = function (gas, cost) {
  // [2, 3, 4], cost = [3,4, 3]
  // [-1, -1, 1]

  const profit = gas.map((amount, i) => amount - cost[i]);
  let tank = 0; // 1
  let i = 0; // 2
  while (i < profit.length) {
    let start = i;
    let j = start; //
    while (true) {
      tank += profit[j]; // -1
      if (tank < 0) {
        start = j + 1;
        tank = 0;
        break;
      }

      j = (j + 1) % profit.length;

      if (j === start) {
        return j;
      }
    }
    if (start <= i) {
      break;
    }
    i = start;
  }
  return -1;
};
```
