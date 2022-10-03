# Replace All ?'s to Avoid Consecutive Repeating Characters

> [leetcode > 1576 > Replace All ?'s to Avoid Consecutive Repeating Characters](https://leetcode.com/problems/replace-all-s-to-avoid-consecutive-repeating-characters/)
> 출처: leetcode, [https://leetcode.com]

- easy

## 해결 과정

1. ? 문자를 앞, 뒤와 다른 문자열로 바꾸는 문제

## 코드 1

```kotlin
fun modifyString(s: String): String {
    val array = s.toCharArray()

    for (i in 0 until array.size) {
        if (array[i] == '?') {
            for (j in 'a' .. 'c') {
                if (i > 0 && array[i -1] == j) {
                    continue
                }
                if (i + 1 < array.size && array[i + 1] == j) {
                    continue
                }
                array[i] = j
            }
        }
    }
    return array.joinToString("")
}
```

## 코드 2 (Most Votes)

```c++
string modifyString(string s) {
    for (auto i = 0; i < s.size(); ++i)
        if (s[i] == '?')
            for (s[i] = 'a'; s[i] <= 'c'; ++s[i])
                if ((i == 0 || s[i - 1] != s[i]) && (i == s.size() - 1 || s[i + 1] != s[i]))
                    break;
    return s;
}
```

## 배운 점
1. 앞,뒤 다른 문자 대입 시 `a ~ c`로 사용 랜덤 필요 없다.
2. `toCharArray` 변경해서 사용하면 편하게 계산 가능하다.

