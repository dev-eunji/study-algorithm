# Two Sum

> [leetcode > 205 > TwoIsomorphic Stringsm](https://leetcode.com/problems/isomorphic-strings)
> 출처: leetcode, [https://leetcode.com]

- Level1

## 해결 과정

1. 같은 구조의 문자열인지 체크
2. 두개의 키 값의 값이 다른지 비교

## 코드 1

```kotlin
fun isIsomorphic(s: String, t: String): Boolean {
    val isomorphicMapS = hashMapOf<Char, Char>()
    val isomorphicMapT = hashMapOf<Char, Char>()
    s.forEachIndexed { index, c ->

        // 'a' must be mapped to a uniq character. (a -> b and a -> c) is false
        if (isomorphicMapS.containsKey(c) && isomorphicMapS[c] != t[index]) {
            return false
        }
        // opposit case is same.
        if (isomorphicMapT.containsKey(t[index]) && isomorphicMapT[t[index]] != c) {
            return false
        }
        isomorphicMapS[c] = t[index]
        isomorphicMapT[t[index]] = c
    }
    return true
}
```

## 코드 2: 다른 사람 코드

```kotlin
bool isIsomorphic(string s, string t) {
    int m1[256] = {0}, m2[256] = {0}, n = s.size();
    for (int i = 0; i < n; ++i) {
        if (m1[s[i]] != m2[t[i]]) return false;
        m1[s[i]] = i + 1;
        m2[t[i]] = i + 1;
    }
    return true;
}

## 배운 점
1. 하나의 해시맵을 이용하려고 했는데 키만 중복이 안되고 값은 중복 허용이기에 두개의 맵을 사용
2. 문제 이해 하기가 어렵다ㅠ

