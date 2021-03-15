Here is my explaning video: https://youtu.be/k0dmejZt1Eo


```js
/**
 * @param {number[]} rains
 * @return {number[]}
 */

// time: O(n^2)
// sapceL O(n)
// var avoidFlood = function(rains) {
//     // 1,2,0,0,3,2,1
  
//     // choose closest full lake which are to be rained
//     // 1 2
  
  
//     // 1. use a set to track the full lakes
//     // 2. search for the first full lake to be rained on on-rainy day
  
//     const fullLakes = new Set()
//     const actions = []
    
//     for (let i = 0; i < rains.length; i++) {
//       if (rains[i] === 0) {
//         // 1,2,0,0,3,2,1
//         let lakeSoonToFlood = null
//         let j = i + 1
//         while (j < rains.length) {
//           if (rains[j] !== 0 && fullLakes.has(rains[j])) {
//             lakeSoonToFlood = rains[j]
//             break
//           }
//           j += 1
//         }
        
//         if (lakeSoonToFlood) {
//           dryIt(lakeSoonToFlood)
//         } else {
//           dryAnyLake()
//         }
        
//       } else {
//         const isSafe = letItBe(rains[i])
//         if (!isSafe) return []
//       }
//     }
  
//     function dryAnyLake() {
//       if (fullLakes.size > 0) {
//         for (let lake of fullLakes) {
//           dryIt(lake)
//           break
//         }
//       } else {
//         dryIt(1)
//       }
//     }
  
//     function dryIt(lake) {
//       fullLakes.delete(lake)
//       actions.push(lake)
//     }
  
  
//     function letItBe(lake) {
//       if (fullLakes.has(lake)) {
//         return false    
//       }
      
//       fullLakes.add(lake)
//       actions.push(-1)
      
//       return true
//     }
  
//     return actions
    
// };


//  1 2 3 4  0 0 0 5 0 0 0 0 0 0 5
//  1 2 3 5  0 6 0 7 0 8 0 9...
//  XXX 0000 XXX 000
// rains - n
// continuous 0 k

// before:  O(k * n)
// after : O(fullLake.size * k)

// O(n^2)
// ~O(n)
var avoidFlood = function(rains) {
    // 1,2,0,0,3,2,1
  
    // choose closest full lake which are to be rained
    // 1 2
  
  
    // 1. use a set to track the full lakes
    // 2. search for the first full lake to be rained on on-rainy day
  
    const fullLakes = new Set()
    const actions = []
    
    for (let i = 0; i < rains.length; i++) {
      if (rains[i] === 0) {
        // 1,2,0,0,3,2,1
        let lakeSoonToFlood = null
        let nonRainDayCount = 0
        
        let j = i
        while (j < rains.length) {
          if (rains[j] !== 0 && fullLakes.has(rains[j])) {
            lakeSoonToFlood = rains[j]
            break
          }
          
          if (rains[j] === 0) {
            nonRainDayCount += 1
            
            if (nonRainDayCount === fullLakes.size) {
              break
            }
          }
          
          j += 1
        }
        
        // j stops at enough zeros, or the soon lake to be raind
        if (lakeSoonToFlood) {
          dryIt(lakeSoonToFlood)
        } else {
          // dray for the leading non-rainy days
          for (let k  = i ; k <= j; k++) {
            if (rains[k] === 0) {
              dryAnyLake()
              i = k
            } else {
              break
            }
          }
        }
        
      } else {
        const isSafe = letItBe(rains[i])
        if (!isSafe) return []
      }
    }
  
    function dryAnyLake() {
      if (fullLakes.size > 0) {
        for (let lake of fullLakes) {
          dryIt(lake)
          break
        }
      } else {
        dryIt(1)
      }
    }
  
    function dryIt(lake) {
      fullLakes.delete(lake)
      actions.push(lake)
    }
  
  
    function letItBe(lake) {
      if (fullLakes.has(lake)) {
        return false    
      }
      
      fullLakes.add(lake)
      actions.push(-1)
      
      return true
    }
  
    return actions
    
};
```
