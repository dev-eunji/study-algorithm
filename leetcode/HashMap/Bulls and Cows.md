# Bulls and Cows

> [leetcode > 299 > Bulls and Cows](https://leetcode.com/problems/bulls-and-cows/)
- 출처: leetcode, [https://leetcode.com]

- Level Easy [HashMap]

## 해결 과정

1. 문자열 중 같은 position에 있으면 A, 아니면 자리는 같지 않더라도 같은 값이 다른 포지션에 있을 경우 B


## 코드 1 (Recursive, Iterative)

```kotlin (HashMap)
fun getHintHashMap(secret: String, guess: String): String {
    var bulls = 0
    var cows = 0
    val answer = HashMap<Char, Int>()

    //check bull
    secret.forEachIndexed { index, char ->
        val guessValue = guess[index]
        if (char == guessValue) {
            bulls++
        } else {
            answer[char] = answer.getOrDefault(char, 0) + 1
        }
    }

    //check cow
    secret.forEachIndexed { index, char ->
        val guessValue = guess[index]
        if (char != guessValue) {
            if (answer.containsKey(guessValue)) {
                cows++
                if (answer[guessValue] == 1) {
                    answer.remove(guessValue)
                } else {
                    var value = answer.getValue(guessValue)
                    value--
                    answer[guessValue] = value
                }
            }
        }
    }

    return "${bulls}A${cows}B"
}
```

```kotlin (2)
fun getHint(secret: String, guess: String): String {
    var bulls = 0
    var cows = 0
    val answer = IntArray(10)
    
    secret.forEachIndexed { index, char ->
        // val secretValue = Character.getNumericValue(char)
        // val guessValue = Character.getNumericValue(guess[index])
        val secretValue = char - '0'
        val guessValue = guess[index] - '0'

        if (secretValue == guessValue) {
            bulls++
        } else {

            if (answer[secretValue] < 0) cows++
            answer[secretValue]++

            if (answer[guessValue] > 0) cows++
            answer[guessValue]--
        }
    }

    return "${bulls}A${cows}B"
}
```

## 코드 2 (다른 사람 코드 Most Votes)

```Python
public String getHint(String secret, String guess) {
    int bulls = 0;
    int cows = 0;
    int[] numbers = new int[10];
    for (int i = 0; i<secret.length(); i++) {
        int s = Character.getNumericValue(secret.charAt(i));
        int g = Character.getNumericValue(guess.charAt(i));
        if (s == g) bulls++;
        else {
            if (numbers[s] < 0) cows++;
            if (numbers[g] > 0) cows++;
            numbers[s] ++;
            numbers[g] --;
        }
    }
    return bulls + "A" + cows + "B";
}
```

## 배운 점
1. `Character.getNumericValu` char to Int
2. 문제가 이해가 되지 않아 풀이를 보고 풀었는데 아직 다 이해하기 어렵다. numbers size는 왜 10일까?ㅜ
