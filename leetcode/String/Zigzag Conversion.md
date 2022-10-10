# Zigzag Conversion

> [leetcode > 6 > Zigzag Conversion](https://leetcode.com/problems/zigzag-conversion)
> 출처: leetcode, [https://leetcode.com]

- Medium

## 해결 과정

1. 지정된 수의 행에 지그재그 패턴으로 문자를 만들고, 한줄씩(가로) 읽어 string을 리턴하는 문제
2. StringBuilder list를 만들어, numRow에 맟춰서 문자를 append해준다.

## 코드 1

```kotlin
fun convert(s: String, numRows: Int): String {
    if (numRows == 1) {
        return s
    }
    val stringBuilderList = mutableListOf<StringBuilder>()
    for (i in 0 until s.length.coerceAtMost(numRows)) {
        stringBuilderList.add(StringBuilder())
    }
    var courrentRow = 0
    var goingDown = false
    s.forEach{ char ->
        stringBuilderList[courrentRow].append(char)
        if (courrentRow == 0 || courrentRow == numRows - 1) {
            goingDown = !goingDown
        }
        courrentRow += if (goingDown) {
            1
        } else {
            -1
        }
    }
    val answer = StringBuilder()
    stringBuilderList.forEach {
        answer.append(it)
    }
    return answer.toString()
}

fun convert(s: String, numRows: Int): String {
    if (numRows < 2) return s

    val stringBuilderList = mutableListOf<StringBuilder>()
    for (i in 0 until s.length.coerceAtMost(numRows)) {
        stringBuilderList.add(StringBuilder())
    }

    var index = 0
    while (index < s.length) {
        for (i in 0 until numRows) {
            stringBuilderList[i].append(s.get(index++))
            if (index == s.length) break
        }
        for (i in numRows - 2 downTo 1) {
            stringBuilderList[i].append(s.get(index++))
            if (index == s.length) break
        }
    }
    val answer = StringBuilder()
    stringBuilderList.forEach {
        answer.append(it)
    }
    return answer.toString()
}
```


## 코드 2 ()

```java
public String convert(String s, int nRows) {
    char[] c = s.toCharArray();
    int len = c.length;
    StringBuffer[] sb = new StringBuffer[nRows];
    for (int i = 0; i < sb.length; i++) sb[i] = new StringBuffer();
    
    int i = 0;
    while (i < len) {
        for (int idx = 0; idx < nRows && i < len; idx++) // vertically down
            sb[idx].append(c[i++]);
        for (int idx = nRows-2; idx >= 1 && i < len; idx--) // obliquely up
            sb[idx].append(c[i++]);
    }
    for (int idx = 1; idx < sb.length; idx++)
        sb[0].append(sb[idx]);
    return sb[0].toString();
}
```

## 배운 점
1. 문자열 조작하는 여러가지 방법을 배웠다.
2. 자바에서는 `idx < nRows && i < len` for문에 조건을 두개 걸 수 있는데 koltin의 방법은? 찾아봐야겠다.

