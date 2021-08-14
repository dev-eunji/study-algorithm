# K번째수

> [프로그래머스 코딩테스트 연습 > 정렬 > K번째수](https://programmers.co.kr/learn/courses/30/lessons/42748)
> 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges

- Level1
- 정렬 (출제 빈도: 높음, 평균 점수: 높음)

## 해결 과정

`array`를 list로 변환한 후 i번째부터 j번째까지 자르고 정렬한다.
정렬 후, k 번째 값을 `answer` list에 더해준다.

이때 리스트의 `index` 는 `~번째` 보다 하나 작은 값이기 때문에
i번째는 `i-1`.

## 코드 1

```kotlin
fun solution(array: IntArray, commands: Array<IntArray>): IntArray {
    val answer = mutableListOf<Int>()
    commands.forEach { command ->
        var input = array.toMutableList()
        val i = command[0]
        val j = command[1]
        val k = command[2]

        input = input.subList(i - 1, j)
        input.sort()
        answer.add(input[k-1])
    }
    return answer.toIntArray()
}
```

## 코드 2 : 다른 사람의 코드

```kotlin
fun solution(array: IntArray, commands: Array<IntArray>): IntArray =  commands.map { command ->
    array.slice(IntRange(command[0] - 1, command[1] - 1)).sorted()[command[2] - 1]
}.toIntArray()
```

## 배운 점

- `map()` 함수로 최종 결과 list를 만드는 아이디어.
- Arrays의 `slice()` 함수와 `sorted()` 함수로 Array를 자르고 정렬하기.

  ```kotlin
  public fun IntArray.slice(indices: IntRange): List<Int> {
      if (indices.isEmpty()) return listOf()
      return copyOfRange(indices.start, indices.endInclusive + 1).asList()
  }
  ```
  
  
## 코드 : orange4912
```kotlin
fun solution(array: IntArray, commands: Array<IntArray>): IntArray {
    // var answer = intArrayOf()
    var answer = IntArray(commands.size)

    if (array.size >= 100 || (commands.size < 1 && commands.size >= 50)) {
        return answer
    }

    for (i in 0 until commands.size) {
        val findSlice = array.slice(commands[i][0] -1 .. commands[i][1] -1).sorted()
        answer[i] = findSlice[commands[i][2] -1]
    }

    return answer
}
```

## 배운 점: orange4912
- Arrays의 `slice()` 함수와 IntArray `sorted()` 함수로 Array를 자르고 정렬하기. (sort 없음)
- slice, subList, sorted, sort 구분하여 쓰기. ide 부재로 알아 두어야 됩니다.ㅠ
- var answer = intArrayOf() 기본 코드에 size 할당 되지 않아 indexoutofboundsexception 발생되고, 디버깅이 어려워 좋은 방법이 없을까 고민 필요
