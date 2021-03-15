here is a video explaining : https://youtu.be/iA2TsM70Ajk

```js
/**
 * @param {number[][]} points
 * @return {number}
 */
var minCostConnectPoints = function(points) {
    // F  ->  T (MST)
  
    // [], -> [e1, e2, ...em]
  
    // e1,...ek,  subset of T
    // ek+1 is also in T
  
    // suppose ek+1 is not int T
    // T + ek+1 => create a circle, at least 2 more edges in this circle
  
    // in F, we avoided circles. ex is not in F.
    // ex >= ek + 1
  
    // if replace ex -> ek+1 => create smaller ST.
  
    // so F is the MST -> is the T
    
    // Array<from, to, distance>
    const edges = []
    
    
    for (let i = 0; i < points.length - 1; i++) {
      for (let j = i + 1; j < points.length; j++) {
        edges.push([i, j, Math.abs(points[i][0] - points[j][0]) + Math.abs(points[i][1] - points[j][1])])
      }
    }
  
    edges.sort((a, b) => a[2] - b[2])
  
    // Map<point index, Set<point index>
    const selectedEdges = new Map()
    let selectedEdgeCount = 0
    
    const addEdge = (from, to) => {
      if (selectedEdges.has(from)) {
        selectedEdges.get(from).add(to)
      } else {
        selectedEdges.set(from, new Set([to]))
      }
      
      if (selectedEdges.has(to)) {
        selectedEdges.get(to).add(from)
      } else {
        selectedEdges.set(to, new Set([from]))
      }
    }
    
    const isGeneratingCircle = (from, to) => {
      if (!selectedEdges.has(from)) {
        return false
      }
      
      const walked = new Set()
      const stack = [from]
      
      while (stack.length > 0) {
        const top  = stack.pop()
        
        if (top === to) {
          return true
        }
        
        if (selectedEdges.has(top)) {
          for (let next of selectedEdges.get(top)) {
            if (walked.has(next)) {
              continue
            }
            
            stack.push(next)
            walked.add(next)
          }    
        }
      }
      
      return false
    }
    
    
    let result = 0
    for (let [from, to, distance] of edges) {
      // if there is a circle, skip
      const isFromGeneratingCircle = isGeneratingCircle(from, to)
      
      if (isFromGeneratingCircle) {
        continue
      }
      
      addEdge(from, to)
      selectedEdgeCount += 1
      result += distance
      
      if (selectedEdgeCount === points.length - 1) {
        break
      }
    }
  
    return result
};
```
