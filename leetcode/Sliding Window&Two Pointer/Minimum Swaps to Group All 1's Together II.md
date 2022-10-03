# Minimum Swaps to Group All 1's Together II

> [leetcode > 2134 > Minimum Swaps to Group All 1's Together II](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Sliding Window/Two Pointer]

## 해결 과정

1. 배열에서 '1'의 개수 세기 
2. 배열을 순회하며 각 지점에서 1이 연속적으로 위치하려면 얼마나 swap이 필요한지 세기
3. 슬라이딩 윈도우를 이동 시키며 계산


## 코드 1

```kotlin
fun minSwaps(nums: IntArray): Int {
    val ones = nums.count { it == 1 } // sliding window length
    if (ones <= 1) {
        return 0
    }

    var maxOnes = 0 // maxOnes in sub array of length ones
    for (i in 0 until ones) {
        if (nums[i] == 1) {
            maxOnes++
        }
    }
    var count = maxOnes
    for (i in ones until nums.size + ones) {
        if (nums[i - ones] == 1) { // if element removing from window is 1, then decrease count.
            count--
        }
        if (nums[i % nums.size] == 1) { // if element adding to window is 1, then increase count.
            count++
        }
        maxOnes = maxOnes.coerceAtLeast(count)
    }
    return ones - maxOnes
}

fun minSwaps1(nums: IntArray): Int {
    val ones = nums.count { it == 1 } // sliding window length
    if (ones <= 1) {
        return 0
    }

    var maxOnes = 0 // maxOnes in sub array of length ones
    for (i in 0 until ones) {
        if (nums[i] == 1) {
            maxOnes++
        }
    }
    var minimum = ones - maxOnes
    for (i in 1 until nums.size) {
        maxOnes -= nums[i - 1]
        maxOnes += nums[(i + ones - 1) % nums.size]
        minimum = minimum.coerceAtMost(ones - maxOnes)
    }
    return minimum
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
public int minSwaps(int[] nums) {
    int ones = 0, x = 0, onesInWindow = 0, i = 0, n = nums.length;
    for (int v: nums)
        if (v == 1) ones++;
    int nums2[] = new int[n * 2];
    for (i = 0; i < n * 2; i++)
        nums2[i] = nums[i % n];
    for (i = 0; i < n * 2; i++) {
        if (i >= ones && nums2[i - ones] == 1) x--;
        if (nums2[i] == 1) x++;
        onesInWindow = Math.max(x, onesInWindow);
    }
    return ones - onesInWindow;
}
```

## 배운 점
1. 슬라이딩 윈도우를 배웠다(복습).
2. max, min을 정해서 로직을 구현해야 된다.

