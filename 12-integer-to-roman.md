## 1

A video explaining this: https://youtu.be/eijp-A4T7cs

```js
const map = new Map([
  [1, "I"],
  [5, "V"],
  [10, "X"],
  [50, "L"],
  [100, "C"],
  [500, "D"],
  [1000, "M"],
]);

/**
 * @param {number} num
 * @return {string}
 */
// get thet last digit one by one
// and generate the result
var intToRoman = function (num) {
  let base = 1;
  const result = [];
  while (num > 0) {
    // get last digit
    const last = num % 10;

    if (last < 4) {
      for (let k = last; k > 0; k--) {
        result.unshift(map.get(base));
      }
    } else if (last === 4) {
      result.unshift(...[map.get(base), map.get(base * 5)]);
    } else if (last === 5) {
      result.unshift(map.get(base * 5));
    } else if (last < 9) {
      for (let k = last; k > 5; k--) {
        result.unshift(map.get(base));
      }
      result.unshift(map.get(base * 5));
    } else {
      result.unshift(...[map.get(base), map.get(base * 10)]);
    }

    base *= 10;

    num = (num - last) / 10;
  }
  return result.join("");
};
```

## 2

```js
var intToRoman = function (num) {
  // 1994 / 1000 => 1
  // 994 / 1000 => 9 => CM
  // 94 / 10 => 9 => XC
  // 4  => IV
  const pairs = [
    {
      base: 1000,
      1: "M",
    },
    {
      base: 100,
      10: "M",
      5: "D",
      1: "C",
    },
    {
      base: 10,
      10: "C",
      5: "L",
      1: "X",
    },
    {
      base: 1,
      10: "X",
      5: "V",
      1: "I",
    },
  ];
  let result = "";

  for (const pair of pairs) {
    const repeat = Math.floor(num / pair.base);
    if (repeat < 4) {
      result += pair[1].repeat(repeat);
    } else if (repeat === 4) {
      result += pair[1] + pair[5];
    } else if (repeat === 5) {
      result += pair[5];
    } else if (repeat < 9) {
      result += pair[5] + pair[1].repeat(repeat - 5);
    } else {
      result += pair[1] + pair[10];
    }
    num = num % pair.base;
  }
  return result;
};
```
