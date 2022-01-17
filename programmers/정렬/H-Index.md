## H-Index

> 프로그래머스 코딩테스트 연습 > 정렬 > H-Index 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/courses/30/lessons/42747
> 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges

- Level2
- 정렬 (출제 빈도: 높음, 평균 점수: 높음)

## 해결 과정
"정렬" 때문입니다. 오름차순으로 정렬한 후라고 합시다. 정렬에 의해서 i에 대해서, i 이후에 원소들은 모두 i에 위치하는 원소보다 크다는 것이 만족됩니다. 즉 다음 수식이 항상 만족되지요.
citations[i + 1] > citations[i]

## 코드 1

```kotlin
fun solution(citations: IntArray): Int {
    var answer = 0
    citations.sort()
    for (i in 0 until citations.size) {
        val h = citations.size - i
        if (citations[i] >= h) {
            answer = h
            break
        }
    }
    return answer
}
```

## 코드 2 : 다른 사람의 코드

```kotlin
fun solution(citations: IntArray): Int {
    val result = citations.sortedArrayDescending()
    for (i in 0 until result.size) {
        if (result[i] < i + 1) {
            return i
        }
    }

    return citations.size
}
```

## 코드 3

```kotlin
 fun solution(citations: IntArray) = citations.sortedDescending().mapIndexed { idx, item -> min(idx + 1, item) }.max()
```

## 배운점
- 오름차순, 내림차순 

## 풀이 참고

- https://gurumee92.tistory.com/177
