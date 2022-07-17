# Best Time to Buy and Sell Stock

> [leetcode > 121 > Best Time to Buy and Sell Stock](https://leetcode.com/problems/linked-list-cycle-ii)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Greedy]

## 해결 과정

1. list 순회하면서 가장 작은 값을 찾는다.
2. maxProfit = buy - sell 가장 큰 이득을 찾는다.


## 코드 1

```kotlin
fun maxProfit(prices: IntArray): Int {
    var buy = prices.first()
    var maxProfit = 0
    prices.forEach { price ->
        buy = buy.coerceAtMost(price) // min
        maxProfit = maxProfit.coerceAtLeast(price - buy) // max
    }

    return maxProfit
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
public int maxProfit(int[] prices) {
    int maxCur = 0, maxSoFar = 0;
    for(int i = 1; i < prices.length; i++) {
        maxCur = Math.max(0, maxCur += prices[i] - prices[i-1]);
        maxSoFar = Math.max(maxCur, maxSoFar);
    }
    return maxSoFar;
}
```

## 배운 점
1. `kotlin coerceAtMost, coerceAtLeast` 
`
/**
 * Ensures that this value is not greater than the specified [maximumValue].
 * 
 * @return this value if it's less than or equal to the [maximumValue] or the [maximumValue] otherwise.
 * 
 * @sample samples.comparisons.ComparableOps.coerceAtMost
 */
public fun Int.coerceAtMost(maximumValue: Int): Int {
    return if (this > maximumValue) maximumValue else this
}
`

`
/**
 * Ensures that this value is not less than the specified [minimumValue].
 * 
 * @return this value if it's greater than or equal to the [minimumValue] or the [minimumValue] otherwise.
 * 
 * @sample samples.comparisons.ComparableOps.coerceAtLeast
 */
public fun Int.coerceAtLeast(minimumValue: Int): Int {
    return if (this < minimumValue) minimumValue else this
}
`

