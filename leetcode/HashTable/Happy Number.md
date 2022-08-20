# Happy Number

> [leetcode > 202 > Happy Number](https://leetcode.com/problems/happy-number/submissions)
- 출처: leetcode, [https://leetcode.com]

- Level Easy [Hash Table, Two Points]

## 해결 과정

1. n 을 각 자릿수별로 나눈다.
2. 나눈 수를 각각 제곱한 다음에 더한다.
3. 더한 수가 1이 되면 Happy Number
4.  위 세 과정을 계속해서 반복하며 Happy Number 로 판단되는 경우 true 를 리턴하고 영원히 반복되는 Cycle 을 형성하는 경우 false 를 리턴합니다. 


## 코드 1 (Recursive, Iterative)

```kotlin (HashTable)
fun isHappy(n: Int): Boolean {
    var number = n
    val hashSet = HashSet<Int>()

    while (number != 1) {
        if (!hashSet.add(number)) {
            return false
        }

        var result = 0
        while (number != 0) {
            result += (number % 10) * (number % 10)
            number /= 10
        }
        number = result
    }

    return true
}
```

```kotlin (Two Pointer)
fun isHappyTwoPoint(n: Int): Boolean {
    var slow = getNext(n)
    var fast = getNext(getNext(n))

    while (slow != 1 && fast != 1) {
        if (slow == fast) return false

        slow = getNext(slow)
        fast = getNext(getNext(fast))
    }
    return true
}

private fun getNext(number: Int): Int {
    var sum = 0
    var numberValue = number
    while (numberValue != 0) {
//            Math.pow(numberValue.toDouble() % 10, 2.0)
        sum += (numberValue % 10) * (numberValue % 10)
        numberValue /= 10
    }
    return sum
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
int digitSquareSum(int n) {
    int sum = 0, tmp;
    while (n) {
        tmp = n % 10;
        sum += tmp * tmp;
        n /= 10;
    }
    return sum;
}

bool isHappy(int n) {
    int slow, fast;
    slow = fast = n;
    do {
        slow = digitSquareSum(slow);
        fast = digitSquareSum(fast);
        fast = digitSquareSum(fast);
    } while(slow != fast);
    if (slow == 1) return 1;
    else return 0;
}
```

## 배운 점
1. `n % 10` `n /= 10` 각 자리수 계산 방법 복습
2. hashSet 사용 및 Tow Point로 풀는 방법을 캐치 해야된다. 
- cycle 경우 two point를 써서 싸이클이 있는지 검사 할때 많이 쓰는 것 같다.


