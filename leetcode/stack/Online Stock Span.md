# Online Stock Span

> [leetcode > 901 > Online Stock Span](https://leetcode.com/problems/online-stock-span)
> 출처: leetcode, [https://leetcode.com]

- Level Medium

## 해결 과정

1. 하루 동안의 주가 범위는 주가가 그 날의 가격보다 낮거나 같은 연속 일수(그 날부터 시작하여 뒤로)의 최대 수를 구하는 문제
2. 문제 이해가 어렵다.

## 코드 1

```kotlin
class StockSpanner() {
    
    private val stack = Stack<Pair<Int, Int>>()
    fun next(price: Int): Int {
        var answer = 1
        
        while (stack.isNotEmpty() && stack.peek().first <= price) {
            answer += stack.pop().second
        }
        
        stack.push(Pair(price, answer))
        return answer
    }
}

```


## 코드 2: 다른 사람 코드

``` Java
Stack<int[]> stack = new Stack<>();
  public int next(int price) {
      int res = 1;
      while (!stack.isEmpty() && stack.peek()[0] <= price)
          res += stack.pop()[1];
      stack.push(new int[]{price, res});
      return res;
  }
```
