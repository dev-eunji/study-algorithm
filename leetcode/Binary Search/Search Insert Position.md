# Search Insert Position

> [leetcode > 35 > Search Insert Position](https://leetcode.com/problems/search-insert-position/?envType=study-plan&id=algorithm-i)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Binary Search]

## 해결 과정

1. 이진 탐색
2. 정렬된 array가 주어질 때 target 값이 들어가 있는 or 들어가 갈 index 반환


## 코드 1

```kotlin
fun searchInsert(nums: IntArray, target: Int): Int {
    var left = 0
    var right = nums.size - 1
    var pivot: Int

    while (left <= right) {
        pivot = left + (right - left) / 2

        when {
            nums[pivot] == target -> {
                return pivot
            }
            nums[pivot] > target -> {
                right--   
            }
            nums[pivot] < target -> {
                left++   
            }
        }
    }
    return left
}
```

## 코드 2 (다른 사람 코드 Most Votes)

``` c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int low = 0, high = nums.size()-1;

        // Invariant: the desired index is between [low, high+1]
        while (low <= high) {
            int mid = low + (high-low)/2;

            if (nums[mid] < target)
                low = mid+1;
            else
                high = mid-1;
        }

        // (1) At this point, low > high. That is, low >= high+1
        // (2) From the invariant, we know that the index is between [low, high+1], so low <= high+1. Follwing from (1), now we know low == high+1.
        // (3) Following from (2), the index is between [low, high+1] = [low, low], which means that low is the desired index
        //     Therefore, we return low as the answer. You can also return high+1 as the result, since low == high+1
        return low;
    }
};
```

