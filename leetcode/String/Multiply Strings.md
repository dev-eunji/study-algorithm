# Multiply Strings

> [leetcode > 43 > Multiply Strings](https://leetcode.com/problems/bulls-and-cows/)
- 출처: leetcode, [https://leetcode.com]

- Level Medium

## 해결 과정

1. 문자열 char를 숫자로 변경하여 곱한다.

## 코드 1

```kotlin
fun multiply(num1: String, num2: String): String {
    if ("0" == num1 || "0" == num2) return "0"

    val result = IntArray(num1.length + num2.length)
    for (i in num1.length - 1 downTo 0) {
        for (j in num2.length - 1 downTo 0) {
            val n1 = num1[i] - '0'
            val n2 = Integer.valueOf(num2[j] - '0')
            result[i + j + 1] += n1 * n2
        }
    }

    for (i in result.size - 1 downTo 1) {
        result[i - 1] += result[i] / 10
        result[i] = result[i] % 10
    }


    val answer = StringBuilder("")
    result.forEach {
        if (!(answer.isEmpty() && it == 0)) {
            answer.append(it)
        }
    }
    return if (answer.toString().isEmpty()) "0" else answer.toString()
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```Java
public String multiply(String num1, String num2) {
    int m = num1.length(), n = num2.length();
    int[] pos = new int[m + n];
   
    for(int i = m - 1; i >= 0; i--) {
        for(int j = n - 1; j >= 0; j--) {
            int mul = (num1.charAt(i) - '0') * (num2.charAt(j) - '0'); 
            int p1 = i + j, p2 = i + j + 1;
            int sum = mul + pos[p2];

            pos[p1] += sum / 10;
            pos[p2] = (sum) % 10;
        }
    }  
    
    StringBuilder sb = new StringBuilder();
    for(int p : pos) if(!(sb.length() == 0 && p == 0)) sb.append(p);
    return sb.length() == 0 ? "0" : sb.toString();
}
```

## 배운 점
1. `- '0'` char to Int
2. 두 수의 곱은 num1.length + num2.length -1 을 넘지 않는다.
3. 목, 나머지 구하는 부분 복습


