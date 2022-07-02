# shuffle string

> [leetcode > 1528 > Shuffle String](https://leetcode.com/problems/shuffle-string)
> 출처: leetcode, [https://leetcode.com]

- Level1

## 해결 과정

1. shuffle[rank] = s[index]

## 코드 1

```kotlin
fun restoreString(s: String, indices: IntArray): String {
    val shuffle = MutableList(s.length) {
        it.toChar()
    }
    indices.forEachIndexed { index, rank ->
        shuffle[rank] = s[index]
    }
    return shuffle.joinToString("")
}
```

## 코드 2: 다른 사람 코드

```kotlin
fun restoreString(s: String, indices: IntArray): String {
    val array = CharArray(s.length)
    indices.forEachIndexed { i, num -> array[num] = s[i] }

    return String(array)
}
