# Make The String Great

> [leetcode > 1544 > Make The String Great](https://leetcode.com/problems/make-the-string-great)
> 출처: leetcode, [https://leetcode.com]

- Easy

## 해결 과정

1. 좋은 문자 만들기 (인접한 두 문자를 없애는 문제)

## 코드 1

```kotlin
fun makeGood(s: String): String {
    val stack = Stack<Char>()

    s.forEach { char ->
        if (stack.isNotEmpty() && abs(stack.lastElement() - char) == 32) {
            stack.pop()
        } else {
            stack.push(char)
        }
    }

    val answer = StringBuilder()
    stack.forEach { currentString ->
        answer.append(currentString)
    }

    return answer.toString()
}
```

## 배운 점
1. 대문자, 소문자 아스키코드 값의 차이는 32이다.
2. Iteration(O(n^2)), Recursion(O(n^2)), Stack(O(n))

