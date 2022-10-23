# String to Integer (atoi)

> [leetcode > 8 > String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi)
> 출처: leetcode, [https://leetcode.com]

- Medium

## 해결 과정

1. 문자를 숫자로 바꾸는 문제이다.
2 제약 조건에 맞게 변경
- 공백이 아닌 문자가 나올 때 까지 최대한 많은 공백을 제거한다
- 첫번째 문자가 + 또는 -인 경우 부호를 택한다.
- 그런다음 등장하는 숫자 모두를 integer로 변환한다.
- 이후에도 문자가 나올 수 있으나 integer변환 이후에 등장하는 문자는 변환에 아무런 영향을 주지 않으므로 무시한다.
- 만약 공백 제거 이후 첫번째 문자가 숫자가 아닌 경우 또는 공백 제거 이후 문자열이 존재하지 않는 경우에는 변환이 일어나지 않는다. 리턴 0

## 코드 1

```kotlin
fun myAtoi(s: String): Int {
    // Base condition
    if (s.isEmpty() || s.all{ it == ' '}) return 0

    // Counter
    var index = 0

    // Remove Spaces
    while (index < s.length && s[index] == ' ') {
        index++
    }

    // Handle signs
    var sign = 1
    if (s[index] === '+' || s[index] === '-') {
        sign = if (s[index] === '+') 1 else -1
        index++
    }

    // This will store the converted number
    var number = 0
    // Loop for each numeric character in the string iff numeric characters are leading
    // characters in the string
    while (index < s.length && s[index] >= '0' && s[index] <= '9') {

        val digit = s[index] - '0'
        if (Int.MAX_VALUE / 10 < number || Int.MAX_VALUE / 10 == number && Int.MAX_VALUE % 10 < digit) {
            return if (sign == 1) {
                Int.MAX_VALUE
            } else {
                Int.MIN_VALUE
            }
        }
        number = number * 10 + digit
        index++
    }
    return number * sign
}
```

## 코드 2 다른 사람 코드

```kotlin
public static int myAtoi(String s) {
    String str = s.stripLeading().split("\\s+")[0];

    if (str.length() == 0) {
        return 0;
    } else if (str.charAt(0) == '+') {
        return convert(str.substring(1), false);
    } else if (str.charAt(0) == '-') {
        return convert(str.substring(1), true);
    } else if (Character.isDigit(str.charAt(0))) {
        return convert(str, false);
    } else {
        return 0;
    }
}

public static int convert(String s, boolean isNegative) {
    long value = 0;

    for (int idx = 0; idx < s.length() && Character.isDigit(s.charAt(idx)); idx++) {
        value = value * 10 + Character.getNumericValue(s.charAt(idx));

        if (value > Integer.MAX_VALUE) {
            return isNegative ? Integer.MIN_VALUE : Integer.MAX_VALUE;
        }
    }

    return (int) (isNegative ? -value : value);
}
```

## 배운 점
1. 문자에서 공백을 제거하기 위해 `replace`를 사용했는데 그럼 "   +0 123" 케이스에서 0다음 공백도 치환되어 오답이 나온다.
2. Int 범위 내에 있는지 검사 하는 방법
```
if (Int.MAX_VALUE / 10 < number || Int.MAX_VALUE / 10 == number && Int.MAX_VALUE % 10 < digit)
```
3. 문자열 자리수 별로 숫자 변환
```
number = number * 10 + digit
```

4. 특정 예외 케이스가 하나씩 생겨서 어렵다. (문제 이해가 선행되어야 시간을 줄일 수 있다.)

