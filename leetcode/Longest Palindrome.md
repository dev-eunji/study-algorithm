# Longest Palindrome.

> [leetcode > 409 > Longest Palindrome.](https://leetcode.com/problems/longest-palindrome)
> 출처: leetcode, [https://leetcode.com]

- Level Easy [Greedy]

## 해결 과정

1. "a" "b" "cccc" "dd" 각 알파벳 별로 분리해서 생각한다.
2. length 가 짝수인 경우 Palindrome(회문)이 가능하다
3. length 가 홀수인 경우
 - 회문이 안 되지만, 문자열의 중앙에서 회문이 가능하다.
 - 가장 큰 홀수를 제외한 나머지는 -1 하여 짝수가 되면 회문이 가능하다.
4. 짝수 + 홀수 


## 코드 1

```kotlin
fun longestPalindrome(s: String): Int {
    val map = mutableMapOf<Int, Int>()
    s.forEach {
        val value = map[it.toInt()]
        map[it.toInt()] = if (value == null) 1 else value + 1
    }

    val sumEvens = map.filter { it.value % 2 == 0 }
        .values
        .sum()

    val odds = map.filter { it.value % 2 != 0 }.values
    val sumOdds = if (odds.sum() == 0) 0 else odds.sum() - odds.size + 1

    return sumEvens + sumOdds
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```c++
public int longestPalindrome(String s) {
    if(s==null || s.length()==0) return 0;
    HashSet<Character> hs = new HashSet<Character>();
    int count = 0;
    for(int i=0; i<s.length(); i++){
        if(hs.contains(s.charAt(i))){
            hs.remove(s.charAt(i));
            count++;
        }else{
            hs.add(s.charAt(i));
        }
    }
    if(!hs.isEmpty()) return count*2+1;
    return count*2;
}
```

## 배운 점
1. 조합 가능한 문자열 회문을 구할 때 짝수, 홀수 맵으로 key: 문자, value: 횟수 
2. length 가 홀수인 경우
 - 회문이 안 되지만, 문자열의 중앙에서 회문이 가능하다.
 - 가장 큰 홀수를 제외한 나머지는 -1 하여 짝수가 되면 회문이 가능하다.
3. sumEvens + sumOdds = 가장 긴 회문 길이가 된다.

- 최대 회문 공식은 아래와 같다.
1.  짝수: 최대 2*N
2.  홀수: 최대 2*N + 1
