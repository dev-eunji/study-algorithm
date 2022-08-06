# Add Two Numbers

> [leetcode > 2 > Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
> 출처: leetcode, [https://leetcode.com]

- Medium

## 해결 과정

1. LinkedList 순회하면서 값을 더한다. (반대로 계산이라고 되어 있지만 순방향으로 더하면 된다.)
2. 반올림 값이 있으면 값 더하고, 마지막 노드 추가

## 코드 1

```kotlin
fun addTwoNumbers(l1: ListNode?, l2: ListNode?): ListNode? {
  var firstNode = l1
  var secondNode = l2
  var answerNode = ListNode(0)
  var currentNode = answerNode

  var carry = 0
  while (firstNode != null || secondNode != null) {
      var x = firstNode?.`val` ?: 0
      var y = secondNode?.`val` ?: 0

      val sum = carry + x + y
      carry = sum / 10
      currentNode.next = ListNode( sum % 10)
      currentNode = currentNode.next ?: ListNode(0)

      if (firstNode != null) {
          firstNode = firstNode.next
      }
      if (secondNode != null) {
          secondNode = secondNode.next
      }
  }

  if (carry > 0) {
      currentNode.next = ListNode(carry)
  }
  return answerNode.next
}
```

## 코드 2: 다른 사람 코드

```kotlin
fun ListNode?.value() = this?.`val` ?: 0

fun addTwoNumbers(l1: ListNode?, l2: ListNode?, carry: Int = 0): ListNode? {
    if (l1 == null && l2 == null && carry == 0) return null
    val s = l1.value() + l2.value() + carry
    return ListNode(s % 10).apply { next = addTwoNumbers(l1?.next, l2?.next, s / 10) }
}

## 배운 점
1. 기본적인 링크드 리스트 구현 (문제에 반대로라는 말 때문에 고민된 문제)
2. LinkedList Head Node가 필요하다. (오랜만에 푸니 생각보다 헷갈린다.)

