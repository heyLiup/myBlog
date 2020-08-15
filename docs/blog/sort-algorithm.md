
# 常用排序算法


## 快速排序

```js


function quickSort (arr) {
    let half = 0;
    let arr1 = [];
    let arr2 = [];
    if (arr.length <= 1 ) {
        return arr;
    }

    //从1开始遍历，确保half不会被重复push
    for (let i = 1, len = arr.length; i < len; i++) {
        if (arr[i] < arr[half]) {
            arr1.push(arr[i])
        } else if (arr[i] >= arr[half]) {
            arr2.push(arr[i])
        }
    }
    return quickSort(arr1).concat([arr[half]], quickSort(arr2));
}


```