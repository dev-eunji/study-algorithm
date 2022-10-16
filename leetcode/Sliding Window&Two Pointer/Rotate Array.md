#  Rotate Array

> [leetcode > 189 > Rotate Array](https://leetcode.com/problems/rotate-array)
> 출처: leetcode, [https://leetcode.com]

- Level Medium [Two Pointer]

## 해결 과정

1. 주어진 배열에서 입력받은 만큼 로테이션 시키는 문제
2. 전체 배열을 한번 다 뒤집는다.
> a= [1,2,3,4,5,6,7] k = 3.
 >> you will get[7,6,5,4,3,2,1]

3. 0 ~ rotate - 1 까지의 값을 다시 뒤집는다.
> reverse the elements from 0 to rotate - 1
 >> reverse the elements 7,6,5
 >> you will get [5,6,7,4,3,2,1]

4. 남은 rotate ~ 마지막 까지의 값을 다시 뒤집는다.
> reverse the elements from rotate to n - 1
 >> reverse the elements 4,3,2,1
 >> you will get[5,6,7,1,2,3,4]

- 첫번째 towPoint 를 사용하는 것이 더 효율성이 높다.


## 코드 1

```kotlin
fun rotate(nums: IntArray, k: Int): Unit {
    var rotate = k % nums.size

    reverse(nums, 0, nums.size - 1)
    reverse(nums, 0, rotate - 1)
    reverse(nums, rotate, nums.size - 1)
}

private fun reverse(nums: IntArray, to: Int, form: Int) {
    var start = to
    var end = form

    while (start < end) {
        val temp = nums[start]
        nums[start] = nums[end]
        nums[end] = temp
        start++
        end--
    }
}
```

## 코드 2

```kotlin
fun rotate1(nums: IntArray, k: Int): Unit {
    if (nums.isEmpty()) {
        return
    }
    var rotate = k % nums.size
    val copy = nums.copyOf()
    for (i in nums.indices) {
        nums[(rotate + i) % nums.size] = copy[i]
    }
}
```

## 코드 3 (다른 사람 코드 Most Votes)

``` Java
public class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length; 
        //(1) new array; 
        int[] oldNums = nums.clone();
        for(int i = 0; i< nums.length;i++){
            nums[(i+k)%nums.length] = oldNums[i]; 
        }
        
        //(2) reverse 3 times 
        // reverse(nums, 0, nums.length-1); 
        // reverse(nums, 0, k-1);
        // reverse(nums, k, nums.length-1); 
        
        //(3) move k times
        // while(k-->0){
        //     int tmp = nums[nums.length-1];
        //     for(int i = nums.length-1; i>0; i--){
        //         nums[i] = nums[i-1];
        //     }
        //     nums[0] = tmp; 
        // }
    }
    
    public void reverse(int[] nums, int start, int end){
        while(start < end){
            int temp = nums[start]; 
            nums[start] = nums[end]; 
            nums[end]=temp; 
            start++; end--; 
        }
    }
}
```

## 배운 점
1. 투포인터 개념 보다는 수학적 공식이 더 중요한 것 같은 느낌
2. 투포인터로 `reverse`를 배웠다.


