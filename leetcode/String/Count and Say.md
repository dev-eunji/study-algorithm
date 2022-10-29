# Count and Say

> [leetcode > 38 > Count and Say](https://leetcode.com/problems/count-and-say)
> 출처: leetcode, [https://leetcode.com]

- Medium

## 해결 과정

1. 주어진 문자열 숫자를 개수, 숫자, 개수, 숫자, ...가 되도록 n번 반복했을 때 return값 구하기
2. 아래와 같이 숫자가 중가하면서 동일 문자롤 숫자로 변환을 반복한다. (처음에 문제 이해가 어렵다.)
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
![img](https://user-images.githubusercontent.com/8637598/198813302-6cf26b08-8e99-40d1-9aee-33251272101f.png)

## 코드 1

```kotlin
fun countAndSay(n: Int): String {
    if (n < 2) return "1"

    var countAndSay = "1"
    for (i in 1 until n) {
        countAndSay = traverse(countAndSay)
    }

    return countAndSay
}

private fun traverse(current: String): String {
    if (current.isEmpty()) {
        return current
    }
    var result = ""
    var count = 1
    var currentChar = current[0]

    for (i in 1 until current.length) {
        if (currentChar != current[i]) {
            result += count.toString() + currentChar
            currentChar = current[i]
            count = 1
        } else {
            count++
        }
    }
    result += count.toString() + currentChar
    return result
}
```

## 코드 2 다른 사람 코드

``` Java
public class Solution {
    public String countAndSay(int n) {
        if(n <= 0) return "-1";
        String result = "1";
        
        for(int i = 1; i < n; i ++) {
            result = build(result);
        }
        return result;
    }
    
    private String build(String result) {
        StringBuilder builder = new StringBuilder();
        int p = 0;
        while(p < result.length()) {
            char val = result.charAt(p);
            int count = 0;
            
            while(p < result.length() && 
              result.charAt(p) == val){
                p ++;
                count ++;
            }
            builder.append(String.valueOf(count));
            builder.append(val);
        }
        return builder.toString();
    }
}
```

## 배운 점
1. 문제 예시를 잘 봐야된다.
2. `String`을 계속 변환한다면 StringBuilder 시용하자.

