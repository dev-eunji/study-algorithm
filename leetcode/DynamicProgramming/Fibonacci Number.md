# Fibonacci Number

> [leetcode > 509 > Fibonacci Number](https://leetcode.com/problems/fibonacci-number)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Dynamic Programming]

## 해결 과정

1. 메모제이션 or 바텀 업 or 탑 다운


## 코드 1

```kotlin
fun fibRecursive(n: Int): Int {
    if (n < 2) {
        return n
    }
    return fibRecursive(n - 1) + fibRecursive(n - 2)
}

fun fibMemoization(n: Int): Int {
    val arr = IntArray(n + 1)
    arr[0] = 0
    arr[1] = 1
    if (n < 2) {
        return arr[n]
    }
    for (i in 2 until n + 1) {
        arr[i] = arr[i - 2] + arr[i - 1]
    }
    return arr[n]
}

fun fibBottomUp(n: Int): Int {
    if (n <= 1) {
        return n
    }
    var first = 0
    var second = 1
    var next = 0
    for (i in 0 until n - 1) {
        next = first + second
        first = second
        second = next
    }
    return next
}

fun fibTopDown(n: Int): Int {
    val arr = IntArray(n + 1)
    if (arr[n] > 0) {
        return arr[n]
    }
    return if (n <= 1) {
        n
    } else {
        arr[n] = fibTopDown(n - 1) + fibTopDown(n - 2)
        arr[n]
    }
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
class Solution {
  public int fib(int n) {
      // edge cases
      if(n <= 1){
          return n;
      }

      // initialization
      int first = 0, second = 1, third = 1;

      // iterate from i = 2 to n to get 
      // the nth Fibonacci number
      for(int i = 2;i <= n;i++){
          third = first + second;
          first = second;
          second = third;
      }

      return third;
  }
}
```

## 배운 점
1. 피보나치수열을 재귀로만 알고 있었는데 여러 가지 방법으로 풀 수 있다.


