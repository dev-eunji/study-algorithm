# N-Queen

> [프로그래머스 코딩테스트 연습 > 연습문제 > N-Queen](https://programmers.co.kr/learn/courses/30/lessons/12952)
> 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges

- Level3

## 해결 과정

1. 각 행을 돌면서, 행마다 각 열의 조건을 체크하고 (`check()`) 조건을 만족하면 Q를 해당 열에 놓는다.
2. 마지막 행까지 도달했다면, `result +1`을 하고 `result`가 최종 반환 값이다.

- `arr[i]`: i 행에 몇 번째 열에 Q 가 놓여있는지 저장
- `check()`: 같은 열에 Q가 있거나 대각선에 Q가 있다면 false 반환

## 코드 1

```kotlin
class Solution {
  var result = 0
  fun solution(n: Int): Int {
      val arr = IntArray(n) { 0 }
      dfs(arr, 0, n)
      return result
  }

  private fun dfs(arr: IntArray, x: Int, n: Int) {
    if(x == n) {
        result += 1
        return
    }
    for(i in 0 until n) {
      arr[x] = i
      if(check(arr, x)) dfs(arr, x+1, n)
    }
  }

  private fun check(arr: IntArray, x: Int) : Boolean {
    for(i in 0 until x) {
      if(arr[x] == arr[i]) return false
      if(Math.abs(arr[x] - arr[i]) == x - i) return false
    }
    return true
  }
}
```

## 배운 점

- 대각선 체크
  => 가로 길이 차이 == 세로 길이 차이
  ```kotlin
  Math.abs(arr[x]-arr[i]) == Math.abs(x - i)
  ```
