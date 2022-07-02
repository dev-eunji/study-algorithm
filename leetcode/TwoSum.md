# Two Sum

> [leetcode > 1 > Two Sum](https://leetcode.com/problems/two-sum)
> 출처: leetcode, [https://leetcode.com]

- Level1

## 해결 과정

1. -

## 코드 1

```kotlin
fun twoSum(nums: IntArray, target: Int): IntArray {
    for (i in nums.indices) {
        for (j in nums.indices) {
            if (i != j && nums[i] + nums[j] == target) {
                return intArrayOf(i, j)
            }
        }
    }
    return intArrayOf(0)
}
```

## 코드 2: 다른 사람 코드

```kotlin
fun twoSum(nums: IntArray, target: Int): IntArray {
    val diffMap = mutableMapOf<Int, Int>()
    nums.forEachIndexed { index, int -> 
        diffMap[int]?.let { return intArrayOf(it, index) }
        diffMap[target - int] = index   
    }
    return intArrayOf()
}
