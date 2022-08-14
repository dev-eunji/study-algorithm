# Backspace String Compare

> [leetcode > 844 > Backspace String Compare](https://leetcode.com/problems/backspace-string-compare)
> 출처: leetcode, [https://leetcode.com]

- Level Easy

## 해결 과정

1. HashMap으ㄹ 사용하여 # 문자를 만나면 pop해주고 아니면 push 마지막 문자 형태 비교
2. 마지막 남은 문자 size가 다른 케이스 예외처리

## 코드 1

```kotlin
fun backspaceCompare(s: String, t: String): Boolean {
    val stackForS = Stack<Char>()
    val stackForT = Stack<Char>()

    s.forEach { char ->
        if (char == '#') {
            if (stackForS.isNotEmpty()) {
                stackForS.pop()
            }
            return@forEach
        }
        stackForS.push(char)
    }
    t.forEach { char ->
        if (char == '#') {
            if (stackForT.isNotEmpty()) {
                stackForT.pop()
            }
            return@forEach
        }
        stackForT.push(char)
    }

    if (stackForS.size != stackForT.size) {
        return false
    }

    while (stackForS.isNotEmpty() && stackForT.isNotEmpty()) {
       if (stackForS.pop() != stackForT.pop()) return false
    }
    return true
}
```


## 코드 2: 다른 사람 코드

```c++
 bool backspaceCompare(string S, string T) {
    int i = S.length() - 1, j = T.length() - 1, back;
    while (true) {
        back = 0;
        while (i >= 0 && (back > 0 || S[i] == '#')) {
            back += S[i] == '#' ? 1 : -1;
            i--;
        }
        back = 0;
        while (j >= 0 && (back > 0 || T[j] == '#')) {
            back += T[j] == '#' ? 1 : -1;
            j--;
        }
        if (i >= 0 && j >= 0 && S[i] == T[j]) {
            i--;
            j--;
        } else {
            break;
        }
    }
    return i == -1 && j == -1;
}
```
