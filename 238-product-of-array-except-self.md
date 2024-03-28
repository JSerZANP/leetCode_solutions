## 1. 3 list easy to understand

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function (nums) {
  // cannot divide
  // then have to calculate the product for the left and product for the right
  // inclusive
  const productTil = new Array(nums.length).fill(1);
  const productFrom = new Array(nums.length).fill(1);

  let product = 1;
  for (let i = 0; i < nums.length; i++) {
    product *= nums[i];
    productTil[i] = product;
  }

  product = 1;
  for (let i = nums.length - 1; i >= 0; i--) {
    product *= nums[i];
    productFrom[i] = product;
  }

  const result = [];
  for (let i = 0; i < nums.length; i++) {
    const productLeft = i === 0 ? 1 : productTil[i - 1];
    const productRight = i === nums.length - 1 ? 1 : productFrom[i + 1];
    result.push(productLeft * productRight);
  }
  return result;
};
```

## 2. use only 1 list

Me explaining it on youtube: https://youtu.be/MljYepMXhAo

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function (nums) {
  const result = [];
  for (let i = 0; i < nums.length; i++) {
    result[i] = i === 0 ? nums[i] : result[i - 1] * nums[i];
  }

  let productRight = 1;
  for (let i = nums.length - 1; i > -1; i--) {
    const productLeft = i === 0 ? 1 : result[i - 1];
    result[i] = productLeft * productRight;

    productRight *= nums[i];
  }

  return result;
};
```
