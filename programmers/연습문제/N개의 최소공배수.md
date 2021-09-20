# N개의 최소공배수

> [프로그래머스 코딩테스트 연습 > 연습문제 > N개의 최소공배수](https://programmers.co.kr/learn/courses/30/lessons/12953)
> 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges

- Level1

## 해결 과정

1. HashMap에 arr의 소인수분해 결과를 저장한다. 단, 같은 수라면 가장 큰 값만 저장한다.

   - 예를 들어서 2와 24라면, (2: 3), (3: 1) 이 HashMap에 저장된다.

2. HashMap의 key 들을 value 만큼 곱하여 반환한다. (`pow`)

## 코드 1

```kotlin
fun solution(arr: IntArray): Int {
    val map = HashMap<Int, Int>()
    arr.forEach {
        var num = it
        for(i in 2..num) {
            var count = 0
            while (num % i == 0) {
                count += 1
                num /= i
            }
            if(!map.containsKey(i)) map[i] = count
            else if(map[i]!! < count) map[i] = count
        }
    }
    return map.toList().fold(1) { total, pair ->
        total * (0 until pair.second).fold(1) { acc, _ ->
            acc * pair.first
        }
    }
}
```

## 배운 점

- 소인수분해 코드

```kotlin
for(i in 2..num) {
    while(num % i == 0) num/=i
}
```

## 질문

- Int 의 제곱을 구할 때 `.toDouble()` 로 형변환을 하면서 `pow()` 함수를 사용하는 것 vs. 직접구현
