---
title:  "[프로그래머스] 가장 큰 수"
excerpt: "0 또는 양의 정수를 이어붙여 가장 큰 수를 만들기"

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2021-07-21
last_modified_at: 2021-07-21
---

제한사항:
- 1<=numbers.length<=100,000
- 0<=numbers.[i]<=1,000
- 수가 너무 클 수 있으니 문자열로 바꾸어 return

예시)
[6,10,2] -> return: 6210
[3,30,34,5,9] -> return 9534330

풀이법:
자바 메소드 중 compareTo()를 사용하면 String클래스의 문자열간 큰기를 비교할 수 있다.
(b+a)compareTo(a+b)를 사용해 b+a가 a+b보다 크다면 b와 a의 자리를 바꿔줌

import java.util.*;

class Solution {
    
    public String solution(int[] numbers) {
        String answer = "";
        String result[] = new String[numbers.length];
        
        for(int i=0; i<numbers.length; i++)
        {
            result[i]=String.valueOf(numbers[i]); //int형인 numbers를 String형으로 변환
        }
        
        Arrays.sort(result, new Comparator<String>() {
           
            @Override //하위클래스의 메소드가 상위클래스를 덮음
            public int compare(String a, String b){
                return (b+a).compareTo(a+b);  //b+a가 a+b보다 크다면 b가 앞으로
            }
        });
        
        if(result[0].equals("0")) //모든 원소가 0으로 이루어져 있을 경우
            return "0";
        
        for(String a : result)
            answer += a;
        
        return answer;
    }
}