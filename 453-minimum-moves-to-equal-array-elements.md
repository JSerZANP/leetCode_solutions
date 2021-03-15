A video explaining this: https://youtu.be/Hl3TivVZ9ME

```js
 /*
 * @param {number[]} nums
 * @return {number}
 */
var minMoves = function(nums) {
    let min = Number.POSITIVE_INFINITY
    let sum = 0
    
    for (let num of nums) {
        sum += num
        if (num < min) {
            min = num
        }
    }

    return sum - nums.length * min
};
```
