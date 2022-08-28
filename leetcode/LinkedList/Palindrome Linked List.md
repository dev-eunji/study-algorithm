# Palindrome Linked List

> [leetcode > 234 > Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list)
- 출처: leetcode, [https://leetcode.com]

- Level Easy (이게 Easy ㅠ)

## 해결 과정

1. slow, fast 방법 (two point)
- 1) 1번 pointer는 head부터 시작해서 1개씩, 2번 pointer는 head부터 시작해서 2개씩 next로 간다
  2) `O(n) time and O(1) space` 조건으로 뒤집은 연결 리스트를 사용 할 수 없다.
  3) 중간 지점을 찾는다. `fast?.next != null`
  4) 중간 지점 부터 tail 까지 뒤집는다.
  5) 앞의 노드, 뒤집은 뒤의 노드를 비교한다.


## 코드 1

```kotlin
fun isPalindrome(head: ListNode?): Boolean {
    if (head == null) {
        return true
    }

    var fast = head
    var slow = head
    // find mid
    while (fast?.next != null) {
        fast = fast.next?.next
        slow = slow?.next
    }

    // 홀수 이면 가운데 값 비교 필요 없다.
    if (fast != null) {
        slow = slow?.next
    }

    var leftNode = head
    var tailReverseNode = slow?.reverse()
    while (leftNode != null && tailReverseNode != null) {
        if (leftNode.`val` != tailReverseNode.`val`) {
            return false
        }
        leftNode = leftNode?.next
        tailReverseNode = tailReverseNode?.next
    }
    return true
}

private fun ListNode.reverse(): ListNode? {
    var node: ListNode? = this
    var tail: ListNode? = null
    while (node != null) {
        val next = node.next
        node.next = tail
        tail = node
        node = next
    }
    return tail
}
```

## 코드 2 ()

```Java
public boolean isPalindrome(ListNode head) {
    ListNode fast = head, slow = head;
    while (fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
    }
    if (fast != null) { // odd nodes: let right half smaller
        slow = slow.next;
    }
    slow = reverse(slow);
    fast = head;
    
    while (slow != null) {
        if (fast.val != slow.val) {
            return false;
        }
        fast = fast.next;
        slow = slow.next;
    }
    return true;
}

public ListNode reverse(ListNode head) {
    ListNode prev = null;
    while (head != null) {
        ListNode next = head.next;
        head.next = prev;
        prev = head;
        head = next;
    }
    return prev;
}
public boolean isPalindrome(ListNode head) {
    ListNode temp = head;
    Stack stack = new Stack();
    while (temp != null) {
        stack.push(temp.val);
        temp = temp.next;
    }

    while (head != null) {
        if (head.val != (int)stack.pop()) {
            return false;
        }
        head = head.next;
    }
    return true;
}
```

## 배운 점
1. slow, fast two point로 회문 여뷸를 알 수 있다.
2. 회문 검사 시 `O(1) space` 이면 중간에서 뒤집어 비교 해야된다. (데칼코마니 형태)
3. 홀수면 `11211` 2는 비교 할 필요가 없다.
4. linkedList 뒤집는 방법
5. 이게 Easy 라니 어렵다. 

