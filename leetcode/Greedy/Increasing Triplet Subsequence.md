# Increasing Triplet Subsequence

> [leetcode > 334 > Increasing Triplet Subsequence](https://leetcode.com/problems/increasing-triplet-subsequence)
> 출처: leetcode, [https://leetcode.com]
- Level Medium [Greedy]

## 해결 과정

1. 순차적으로 `nums[i] < nums[j] < nums[k]`가 존재하는지 리턴하는 문제이다.
2. 전체 배열 길이 만큼 반복하면서, first, second 변수에 담아 비교한다.


## 코드 1

```kotlin
fun increasingTriplet(nums: IntArray): Boolean {
    var first = Int.MAX_VALUE
    var second = Int.MAX_VALUE

    nums.forEach { num ->
        if (num <= first) {
            first = num
        } else if (num <= second) {
            second = num
        } else {
            return true
        }
    }
    return false
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
if      (x <= a) a = x; // a = min so far
else if (x <= b) b = x; // b = min element **with a smaller element to the left**
else    return true;    // x > b, we found an answer
```

## 배운 점
1. Medium 문제여서 어렵게 생각하지 말고 단순하게 생각하자
2. Gready 문제로 순차적 증감 여부 확인하는 방법을 배웠다.
