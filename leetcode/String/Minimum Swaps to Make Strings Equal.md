# Minimum Swaps to Make Strings Equal

> [leetcode > 1247 > Minimum Swaps to Make Strings Equal](https://leetcode.com/problems/minimum-swaps-to-make-strings-equal/)
> 출처: leetcode, [https://leetcode.com]

- Medium

## 해결 과정

1. x’와 ‘y’로 이루어진 두개의 문자를 스왑할 수 있을 때 가장 적게 스왑하여 두 문자를 같게 만들어야 한다.
2. 홀수 이면 글자를 맞출수 없기에 -1 리턴
3. "xy" or "yx" =>  일 경우 한번 더 swap 해줘야 된다. x1 % 2

## 코드 1

```kotlin
fun minimumSwap(s1: String, s2: String): Int {
    var xCount = 0
    var yCount = 0
    var result = 0

    for (i in s1.indices) {
        if (s1[i] != s2[i]) {
            if (s1[i] == 'x') {
                xCount++
            } else {
                yCount++
            }
        }
    }
    if ((xCount + yCount) % 2 == 1) {
        return -1
    }
    result = (xCount / 2) + (yCount / 2)
    if (xCount % 2 == 1) { // "xy" or "yx" case
        result += 2
    }
    return result
}

fun minimumSwap1(s1: String, s2: String): Int {
    var countXY = 0
    var countYX = 0
    var res = 0
    for (i in s1.indices) {
        if (s1[i] == 'x' && s2[i] == 'y') {
            countXY++
            if (countXY == 2) {
                res++
                countXY = 0
            }
        } else if (s2[i] == 'x' && s1[i] == 'y') {
            countYX++
            if (countYX == 2) {
                res++
                countYX = 0
            }
        }
    }
    return if (countXY + countYX == 1) -1 else res + countXY + countYX
}
```

## 코드 1 (two point)

```kotlin
public int minimumSwap(String s1, String s2) {
    int x1 = 0; // number of 'x' in s1 (skip equal chars at same index)
		int y1 = 0; // number of 'y' in s1 (skip equal chars at same index)
		int x2 = 0; // number of 'x' in s2 (skip equal chars at same index)
		int y2 = 0; // number of 'y' in s2 (skip equal chars at same index)

    for(int i = 0; i < s1.length(); i ++){
        char c1 = s1.charAt(i);
        char c2 = s2.charAt(i);
        if(c1 == c2){ // skip chars that are equal at the same index in s1 and s2
            continue;
        }
        if(c1 == 'x'){
            x1 ++;
        }else{
            y1 ++;
        }
        if(c2 == 'x'){
            x2 ++;
        }else{
            y2 ++;
        }
    } // end for

    // After skip "c1 == c2", check the number of  'x' and 'y' left in s1 and s2.
    if((x1 + x2) % 2 != 0 || (y1 + y2) % 2 != 0){
        return -1; // if number of 'x' or 'y' is odd, we can not make s1 equals to s2
    }

    int swaps = x1 / 2 + y1 / 2 + (x1 % 2) * 2;
    // Cases to do 1 swap:
    // "xx" => x1 / 2 => how many pairs of 'x' we have ?
    // "yy" => y1 / 2 => how many pairs of 'y' we have ?
    // 
    // Cases to do 2 swaps:
    // "xy" or "yx" =>  x1 % 2

    return swaps;        
} 
```

## 배운 점
1. 문자열 swap 형태를 배웠다.
2. `xy` or `yx` case 처리 해줘야 된다. (풀이 방법 참고 했다. 어렵다;)

