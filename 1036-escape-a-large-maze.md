A video explaining this: https://youtu.be/ouptJDhag8Y

```js

const getGrid = (statusGrid, x, y) => {
    const row = statusGrid[x]
    return row ? row[y] : undefined;
}


// 2 - block
// 1 - checked
// 0 - uncheck
const setGrid = (statusGrid, x, y, data) => {
    const row = statusGrid[x]
    if (row) {
        row[y] =  data
    } else {
        statusGrid[x] = []
        statusGrid[x][y] = data
    }
}

const equal = (a, b) => {
   return a && b && a[0] === b[0] && a[1] === b[1]
}

const length = 10**6

const isPossibileWithStartOf = (blocked, source, target, statusGrid) => {
    // for 2000 blocks
    // maximum , together with border, triangle
    // 2 block => 1
    // 3 blocks => 1 + 2
    // 200 blocks => 1 + 2 + ....199
    // max = 200 * 199 / 2 = 19900
    // BFS from the source
    //     1. if target is met , true
    //     2. if count > 19900, true
    //     3. if stopped, false
    
    let temp = [source];
    let availCount = 0;
    let isPossible = 0; // not possible
    
    // while there is possible squares
    // update them with new round
    while(temp.length) {
        const newTemp = [];
        for (let i = 0, total = temp.length; i < total;i++) {
            // if target is met
            if (equal(temp[i], target)) {
                isPossible = 2 // found
                break;
            }
            
            const current = temp[i];
            const status = getGrid(statusGrid, current[0], current[1])
            switch (status) {
                case 2:
                case 1:
                    break
                default:
                    availCount += 1
                    setGrid(statusGrid, current[0], current[1], 1)
                    if (current[0] + 1 < length ) {
                        newTemp.push([current[0] + 1, current[1]])
                    }
                    if (current[0] > 0 ) {
                        newTemp.push([current[0] - 1, current[1]])
                    }
                    if (current[1] + 1 < length ) {
                        newTemp.push([current[0], current[1] + 1])
                    }
                    if (current[1] > 0 ) {
                        newTemp.push([current[0], current[1] - 1])
                    }
                
            }
        }
        
        if (isPossible) {
            break
        }
        
        if (availCount > 19900) {
            isPossible = 1 // possible
            break
        }
        
        temp = newTemp
    }
    
    return isPossible
}

/**
 * @param {number[][]} blocked
 * @param {number[]} source
 * @param {number[]} target
 * @return {boolean}
 */
var isEscapePossible = function(blocked, source, target) {
    // need to check again from target => source
    const statusGrid = []
    
    // first thing is to map the block squares
    blocked.forEach(block => {
        setGrid(statusGrid, block[0], block[1], 2);
    })
    
    const isPossibleFromSource = isPossibileWithStartOf(blocked, source, target, statusGrid);
    
    switch (isPossibleFromSource) {
        case 2: // met
            return true
        case 0: // source is circled
            return false
        default:
            const isPossibleFromTarget = isPossibileWithStartOf(blocked, target, source, statusGrid); 
            return isPossibleFromTarget !== 0; // target is not circled
    }
        
}; 
```
