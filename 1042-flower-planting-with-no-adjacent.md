Youtube video explaining this: https://youtu.be/IXk3kdXWp5M


```js
var gardenNoAdj = function(N, paths) {
    let map = {};
    for(let i=1; i<=N; i++){
        map[i] = [];
    }
    
    for(let path of paths){
        map[path[0]].push(path[1]);
        map[path[1]].push(path[0]);
    }
    let res = new Array(N).fill(0);
    for(let i=1; i<=N; i++){
        let set = new Set([1,2,3,4]);
        
        for(let next of map[i]){
            if(set.has(res[next-1])) set.delete(res[next-1]);
        }
        
        res[i-1] = set.values().next().value; 
    }
    
    return res;
};
```
