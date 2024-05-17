A video explaining this: https://youtu.be/FU1D938frV8

```js
/**
 * @param {string} s
 * @return {number}
 */
var calculate = function (s) {
  const stack = [];

  const tempNumbers = [];
  for (let i = 0; i < s.length + 1; i++) {
    const char = s[i];

    if (char >= "0" && char <= "9") {
      tempNumbers.push(char);
    } else {
      // get the number and push it
      if (tempNumbers.length > 0) {
        const number = parseInt(tempNumbers.join(""));
        tempNumbers.splice(0);
        stack.push(number);
      }

      if (["+", "-", "("].includes(char)) {
        stack.push(char);
      }

      if (char === ")" || i === s.length) {
        // until we met a left parentheses
        const calculationStack = [];
        while (stack.length > 0) {
          const top = stack.pop();
          if (top !== "(") {
            calculationStack.push(top);
          } else {
            break;
          }
        }
        while (calculationStack.length > 0) {
          const top = calculationStack.pop();
          // it should be a number
          const operator = calculationStack.pop();
          if (operator === "+") {
            const secondNumber = calculationStack.pop();
            calculationStack.push(top + secondNumber);
          } else if (operator === "-") {
            const secondNumber = calculationStack.pop();
            calculationStack.push(top - secondNumber);
          } else if (calculationStack.length === 0) {
            stack.push(top);
            break;
          }
        }
      }
    }
  }

  return stack[0];
};
```

Another try

```js
/**
 * @param {string} s
 * @return {number}
 */
var calculate = function (s) {
  const stack = [];

  // process the stack until meet '('
  const processStack = () => {
    // need to reverse the items until (
    const calculationStack = [];
    while (true) {
      const top = stack.pop();
      if (top === "(" || top == null) {
        break;
      }
      calculationStack.push(top);
    }

    if (calculationStack.at(-1) === "-") {
      calculationStack.push(0);
    }
    let result = 0;
    while (calculationStack.length > 1) {
      let operand2 = calculationStack.pop();
      let operator = calculationStack.pop();
      if (operator == null || operator === "(") {
        calculationStack.push(operand2);
        break;
      } else {
        const operand1 = calculationStack.pop() ?? 0;
        const result =
          operator === "+" ? operand1 + operand2 : operand2 - operand1;
        calculationStack.push(result);
      }
    }
    stack.push(calculationStack[0]);
  };

  let buffer = "";
  for (const char of s) {
    if (/[0-9]/.test(char)) {
      buffer += char;
    } else {
      if (buffer.length > 0) {
        stack.push(parseInt(buffer, 10));
        buffer = "";
      }
      if (char === " ") {
        continue;
      }

      if (char !== ")") {
        stack.push(char);
      } else {
        processStack();
      }
    }
  }
  if (buffer.length > 0) {
    stack.push(parseInt(buffer, 10));
  }
  processStack();
  return stack[0];
};
```
