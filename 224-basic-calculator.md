A video explaining this: https://youtu.be/FU1D938frV8



```js
/**
 * @param {string} s
 * @return {number}
 */
var calculate = function(s) {
    const stack = []
    
    const tempNumbers = []
    for (let i = 0; i < s.length + 1; i++) {
        const char = s[i]

        if (char >= '0' && char <= '9') {
            tempNumbers.push(char)
        } else {
            // get the number and push it
            if (tempNumbers.length > 0) {
                const number = parseInt(tempNumbers.join(''))
                tempNumbers.splice(0)
                stack.push(number)
            }
            
            if (['+','-','('].includes(char)) {
                stack.push(char)
            }    
            
            if (char === ')' || i === s.length) {
                // until we met a left parentheses
                const calculationStack = []
                while (stack.length > 0) {
                    const top = stack.pop()
                    if (top !== '(') {
                        calculationStack.push(top)
                    } else {
                        break
                    }
                }
                while (calculationStack.length > 0) {
                    const top = calculationStack.pop()
                    // it should be a number
                    const operator = calculationStack.pop()
                    if (operator === '+') {
                        const secondNumber = calculationStack.pop()
                        calculationStack.push(top + secondNumber)
                    } else if (operator === '-') {
                        const secondNumber = calculationStack.pop()
                        calculationStack.push(top - secondNumber)
                    } else if (calculationStack.length === 0) {
                        stack.push(top)
                        break;
                    }
                }
            }
        }
    }
    
    return stack[0]
};
```
