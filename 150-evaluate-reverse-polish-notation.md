```js
/**
 * @param {string[]} tokens
 * @return {number}
 */
var evalRPN = function (tokens) {
  const stack = [];
  for (const token of tokens) {
    switch (token) {
      case "+": {
        const operand2 = stack.pop();
        const operand1 = stack.pop();
        stack.push(operand1 + operand2);
        break;
      }
      case "-": {
        const operand2 = stack.pop();
        const operand1 = stack.pop();
        stack.push(operand1 - operand2);
        break;
      }
      case "*": {
        const operand2 = stack.pop();
        const operand1 = stack.pop();
        stack.push(operand1 * operand2);
        break;
      }
      case "/": {
        const operand2 = stack.pop();
        const operand1 = stack.pop();
        stack.push(Math.trunc(operand1 / operand2));
        break;
      }
      default:
        stack.push(parseInt(token, 10));
    }
  }
  return stack[0];
};
```
