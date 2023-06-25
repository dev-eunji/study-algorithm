# Majority Element

> [leetcode > 169 > Majority Element](https://leetcode.com/problems/majority-element/description/?envType=study-plan-v2&envId=top-interview-150)
- 출처: leetcode, [https://leetcode.com]

- Level Easy

## 해결 과정

1. sort, hashMap, Moore voting algorithm
- Moore voting algorithm: https://sgc109.github.io/2020/11/30/boyer-moore-majority-vote-algorithm/


## 코드 1

```kotlin
fun majorityElement(nums: IntArray): Int {
    var count = 0
    var major = 0

    for (num in nums) {
        if (count == 0) {
            major = num
        }
        if (num != major) {
            count--
        } else {
            count++
        }
    }
    return major
}
```

```kotlin
fun majorityElement(nums: IntArray): Int {
    nums.sort()
    return nums[nums.size/2]
}
```

```kotlin
fun majorityElement(nums: IntArray): Int {
    return nums.find { num -> 
        nums.count { it == num } > nums.size / 2 
    } ?: 0
}
```

## 배운 점
1. Boyer-Moore 과반수 투표 알고리즘에 대해 배웠다.
 - 배열에 포함된 원소들 중 절반 이상 포함된 원소를 linear time 과 constant space 로 찾을 수 있는 알고리즘이다.



