Youtube video explaining this: https://youtu.be/Mqd_ZPcljT8


```js

const minMoves = (a, b, c) => {
    return Math.min(b - a - 1, 1) + Math.min(c - b - 1, 1);
}

const maxMoves = (a, b, c) => {
    return b - a - 1 + c - b - 1;
}

/**
 * @param {number} a
 * @param {number} b
 * @param {number} c
 * @return {number[]}
 */
var numMovesStones = function(a, b, c) {
    const input = [a,b,c].sort((a, b) => a - b)
    const result = [
        minMoves(input[0], input[1], input[2]),
        maxMoves(input[0], input[1], input[2])
    ]
    
    if (input[2] > input[1] + 1) {
        result[0] = Math.min(result[0], minMoves(input[1], input[1] + 1, input[2]) + 1);
    }
    
    if (input[1] > input[0] + 1) {
        result[0] = Math.min(result[0], minMoves(input[0], input[0] + 1, input[1]) + 1);
    }
    
    return result;
};
```
