# Maximum 69 Number

> [leetcode > 1323 > Maximum 69 Number](https://leetcode.com/problems/maximum-69-number)
> 출처: leetcode, [https://leetcode.com]
- Level Easy [Greedy]

## 해결 과정

1. 6 & 9로 이루어진 수를 한 자리 수를 변경하여 얻을 수 있는 최대 수를 반환


## 코드 1

```kotlin
fun maximum69Number (num: Int): Int {
    var numCopy = num
    var index = -1
    var currentDigit = 0

    while (numCopy > 0) {
        if (numCopy % 10 == 6) {
            index = currentDigit
        }

        numCopy /= 10
        currentDigit++
    }

    return if (index == -1) {
         num
    } else {
        num + 3 * 10.0.pow(index.toDouble()).toInt()
    }
}

fun maximum69Number (num: Int): Int {
    return num.toString().replaceFirst("6", "9").toInt()
}
```

## 배운 점
1. Check the remainder 알고리즘으로 변경된 자리수의 값을 구할수 있다. 
- ![image](https://user-images.githubusercontent.com/8637598/201510374-3ecfaf0b-fab1-4010-b7fe-c5c5e51d88c6.png)
