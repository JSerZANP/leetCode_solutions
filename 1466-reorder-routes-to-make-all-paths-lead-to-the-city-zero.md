me explaining it on youtube: https://youtu.be/LVuQFBTev58


```js
/**
 * @param {number} n
 * @param {number[][]} connections
 * @return {number}
 */
var minReorder = function(n, connections) {
    // const
    // two Maps<city, Set<city>>
  
    const inboundMap = new Map()
    const outboundMap = new Map()
    
    for (let [from, to] of connections) {
      if (outboundMap.has(from)) {
        outboundMap.get(from).add(to)
      } else {
        outboundMap.set(from, new Set([to]))
      }
      
      if (inboundMap.has(to)) {
        inboundMap.get(to).add(from)
      } else {
        inboundMap.set(to, new Set([from]))
      }
    }
    
    const traversed = new Set()
    
    let result = 0
    
    const walk = (city) => {
      traversed.add(city)
      
      // 1. look at the inbound 
      if (inboundMap.has(city)) {
        for (let from of inboundMap.get(city)) {
          if (!traversed.has(from)) {
            walk(from)
          }
        }
      }
      
      // 2. look at the outbound
      if (outboundMap.has(city)) {
        for (let to of outboundMap.get(city)) {
          if (!traversed.has(to)) {
            result += 1
            walk(to)
          }
        }        
      }
    }
    
    walk(0)
    
    return result
};
```
