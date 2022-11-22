## 参考

https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_custom_properties#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95

```typescript
const arr = [6, 1, 5, 2, 4, 3, 3, 4, 2, 5, 1, 6];

// 如何将 arr 转换成 arr2

const arr2 = [
    [6],
    [1, 5],
    [2, 4],
    [3, 3],
    [4, 2],
    [5, 1],
    [6]
];

const result = [];
let sum = 0;
const flag = 6;
let i = 0;
let item = [];

while (arr[i]) {
    sum += arr[i];
    item.push(arr[i]);
    if (sum === flag) {
        result.push(item);
        sum = 0;
        item = [];
    }
    i++;
}
console.log(result, arr.length, i);
```