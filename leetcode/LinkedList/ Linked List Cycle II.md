# Linked List Cycle II

> [leetcode > 142 > Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii)
> 출처: leetcode, [https://leetcode.com]

- Level Medium

## 해결 과정

1. set 이용하는 방법
2. slow, fast 방법 (two point)
- ![image](https://user-images.githubusercontent.com/8637598/179339950-ebffd175-504a-4a4d-a39e-f33dcfc1b1b9.png)
- 1) 1번 pointer는 head부터 시작해서 1개씩, 2번 pointer는 head부터 시작해서 2개씩 next로 간다
  2) 1번 pointer와 2번 pointer가 만나면
  3) 2번 pointer를 다시 head 부터 시작해서 이제부턴 1,2번 pointer 모두 1개씩 next로 간다
  4) 1,2번 pointer가 만나는 지점이 cycle의 시작점이다




## 코드 1

```kotlin
fun detectCycle(head: ListNode?): ListNode? {
    var slow = head
    var fast = head

    while (slow?.next != null) {
        slow = slow.next
        fast = fast?.next?.next

        if (slow == fast) { // 두 포인터가 만나는 지점까지 반복
            slow = head // slow head에서 다시 시작 (fast 도 상관없음)
            while (slow != fast) {
                slow = slow?.next
                fast = fast?.next
            }
            return slow
        }
    }
    return null
}
```

## 코드 2

```kotlin
fun detectCycleSet(head: ListNode?): ListNode? {
  val set = hashSetOf<ListNode>()
  var headNode = head
  while (headNode != null) {
      if (!set.add(headNode)) {
          return headNode
      }
      headNode = headNode.next
  }

  return null
}
```

## 배운 점
1. slow, fast two point로 cycle을 알 수 있다.

