# 3Sum Closest

> [leetcode > 16 > 3Sum Closest](https://leetcode.com/problems/3sum-closest)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Two Pointer]

## 해결 과정

1. 주어진 배열에서 3개의 합이 target에 가까운 값을 찾는 문제
2. 배열 루프를 도는 first + twoPoint left + twoPoint right의 합을 계산한다.
 - 루프는 `0 ~ nums.size - 2` 돌면서 `1 ~ nums.size - 1` twoPint 
3. 조건에 맞으면 값 리턴, 
4. 조건이 크면 right--, 작으면 left++ 범위를 좁혀간다.
5. 가장 가까운 target값 left 리턴


## 코드 1

```kotlin
fun threeSumClosest(nums: IntArray, target: Int): Int {
    if (nums.size < 3) return 0

    nums.sort()
    var closestSum = Integer.MAX_VALUE

    for (first in 0 until nums.size - 2) {
        var secondTwoPointLeft = first + 1
        var thirdTwoPointRight = nums.size - 1

        while (secondTwoPointLeft < thirdTwoPointRight) {
            val currentSum = nums[first] + nums[secondTwoPointLeft] + nums[thirdTwoPointRight]
            if (currentSum == target) return currentSum

            if (abs(target - closestSum) > abs(target - currentSum)) {
                closestSum = currentSum
            }
            // two point move
            if (currentSum > target) {
                thirdTwoPointRight--
            } else {
                secondTwoPointLeft++
            }
        }
    }
    return closestSum
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
int threeSumClosest(vector<int> &num, int target) {        
    vector<int> v(num.begin(), num.end()); // I didn't wanted to disturb original array.
    int n = 0;
    int ans = 0;
    int sum;
    
    sort(v.begin(), v.end());
    
    // If less then 3 elements then return their sum
    while (v.size() <= 3) {
        return accumulate(v.begin(), v.end(), 0);
    }
    
    n = v.size();
    
    /* v[0] v[1] v[2] ... v[i] .... v[j] ... v[k] ... v[n-2] v[n-1]
     *                    v[i]  <=  v[j]  <= v[k] always, because we sorted our array. 
     * Now, for each number, v[i] : we look for pairs v[j] & v[k] such that 
     * absolute value of (target - (v[i] + v[j] + v[k]) is minimised.
     * if the sum of the triplet is greater then the target it implies
     * we need to reduce our sum, so we do K = K - 1, that is we reduce
     * our sum by taking a smaller number.
     * Simillarly if sum of the triplet is less then the target then we
     * increase out sum by taking a larger number, i.e. J = J + 1.
     */
    ans = v[0] + v[1] + v[2];
    for (int i = 0; i < n-2; i++) {
        int j = i + 1;
        int k = n - 1;
        while (j < k) {
            sum = v[i] + v[j] + v[k];
            if (abs(target - ans) > abs(target - sum)) {
                ans = sum;
                if (ans == target) return ans;
            }
            (sum > target) ? k-- : j++;
        }
    }
    return ans;
}
```

## 배운 점
1. 투포인터는 기본적으로 정렬이 되어 있어야 된다. (복습)


