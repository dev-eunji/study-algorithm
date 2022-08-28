# Longest Common Prefix

> [leetcode > 14 > Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)
- 출처: leetcode, [https://leetcode.com]

- Easy

## 해결 과정

1. 전형적인 LCP 문제
2. 완전 탐색을 통해 해당 prefix 검사 `indexOf`
3. 이진탐색으로 풀이 가능하다.

## 코드 1

```kotlin
fun longestCommonPrefix(strs: Array<String>): String {
    // Horizontal Scanning
    if (strs.isNullOrEmpty()) {
        return "-1"
    }
    var prefix = strs[0]
    for (i in 1 until strs.size) {
        while (strs[i].indexOf(prefix) != 0) {
            prefix = prefix.substring(0, prefix.length - 1)
        }
    }
    return prefix
}

fun longestCommonPrefix1(strs: Array<String>): String {
    // Vertical Scanning
    if (strs.isNullOrEmpty()) {
        return "-1"
    }
    var prefix = strs
    for (i in 0 until strs[0].length) {
        val target = strs[0][i]
        for (j in 1 until strs.size) {
            if (i == strs[j].length || strs[j][i] != target) {
                return strs[0].substring(0, i)
            }
        }
    }
    return prefix[0]
}
```

## 코드 1 (binarysearch)

```kotlin
private fun getMinLength(strs: Array<String>): Int {
    var minLength = Integer.MAX_VALUE
    strs.forEach {
        minLength = minLength.coerceAtMost(it.length)
    }
    return minLength
}

private fun isLeftTargetUnder(
    arr: Array<String>,
    target: String,
    start: Int,
    end: Int
): Boolean {
    for (element in arr) {
        for (index in start..end) {
            if (element[index] != target[index]) {
                return false
            }
        }
    }
    return true
}

fun longestCommonPrefix(strs: Array<String>): String {
    // Binary search
    if (strs.isNullOrEmpty()) {
        return "-1"
    }
    var prefix = ""
    val minLength = getMinLength(strs)
    var left = 0
    var right = minLength - 1
    val target = strs[0]
    while (left <= right) {
        val mid = left + (right - left) / 2

        if (isLeftTargetUnder(strs, target, left, mid)) {
            prefix += target.substring(left, mid + 1)
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return prefix
}
```

## 코드 2 (Most Votes)
```
public String longestCommonPrefix(String[] strs) {
    if (strs == null || strs.length == 0)
        return "";

    Arrays.sort(strs);
    String first = strs[0];
    String last = strs[strs.length - 1];
    int c = 0;
    while(c < first.length())
    {
        if (first.charAt(c) == last.charAt(c))
            c++;
        else
            break;
    }
    return c == 0 ? "" : first.substring(0, c);
}
```

## 배운 점
1. 처음에 hash를 사용해서 풀었는데 의미 없다. (LCP 방법론 공부)
2. LCP 를 배웠다.
3. `indexOf` 는 값이 없을 경우 -1 return 

## 질문
- Most Votes 풀이를 보면 `first`, `last` 만 비교하는데 왜 가능한지 모르겠다.

