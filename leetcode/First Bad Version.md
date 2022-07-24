# First Bad Version

> [leetcode > 278 > First Bad Version](https://leetcode.com/problems/first-bad-version)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Binary Search]

## 해결 과정

1. 이진 탐색
 - isBadVersion == true -> right 범위 좁힘
 - isBadVersion == false -> left 범위 넓힘
 - (검색 범위를 지정할 두개의 포인터를 두고 가운데 값(mid)을 스캔한 후 찾는 값(target)이 중간값보다 작으면 스캔범위를 포인터를 앞으로 옮기고 아니면 뒤쪽을 스캔하는 것을 반복)
2. 첫번째 badVersion left를 리턴


## 코드 1

```kotlin
override fun firstBadVersion(n: Int) : Int {
    var left = 1
    var right = n

    var mid: Int
    while (left <= right) {
        mid = left + (right - left) / 2

        if (isBadVersion(mid)) {
            right = mid - 1
        } else {
            left = mid + 1
        }
    }

    return left
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```python
def firstBadVersion(self, n) -> int:
    left, right = 1, n
    while left < right:
        mid = left + (right - left) // 2
        if isBadVersion(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

## 배운 점
1. mid 값을 계산 할 경우 `mid = left + (right - left) / 2` [익숙해 지자]
 - `mid = (left + right) / 2` 는 Int 범위를 넘어가게 된다.


