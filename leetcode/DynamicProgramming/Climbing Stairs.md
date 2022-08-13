# Climbing Stairs

> [leetcode > 70 > Climbing Stairs](https://leetcode.com/problems/climbing-stairs)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Dynamic Programming]

## 해결 과정

1. 동적프로그래밍 DP를 이용하여 분할하여 값을 계산합니다. 피보나치 수열과 유사하게 n-1 + n-2 에서의 경우의 수를 합치면 n번째의 가능한 경우의 수가 나오므로 앞에서부터 분할하여 정복
- ways(n) = ways(n-1) + ways(n-2)
- ways(1) = fib(2) = 1
- ways(2) = fib(3) = 2
- ways(3) = fib(4) = 3

- Input: N = 4

                  fib(5)
           '3'  /        \   '2'
               /          \
           fib(4)         fib(3)
     '2'  /      \ '1'   /      \  
         /        \     /        \ 
     fib(3)     fib(2)fib(2)      fib(1) 
     /    \ '1' /   \ '0'
'1' /   '1'\   /     \ 
   /        \ fib(1) fib(0) 
fib(2)     fib(1)


## 코드 1

```kotlin
fun climbStairs(n: Int): Int {
    if (n <= 1) return 1

    val dp = IntArray(n + 1)
    dp[1] = 1
    dp[2] = 2

    for (i in 2 .. n) {
        dp[i] = dp[i - 1] + dp[i - 2]
    }
    return dp[n]
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```java
public int climbStairs(int n) {
    // base cases
    if(n <= 0) return 0;
    if(n == 1) return 1;
    if(n == 2) return 2;
    
    int one_step_before = 2;
    int two_steps_before = 1;
    int all_ways = 0;
    
    for(int i=2; i<n; i++){
    	all_ways = one_step_before + two_steps_before;
    	two_steps_before = one_step_before;
      one_step_before = all_ways;
    }
    return all_ways;
}
```

``` c++
int climbStairs(int n) {
    int a = 1, b = 1;
    while (n--)
        a = (b += a) - a;
    return a;
}
```

## 배운 점
1. 경우의 수를 계산하는 여러가지 방법을 배


