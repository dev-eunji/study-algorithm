# Kth Largest Element in a Stream

> [leetcode > 703 > Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/). 
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Heep]

## 해결 과정

1. k, nums 배열을 초기값으로 입력받고, 정수값 val을 nums 배열에 추가하는 함수 add를 제공할 때, k번째로 큰 원소를 찾기위한 클래스를 설계해라.
2. PriorityQueue 를 통해 정렬하고 k번째까지 offer 하고 리턴


## 코드 1 (Recursive, Iterative)

```kotlin
class KthLargest(val k: Int, val nums: IntArray) {

    private val priorityQueue = PriorityQueue<Int>(k)

    init {
        nums.forEach {
            add(it)
        }
    }

    fun add(`val`: Int): Int {
        priorityQueue.offer(`val`)
        if (priorityQueue.size > k) {
            priorityQueue.poll()
        }
        return priorityQueue.peek()
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * var obj = KthLargest(k, nums)
 * var param_1 = obj.add(`val`)
 */
```

## 배운 점
1. `PriorityQueue` 복습
- 정렬 방식 IDE가 없으면 헷갈리는 외우는게 좋은것 같다.
```Kotlin
val priorityQueue = PriorityQueue<Int>( compareByDescending{it} )
val priorityQueue = PriorityQueue<Int>(compareBy { it })
val minHeap = PriorityQueue<Int>()
val maxHeap = PriorityQueue<Int>(Collections.reverseOrder())
```

