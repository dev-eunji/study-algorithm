# Break a Palindrome

> [leetcode > 1328 > Break a Palindrome](https://leetcode.com/problems/break-a-palindrome)
> 출처: leetcode, [https://leetcode.com]
- Level Medium [Greedy], [String]

## 해결 과정

1. 회문(palindrome, 거꾸로 읽어도 동일한 문자열)이 주어졌을 때, 한 문자만 바꿔서 회문을 깨는 문제입니다. 
 - 단, 한 문자만 바꾸는 경우의 수는 엄청 많을 수 있으니 알파벳 순으로 가장 가까운 문자열로 바꿔줘야 합니다.
 - 한 문자를 바꿔서 회문을 깰 수 없다면 빈 문자열을 반환합니다.

2. 회문을 바꾸는 것이기에 문자열 길이 반만큼 반복
3. 알파벳 순으로 가장 가까운 문자로 바꿔야 되서 'a' 문자열로 치환
4. 모든 문자열이 'a'일 경우 마지막 index에 'b'로 치환


## 코드 1

```kotlin
fun breakPalindrome(palindrome: String): String {
    if (palindrome.length <= 1) {
        return ""
    }
    val palindromes = palindrome.toCharArray()
    for (index in 0 until palindromes.size / 2) {
        if (palindromes[index] != 'a') {
            palindromes[index] = 'a'
            return palindromes.joinToString("")
        }
    }
    palindromes[palindromes.size - 1] = 'b'
    return palindromes.joinToString("")
}
```

## 코드 2 (다른 사람 코드 Most Votes)

``` java
public String breakPalindrome(String palindrome) {
    char[] s = palindrome.toCharArray();
    int n = s.length;

    for (int i = 0; i < n / 2; i++) {
        if (s[i] != 'a') {
            s[i] = 'a';
            return String.valueOf(s);
        }
    }
    s[n - 1] = 'b'; //if all 'a'
    return n < 2 ? "" : String.valueOf(s);
}

```

## 배운 점
1. 회문 깨기 문제를 배웠다. (유명한 문제라고 함)
2. 회문 검사는 길의 / 2 만 하면된다.
3. Array -> String 변환
```
joinToString(""), String.valueOf()
```
 
