# Squares of a Sorted Array

> [leetcode > 977 > Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Two Pointer]

## 해결 과정

1. 내림차순으로 정렬된 Integer 배열 nums의 값들을 제곱하여 내림차순 정렬 후 반환 문제
2. TwoPoint 형태로 배열의 왼쪽, 오른쪽 비교하여 정렬
3. 제곱근을 구하고 범위를 좁힌다.
 - `abs` 를 이용하여 절대 값 비교
 - ![image](https://user-images.githubusercontent.com/8637598/196018823-b0c07bc5-4279-4ba4-9952-613b28da1d58.png)


## 코드 1

```kotlin
fun sortedSquares(nums: IntArray): IntArray {
    val answer = IntArray(nums.size)
    var low = 0
    var higt = nums.size - 1

    for (index in nums.size - 1 downTo 0) {
        if (abs(nums[low]) > abs(nums[higt])) {
            answer[index] = nums[low] * nums[low]
            low++
        } else {
            answer[index] = nums[higt] * nums[higt]
            higt--
        }
    }
    return answer
}
```

## 배운 점
1. 투포인터를 이용하여 IntArray size만큼 돌면서 제곱근을 구하고, 정렬을 한꺼번에 할 수 있다.


