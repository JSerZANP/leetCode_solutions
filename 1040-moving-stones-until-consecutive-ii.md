A video explaining this: https://youtu.be/Hdtc-PCRmD4

```js

const getMax = (stones) => {
    // sum up the spaces
    // except case that only one endpoint at one side
    // o x x x o o o x x x x x x o
    const total = stones.length
    const sum = stones[total - 1] - stones[0] + 1 - total
    return sum - Math.min(stones[1] - stones[0] - 1, stones[total - 1] - stones[total - 2] - 1)
}


// o [ o o o] o
// [o o o x x]  o o 
// [o o o o x] o  ==> 1
// [o o o o x] x o ==> 2
// [o o o o x] x x o ==> 2
const getMin = (stones) => {
    let min = Infinity
    let left = 0
    let right = 0
    const total = stones.length
    // [o o o o x] x x o
    if (stones[total - 2] - stones[0] + 1 === total - 1) {
        return Math.min(2, stones[total - 1] - stones[total - 2] - 1)
    }
    
    // o x x x [ o o o o] 
    if (stones[total - 1] - stones[1] + 1 === total - 1) {
        return Math.min(2, stones[1] - stones[0] - 1)
    }
    
    // for all the other cases
    // we can safely suppose sliding window ends on stones
    for (; right < total; right++) {
        while (stones[right] - stones[left] + 1 > total) {
            left += 1
        }
        min = Math.min(min, total - (right - left + 1))
    }
    return min
}


/**
 * @param {number[]} stones
 * @return {number[]}
 */
var numMovesStonesII = function(stones) {
    stones.sort((a, b) => a - b)
    return [getMin(stones), getMax(stones)]
};
```
