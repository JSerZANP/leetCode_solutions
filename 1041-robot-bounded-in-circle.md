youtube video explaining this: https://youtu.be/HTDfnhZHNN8

```js
/**
 * @param {string} instructions
 * @return {boolean}
 */
var isRobotBounded = function(instructions) {
    let direction = [0, 1]
    let pos = [0, 0]
    
    for (let i = 0, total = instructions.length; i < total; i++) {
        const instruction = instructions[i]
        if (instruction === 'G') {
            pos[0] += direction[0]
            pos[1] += direction[1]
        } else if (instruction === 'L') {
            [direction[0], direction[1]] = [-direction[1], direction[0]]
        } else {
            [direction[0], direction[1]] = [direction[1], -direction[0]]
        }
    }
    
    // if we are still at the origin
    if (pos[0] === 0 && pos[1] === 0) {
        return true
    }
    
    // check if direction changes bigger than 90 degrees
    // cos(theta) = A * B / (|A| * |B|)
    // A => direction
    // B => [0, 1]
    return direction[1] <= 0
};
```
