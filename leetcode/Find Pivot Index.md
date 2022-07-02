# Find Pivot Index

> [leetcode > 724 > Find Pivot Index](https://leetcode.com/problems/find-pivot-index)
> 출처: leetcode, [https://leetcode.com]

- Level1

## 해결 과정

1. sliding

## 코드 1

```kotlin
fun pivotIndex(nums: IntArray): Int {
    var totalSum = nums.sum()
    var leftSum = 0
    nums.forEachIndexed { index, num ->
        totalSum -= num
        if (leftSum == totalSum) {
            return index
        }
        leftSum += num
    }

    return -1
}
```
