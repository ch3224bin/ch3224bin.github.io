---
layout: post
title: "프로그래머스 알고리즘 문제 - 위장(level 2)"
categories: [취미,알고리즘]
comments: true
---
# 왜 이글을 쓰는지?
이직 준비로 예전에 알고리즘 문제를 조금 풀었었는데, 골치아팠던게 순열, 조합 관련된 문제였다.

그래서 인지 아무데나 조합, 순열을 들이대다가 주화입마에 빠졌다.  

이 문제를 보았을때, 조합 문제인 줄 알고.. 머리를 싸메고 몇시간을 허비하여 깊은 빡침에 이 글을 쓴다.

# 문제
아래 링크에서 확인 가능  
https://programmers.co.kr/learn/courses/30/lessons/42578

# 풀이
언듯 문제를 보면 조합을 쓰고 싶어지고 함정에 빠지게 된다.(내가)  
단순히 생각하면 쉽다. (정답지를 보면 쉽다는 뜻.)  

모자에 캡, 중절모가 있다면, 모자에서는 3가지 확률이 나온다.  
캡을 쓸 경우, 중절모를 쓸 경우, 아무것도 안 쓸 경우.  
부위별 옷가지 갯수에 안입는 경우 하나를 더해주는게 포인트다.

그럼 각 부위별 갯수를 모두 곱해주면 되고, 몸전체에 아무것도 안 입는 경우는 1이니 1만 빼주면 된다.  
각 부위별로 곱하는 이유는 확률에서 곱의 법칙이 적용되기 때문인데,  
주사위 두개를 동시에 굴렸을때 나오는 숫자의 조합을 생각하면 이해하기 쉽다. 6x6

```java
class Solution {
    public int solution(String[][] clothes) {
        java.util.Map<String, Integer> m = new java.util.HashMap<>();
        for (String[] c : clothes) {
            m.put(c[1], m.getOrDefault(c[1], 0) + 1);
        }
        int answer = 1;
        for (Integer v : m.values()) {
            answer *= v + 1;
        }
        return answer - 1;
    }
}
```
