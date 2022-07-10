# Merge Two Sorted Lists

> [leetcode > 21 > Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists)
> 출처: leetcode, [https://leetcode.com]

- Level easy

## 해결 과정

1. 2개의 Linked List 비교하여 작거나 같은 경우 첫번째 노드 대입
2. 마지막 노드 추가

## 코드 1

```kotlin
fun mergeTwoLists(list1: ListNode?, list2: ListNode?): ListNode? {
    if (list1 == null && list2 == null) {
        return null
    }
    val headNode = ListNode(0)
    var mergeNode = headNode
    var firstNode = list1
    var secondNode = list2

    while (firstNode != null && secondNode != null) {
        if (firstNode.`val` <= secondNode.`val`) {
            mergeNode.next = firstNode
            firstNode = firstNode?.next
        } else {
            mergeNode.next = secondNode
            secondNode = secondNode?.next
        }
        mergeNode = mergeNode.next ?: ListNode(0)
    }

    if (firstNode != null) {
        mergeNode.next = firstNode
    } else if (secondNode != null) {
        mergeNode.next = secondNode
    }

    return headNode.next
}
```

## 코드 2: 다른 사람 코드

```kotlin
fun mergeTwoLists(list1: ListNode?, list2: ListNode?): ListNode? {
    if (list1 == null) return list2
    if (list2 == null) return list1
    return when (list1.`val`.compareTo(list2.`val`)) {
        0, 1 -> list2.apply { next = mergeTwoLists(list1, list2.next) }
        else -> list1.apply { next = mergeTwoLists(list2, list1.next) }
    }
}
```

## 배운 점
1. Linked List 복습
2. 재귀 방식으로 풀 수 있다.

