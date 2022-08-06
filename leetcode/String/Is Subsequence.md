# Is Subsequence

> [leetcode > 329 > Is Subsequence](https://leetcode.com/problems/is-subsequence)
> 출처: leetcode, [https://leetcode.com]

- easy

## 해결 과정

1. sequence 형태로 값이 indexOf 사용하여 다음 문자 검사
2. 투 포인트 형태로 풀이 가능 (더 빠르다)

## 코드 1

```kotlin
fun isSubsequence(s: String, t: String): Boolean {
    var index = 0
    s.forEach { char ->
        index = t.indexOf(char, index)
        if (index == -1) {
            return false
        }
        index++
    }
    return true
}
```

## 코드 1 (two point)

```kotlin
fun isSubsequence(s: String, t: String): Boolean {
    if (s.isEmpty()) {
        return true
    }
    var leftPoint = 0
    t.forEach { char ->
        if (s[leftPoint] == char) {
            leftPoint++
            if (leftPoint == s.length) {
                return true
            }
        }
    }
    return false
}
```

## 배운 점
1. 문자열, list 검색은 이진 탐색이나, tow point 사용
2. `indexOf` 는 값이 없을 경우 -1 return 

