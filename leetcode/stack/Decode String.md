# Decode String

> [leetcode > 394 > Decode String](https://leetcode.com/problems/decode-string)
> 출처: leetcode, [https://leetcode.com]

- Level Medium

## 해결 과정

1. HashMap을 이용하여 괄호 `[]` 안의 문자열을 `[` 문자 앞의 반복 숫자로 표현하는 문제이다.
2. 기존 저장된 문자열을 별도의 `stack`에 담아서 보관하고 합쳐준다.
3. 반복 숫자는 `count = 10 * count + (s[index] - '0') // 1자리 이상의 repeat int 값 계산`

## 코드 1

```kotlin
fun decodeString(s: String): String {
    var answer = StringBuilder()
    val stackNumber = Stack<Int>()
    val stackResult = Stack<String>()

    var index = 0
    while (index < s.length) {
        val char = s[index]
        if (char.isDigit()) {
            var count = 0
            while (s[index].isDigit()) {
                count = 10 * count + (s[index] - '0') // 1자리 이상의 repeat int 값 계산
                index++
            }
            stackNumber.push(count)
        } else if (char == '[') {
            stackResult.push(answer.toString()) // 기존
            answer.clear()
            index++
        } else if (char == ']' && stackResult.isNotEmpty()) {
            val tempString = StringBuilder(stackResult.pop()) // 기존 값 temp
            val repeatTimes: Int = stackNumber.pop()
//                tempString.append(answer.toString().repeat(Math.max(0, repeatTimes)))
            tempString.append(answer.toString().repeat(0.coerceAtLeast(repeatTimes)))
            answer.clear()
            answer.append(tempString.toString())
            index++
        } else {
            answer.append(char)
            index++
        }
    }

//        s.forEachIndexed { index, char ->
//            if (char.isDigit()) {
//                var count = 0
//                while (s[index].isDigit()) {
//                    count = 10 * count + (s[index] - '0')
//                    index++
//                }
//                stackNumber.push(char - '0')
//            } else if (char == '[') {
//                stackResult.push(answer.toString()) // 기존
//                answer.clear()
//            } else if (char == ']' && stackResult.isNotEmpty()) {
//                val tempString = StringBuilder(stackResult.pop()) // 기존 값 temp
//                val repeatTimes: Int = stackNumber.pop()
////                tempString.append(answer.toString().repeat(Math.max(0, repeatTimes)))
//                tempString.append(answer.toString().repeat(0.coerceAtLeast(repeatTimes)))
//                answer.clear()
//                answer.append(tempString.toString())
//            } else {
//                answer.append(char)
//            }
//        }
    return answer.toString()
}
```


## 코드 2: 다른 사람 코드

```Python
def decodeString(self, s):
  stack = []; curNum = 0; curString = ''
  for c in s:
      if c == '[':
          stack.append(curString)
          stack.append(curNum)
          curString = ''
          curNum = 0
      elif c == ']':
          num = stack.pop()
          prevString = stack.pop()
          curString = prevString + num*curString
      elif c.isdigit():
          curNum = curNum*10 + int(c)
      else:
          curString += c
  return curString
```

## 배운 점
1. 1자리 이상의 char 값의 변환 `count = 10 * count + (s[index] - '0') // 1자리 이상의 repeat int 값 계산`
2. `repeat` string 반복된 결과값을 리턴해준다.
```
public actual fun CharSequence.repeat(n: Int): String
```
3. for문으로 풀려고 했는데 1자리 이상 숫자 계산 부분에서 막혔다.ㅠ


