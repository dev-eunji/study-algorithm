# Convert Sorted Array to Binary Search Tree

> [leetcode > 108 > Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree)
- 출처: leetcode, [https://leetcode.com]

- Level Easy

## 해결 과정

1. 오름차순으로 정렬되어 있는 int 배열이 주어지면 높이가 1 이상 차이나지 않는 BST 를 만드는 문제
2. 이분탐색 하듯이 트리를 순회
- 배열이 오름차순으로 되어 있기 때문에 중앙에 있는 값이 무조건 root
- 부모 노드 nums[mid] 를 만들고 나면 왼쪽 서브트리는 0 ~ mid - 1 로 만든 트리고 오른쪽 서브트리는 mid + 1 ~ nums.length - 1 로 만든 트리



## 코드 1

```kotlin
fun sortedArrayToBST(nums: IntArray): TreeNode? {
    if (nums.isEmpty()) {
        return null
    }
    return traverse(nums)
}

private fun traverse(
    nums: IntArray,
    low: Int = 0,
    high: Int = nums.size - 1
): TreeNode? {
    if (low > high) {
        return null
    }

    val mid = low + (high - low) / 2
    return TreeNode(nums[mid]).apply {
        left = traverse(nums, low, mid - 1)
        right = traverse(nums, mid + 1, high)
    }
}
```

## 배운 점
1. 균형 이진 트리는 두 하위 트리의 깊이(depth)가 1이 넘게 차이나지 않는 것을 의미힌다.
2. 예시가 너무 헷갈린다.
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:
![image](https://user-images.githubusercontent.com/8637598/188259384-be26c3e7-f01b-4169-a37e-f5f98dc324d7.png)



