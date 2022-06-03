---
title:  "[프로그래머스] 타겟 넘버"
excerpt: "사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요."

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2021-07-25
last_modified_at: 2021-07-25
---

# 타겟 넘버

문제 설명
n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

    -1+1+1+1+1 = 3
    +1-1+1+1+1 = 3
    +1+1-1+1+1 = 3
    +1+1+1-1+1 = 3
    +1+1+1+1-1 = 3

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

제한사항
주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
각 숫자는 1 이상 50 이하인 자연수입니다.
타겟 넘버는 1 이상 1000 이하인 자연수입니다.

    입출력 예
    numbers     	target	return
    [1, 1, 1, 1, 1]	3	    5
    

# 접근 방법
문제를 처음 봤을 때, 아 이건 DP를 써서 재귀를 돌려야겠다. 라고 생각이 들었다. numbers에서 숫자들을 알아서 받아오니까 해야하는건

1. numbers에 있는 수들을 각각 더하거나 빼주는 재귀를 짠다.
2. 그 횟수를 세서 numbers.length와 같아지면 return한다.
3. return시에 그 수들이 target과 같아지면 answer++한다.


        import java.util.*;
        
        class Solution {
            int answer = 0;
            public int solution(int[] numbers, int target) {
                int sum = 0;
                int count = 0;
                
                DP(numbers, sum, count, target);
                
                return answer;
            }
            
            public void DP(int[] number, int sum, int count, int target)
            {
                if(count == number.length)  //DP의 깊이가 배열 길이와 같다면
                {
                    if(sum == target)       //만약 더한 수들이 타겟과 같으면
                        answer++;           //answer++
                    return;                 //반환
                }
                int plusSum= sum + number[count];   //더하기
                int minusSum= sum - number[count];  //빼기
                count++;                            //횟수 증가
                DP(number, plusSum, count, target);
                DP(number,minusSum, count, target);
                return;
            }
        }

알고리즘 푸는데 원래 상당히 오래걸리지만 이 문제는 간단해서 금방 풀었던 것 같다.