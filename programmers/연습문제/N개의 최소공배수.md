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

## 코드 2 : orange4912

```kotlin
fun solution(arr: IntArray): Int {
  if (arr.size < 1 || arr.size >= 100) return 0
  var answer = arr[0]
  arr.forEach {
      answer = lcm(answer, it)
  }
  return answer
}

fun gcd(a: Int, b: Int): Int = if (b == 0) a else gcd(b, a % b)
fun lcm(a: Int, b: Int): Int = a * b / gcd(a, b)
```

## 배운 점

- 소인수분해 코드

```kotlin
for(i in 2..num) {
    while(num % i == 0) num/=i
}
```

- 최대공약수, 최소공배수는 기본적으로 숙지하자.

## 질문

- Int 의 제곱을 구할 때 `.toDouble()` 로 형변환을 하면서 `pow()` 함수를 사용하는 것 vs. 직접구현

  > ide가 없는 경우 case exception 발생 할 가능성이 있지만 개인적으로는 직접 구현 시 디버깅(오류 및 오타)으로 함수 사용이 좋지 않을까 하는 의견입니다.
  > imprt java.util.\* 필수로 쓰고 시작하는게 편한것 같습니다.

- sqrt : 제곱근
  `public actual inline fun sqrt(x: Double): Double = nativeMath.sqrt(x)`

- pow : n 제곱 수
  `public actual inline fun Double.pow(n: Int): Double = nativeMath.pow(this, n.toDouble())`

- hypot : 두 수 각각의 제곱 수를 합한 수의 제곱근
  `public actual inline fun hypot(x: Double, y: Double): Double = nativeMath.hypot(x, y)`

각 인수들과 반환형은 Double 형이므로 이점을 사용할 때 주의하여야 한다.

- 코드2 구현 👍👍
  - 2개의 최소공배수를 구할때와 동일하게 N개의 최소공배수도 구할 수 있다.
