```js
let randomArray = (length, max) => [...new Array(length)].map(() => Math.round(Math.random() * max))

let a = randomArray(1000000, 1000000)
console.time("Quick Sort")
quickSort(a)
console.timeEnd("Quick Sort")
```