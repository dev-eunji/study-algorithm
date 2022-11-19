# BinaryGuess Number Higher or Lower

> [leetcode > 374 > BinaryGuess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Binary Search]

## 해결 과정

1. 이진 탐색 
 - left or low, right or high 중간값 pivot을 중심으로 타겟 값을 비교하여 범위를 줄이며 탐색한다.


## 코드 1

```kotlin
override fun guessNumber(n:Int):Int {
    var low = 1
    var high = n

    while (low <= high) {
        val mid = low + (high - low) / 2

        val res = guess(mid)
        when {
            res == 0 -> {
                return mid
            }
            res < 0 -> {
                high = mid - 1
            }
            else -> {
                low = mid + 1
            }
        }
    }
    return -1
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```python
def guessNumber(self, n):
  lo, hi = 1, n
  while lo < hi:
      mid = (lo + hi) / 2
      if guess(mid) == 1:
          lo = mid + 1
      else:
          hi = mid
  return lo
```

## 배운 점
1. 이진탐색 시 low를 리턴하면 target값에 가장 가까운 값을 리턴 할 수 있다.
