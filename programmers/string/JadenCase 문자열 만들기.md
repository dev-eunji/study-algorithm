# JadenCase 문자열 만들기

> [프로그래머스 코딩테스트 연습 > 연습문제 > JadenCase 문자열 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/12951)
> 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges

- Level2

## 해결 과정 

1. 첫번째 문자는 대문자 치환, 나머지는 소문자 치환
2. 순차적 코드 리팩토링

## 코드 1

```kotlin
fun solution(s: String): String {    
    return s.lowercase().split(" ").map {
        it.capitalize() // @DeprecatedSinceKotlin("1.5") -> replaceFirstChar
    }.joinToString(" ")
}

fun solution2(s: String): String {
    var answer = StringBuilder()

    s.forEachIndexed { index, char ->
        if (index == 0 || s[index - 1] == ' ') {
            answer.append(char.uppercase())
        } else {
            answer.append(char.lowercase())
        }
    }

    return answer.toString()
}

fun solution1(s: String): String {
    var answer = StringBuilder()

    var words = s.split(" ")
    words.forEachIndexed { index, word ->
        word.forEachIndexed { index, char ->
            if (index == 0) {
                answer.append(char.uppercase())
            } else {
                answer.append(char.lowercase())
            }
        }
        if (index != words.lastIndex) {
            answer.append(" ")
        }
    }
    return answer.toString()
}
```

## 배운 점

1.`capitalize` 첫문자만 대문자 치환 (프로그래머스는 아직 사용 가능) 버전이 낮은거 같다.
  - @DeprecatedSinceKotlin("1.5") -> `replaceFirstChar` 사용
