Here is a video explainig it: https://youtu.be/DpipzCreVMU

```js
/**
 * @param {number} numBottles
 * @param {number} numExchange
 * @return {number}
 */
var numWaterBottles = function(numBottles, numExchange) {
    let fullBottleCount = numBottles
    let emptyBottlCount = 0
    let result = 0
    
    while (fullBottleCount > 0) {
      result += fullBottleCount
      emptyBottlCount += fullBottleCount
      
      fullBottleCount = Math.floor(emptyBottlCount / numExchange)
      emptyBottlCount %= numExchange
    }
  
    return result
};
```
