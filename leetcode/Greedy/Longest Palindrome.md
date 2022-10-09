# Longest Palindrome.

> [leetcode > 409 > Longest Palindrome.](https://leetcode.com/problems/longest-palindrome)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Greedy or Expand Around Center]

## 해결 과정

1. 0부터 index를 활용해 투포인트 형태로 회문을 검사한다.
2. 아래의 코드 처럼 index 기준으로 넓혀가면서 회문 검사한다.
```
while (start >= 0 && end < s.length && s[start] == s[end]) {
  start--
  end++
}
```
3. start, end 기준을 찾아 가장 긴 회문 substring


## 코드 1

```kotlin
fun longestPalindrome(s: String): String {
    if (s.length <= 1) return s

    var answer = ""
    for (i in s.indices) {
        val longOdd = findPalindrome(s, i, i)
        val longEven = findPalindrome(s, i, i + 1)

        if (longOdd.length < longEven.length && answer.length < longEven.length) {
            answer = longEven
        } else if (longEven.length < longOdd.length && answer.length < longOdd.length) {
            answer = longOdd
        }
    }
    return answer
}

private fun findPalindrome(s: String, start: Int, end: Int): String {
    var start = start
    var end = end

//        val stringBuilder = StringBuilder()
    while (start >= 0 && end < s.length && s[start] == s[end]) {
//            if (start == end) {
//                stringBuilder.append(s[start])
//            } else {
//                stringBuilder.insert(0, s[start])
//                stringBuilder.append(s[end])
//            }
        start--
        end++
    }
    // Palindrome length == end - start - 1 or start + 1 + end
    return s.substring(start + 1, end)
}
```

## 솔루션 (Expand Around Center)
``` java
fun longestPalindrome1(s: String?): String? {
    if (s == null || s.isEmpty()) return ""
    var start = 0
    var end = 0
    for (i in s.indices) {
        val len1 = expandAroundCenter(s, i, i)
        val len2 = expandAroundCenter(s, i, i + 1)
        val len = len1.coerceAtLeast(len2)
        if (len > end - start) {
            start = i - (len - 1) / 2
            end = i + len / 2
        }
    }
    return s.substring(start, end + 1)
}

private fun expandAroundCenter(s: String, left: Int, right: Int): Int {
    var L = left
    var R = right
    while (L >= 0 && R < s.length && s[L] == s[R]) {
        L--
        R++
    }
    return R - L - 1
}
```

## 코드 2 (다른 사람 코드 Most Votes) DP 방식

```c++
public String longestPalindrome(String s) {
  int n = s.length();
  String res = null;
    
  boolean[][] dp = new boolean[n][n];
    
  for (int i = n - 1; i >= 0; i--) {
    for (int j = i; j < n; j++) {
      dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i < 3 || dp[i + 1][j - 1]);
            
      if (dp[i][j] && (res == null || j - i + 1 > res.length())) {
        res = s.substring(i, j + 1);
      }
    }
  }
    
  return res;
}
```

## 배운 점 
1. Expand Around Center 방식의 회문 검사를 배웠다.
2. `Palindrome length == end - start - 1 or start + 1 + end` 회문 길이 계산법
3. 시작점과 끝 점 계산 식
```
val len = len1.coerceAtLeast(len2)
if (len > end - start) {
    start = i - (len - 1) / 2
    end = i + len / 2
}
```
