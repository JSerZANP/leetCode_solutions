Here is my video explaining it: https://youtu.be/tAMRNMh_VCU

```js
/**
 * @param {number[][]} workers
 * @param {number[][]} bikes
 * @return {number[]}
 */

const getDistance = (worker, bike) => {
    return Math.abs(worker[0] - bike[0]) + Math.abs(worker[1] - bike[1])
}

// O(NM*log(NM))
// O(NM)
// var assignBikes = function(workers, bikes) {
//     // n ^ 2
//     // [i, j , distance] => O(n ^ 2)
//     //  sort => distance, worker index(if bike is the same),, bike index (if worker is the same) 
//     // [0, 0, 1]
//     // [1, 0, 1]
//     // [1, 2, 1]
//     // [2, 0, 1]
//     // [2, 2, 1]
//     // ....
    
    
//     //1. get all combinations
//     // O(N * M) both for Time/Space
//     const combinations = []
//     for (let i = 0; i < workers.length; i++) {
//         for (let j = 0; j < bikes.length; j++) {
//             combinations.push([i, j, getDistance(workers[i], bikes[j])])
//         }
//     }
    
//     // 2. sort them, distance > worker => bike
//     // O(N * M * log(N * M))
//     combinations.sort((a, b) => {
//         if (a[2] === b[2]) {
//             if (a[0] === b[0]) {
//                 return a[1] - b[1]
//             } else {
//                 return a[0] - b[0]
//             }
//         } else {
//             return a[2] - b[2]
//         }
//     })
    
//     // 3. collect result
//     const result = []
//     // O(N) + O(M)
//     // O(NM)
//     const usedWorker = new Set()
//     const usedBike = new Set()
//     for (let combination of combinations) {
//         const [workerIndex, bikeIndex] = combination
//         if (!usedWorker.has(workerIndex) && !usedBike.has(bikeIndex)) {
//             result[workerIndex] = bikeIndex
//             usedWorker.add(workerIndex)
//             usedBike.add(bikeIndex)
//         }
        
//         if (usedWorker.size === workers.length) {
//             break
//         }
//     }
    
//     return result
// };



// Time: O(Max(workers[i][0], bikes[i][0]) * Max(workers[i][1], bikes[i][1]))
// Space: O(NM)
var assignBikes = function(workers, bikes) {
    //1. get all combinations
    // Time: O(NM)
    // Space: O(NM)  depends on the implement of sparse array.
    const combinations = []
    for (let i = 0; i < workers.length; i++) {
        for (let j = 0; j < bikes.length; j++) {
            const distance = getDistance(workers[i], bikes[j])
            if (!combinations[distance]) {
                combinations[distance] = []
            }
            combinations[distance].push([i, j])
        }
    }
    
    // notice now combinations might be a sparse array
    // 2. collect result
    const result = []
    
    
    const Used = {
        _usedWorker: new Set(),
        _usedBike: new Set(),
        has(i, j) {
            return this._usedWorker.has(i) || this._usedBike.has(j)
        },
        set(i, j) {
            this._usedWorker.add(i)
            this._usedBike.add(j)
        }
    }
    
    // Space: O(N) + O(M)
    const usedWorker = new Set()
    const usedBike = new Set()
    // Time: worst would be O(Max(workers[i][0], bikes[i][0]) * Max(workers[i][1], bikes[i][1]))
    for (let combination of combinations) {
        if (!combination) continue
        // Time: Totally O(NM)
        for (let [workerIndex, bikeIndex] of combination) {
            if (!Used.has(workerIndex, bikeIndex)) {
                result[workerIndex] = bikeIndex
                Used.set(workerIndex, bikeIndex)
            }
            
            if (usedWorker.size === workers.length) {
                break
            }
        }
    }
    
    return result
};








```
