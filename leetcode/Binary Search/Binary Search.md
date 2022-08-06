# Binary Search

> [leetcode > 704 > Binary Search](https://leetcode.com/problems/binary-search)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Binary Search]

## 해결 과정

1. 이진 탐색 
 - left, right 중간값 pivot을 중심으로 타겟 값을 비교하여 범위를 줄이며 탐색한다.


## 코드 1

```kotlin
fun search(nums: IntArray, target: Int): Int {
    var left = 0
    var right = nums.lastIndex
    var pivot: Int

    while (left <= right) {
        pivot = (left + right) / 2
        if (nums[pivot] == target) {
            return pivot
        } else if (nums[pivot] < target) {
            left = pivot + 1
        } else {
            right = pivot - 1
        }
    }

    return -1 // 해당 index 없으면 -1 리턴
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
int search(vector<int>& nums, int target) {
    int n = nums.size()-1;
    int low = 0, high = n;
    while( low <= high){
        int mid = low + (high-low)/2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] > target) high = mid -1;
        else low = mid + 1;
    }
    return -1;
}
```

## 배운 점
1. 이진탐색 복습 
