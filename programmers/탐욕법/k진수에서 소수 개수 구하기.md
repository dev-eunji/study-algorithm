# 큰 수 만들기

> [프로그래머스 코딩테스트 연습 > 2022 KAKAO BLIND RECRUITMENT > k진수에서 소수 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/92335?language=kotlin)
> 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges

- Level2
- 탐욕법 (출제 빈도: 낮음, 평균 점수:낮음)

## 해결 과정

- k 진수로 변경하여 조건에 맞는 소수를 찾는다.

## 코드 1

```kotlin
fun solution(n: Int, k: Int): Int {
    var answer: Int = 0

    val result = covertValue(n, k)
    var calValue = StringBuilder()
    result.forEach { number ->
        if (number == '0') {
            if (calValue.toString().isNotEmpty() 
                && isPrime(calValue.toString().toLong())) {
                answer++
            }
            calValue.clear()
        } else {
            calValue.append(number)
        }
    }

    if (calValue.toString().isNotEmpty() 
        && isPrime(calValue.toString().toLong())) {
        answer++
    }

    return answer
}

private fun covertValue(n: Int, k: Int): String {
    val result = StringBuilder()
    var number = n
    while (number != 0) {
        result.append(number % k)
        number /= k
    }
    return result.reverse().toString()
}

private fun isPrime(number: Long): Boolean {
    if (number < 2) {
        return false
    }
    for (i in 2 .. sqrt(number.toDouble()).toLong()) {
        if (number % i == 0L) {
            return false
        }
    }
    return true
}
```

## 코드 2 : 다른 사람 코드

```kotlin
fun solution(n: Int, k: Int): Int {
    val s = n.toString(k)
    return s.split("0")
        .filter { p ->
            p.isNotEmpty() // swift에서는 없을수도 있음 체크
                    && p != "1"
                    && isPrimeNum(p.toBigInteger())
                    && (s.contains("0${p}0")
                    || s.contains("${p}0")
                    || s.contains("0${p}")
                    || s.contains(p))
        }
        .size
}

private fun isPrimeNum(num: BigInteger): Boolean {
    var i = 2

    while (i <= sqrt(num.toDouble())) {
        if (num % i.toBigInteger() == BigInteger.ZERO) return false
        i++
    }
    return true
}
```

## 배운 점

- Int 형으로 계산을 하게 되면 범위가 넘어 1, 11번 테스트 케이스에서 타임 아웃 발생된다.
- 변수 이름 짓기가 너무 어렵다.


