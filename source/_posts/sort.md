---
title: 常用排序js实现
---

```
// 冒泡排序
function bubbleSort(arr) {
    const len = arr.length
    let temp = 0
    for(let i = 0; i < len; i++){
        for(let j =0; j < len - i -1; j++){
        if(arr[j] > arr[j+1]){
            temp = arr[j]
            arr[j] = arr[j+1]
            arr[j+1] = temp
        }
        }
    }
    return arr
}

// 选择排序
function selectionSort(arr) {
    const len = arr.length
    let temp, minIndex
    for (let i = 0; i < len - 1; i++){
        minIndex = i
        for(let j = i + 1; j< len; j++){
            if(arr[j] < arr[minIndex]){
                minIndex = j
            }
        }
        temp = arr[i]
        arr[i] = arr[minIndex]
        arr[minIndex] = temp
    }
    return arr
}

// 插入排序
function insertionSort(arr){

}

// 快速排序
function quickSort(arr) {
    const len = arr.length
    if (len <= 1) return arr
    const pivotIndex = Math.floor(len / 2)
    const pivot = arr.splice(pivotIndex, 1)[0]
    const left = [], right = []
    for (let i = 0; i < len - 1; i++) {
        if (arr[i] < pivot) {
            left.push(arr[i])
        } else {
            right.push(arr[i])
        }
    }
    return quickSort(left).concat([pivot], quickSort(right))
}
```