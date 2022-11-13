# Remove All Adjacent Duplicates In String

> [leetcode > 1047 > Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string)
> 출처: leetcode, [https://leetcode.com]

- Level Easy

## 해결 과정

1. 문자가 주어졌을때 인접한 동일 문자 제거하는 문제
2. Stack를 사용하여 인접 동일 문자 제거한다. (Stack을 직접 사용해도 되지만 StringBuilder 대체 가능)

## 코드 1

```kotlin
fun removeDuplicates(s: String): String {
    val sb = StringBuilder()
    s.toCharArray().forEach { char ->
        if (sb.isNotEmpty() && sb.last() == char) {
            sb.deleteCharAt(sb.lastIndex)
        } else {
            sb.append(char)
        }
    }
    return sb.toString()
}
```


## 코드 2: 다른 사람 코드

``` Java
public String removeDuplicates(String s) {
    int i = 0, n = s.length();
    char[] res = s.toCharArray();
    for (int j = 0; j < n; ++j, ++i) {
        res[i] = res[j];
        if (i > 0 && res[i - 1] == res[i]) // count = 2
            i -= 2;
    }
    return new String(res, 0, i);
}
```

## 배운 점
1. StringBuilder API `last()`, `deleteCharAt()`을 배웠다.
