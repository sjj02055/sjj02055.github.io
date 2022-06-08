---
title:  "[프로그래머스] 체육복"
excerpt: "학생수가 n명이고 체육복을 잃어버린 사람의 배열이 lost이고 예비체육복을 가져온 사람의 배열이 reserve일 때, 체육복을 들을 수 있는 학생의 최댓값을 return"

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2021-07-21
last_modified_at: 2021-07-21
---

제한사항:
- 2<=n<=30
- 1<=lost[i]<=n
- 1<=reserve[i]<=n
- 여벌 체육복이 있는 학생만 다른 이에게 빌려줄 수 있습니다.
- 여벌 체육복 있는 사람이 하나만 도난당할 수 있습니다. 도난당했을 경우, 빌려줄 수 없습니다.

풀이법:
체육복이 몇개 있는지 미리 카운트하여 0,1,2의 값을 주고 시작한 다음 전체 학생 수를 for문으로
도는동안 체육복이 없을 경우 오른쪽 사람에게 먼저 빌려보고 오른쪽 사람도 없으면 왼쪽 사람에게
체육복을 빌려본다.


```java
import java.util.*;
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int num[] = new int[n];
        for(int i=0;i<n;i++)
        {
            num[i]=1;
        }
        for(int i=0; i<lost.length; i++)
        {
            num[lost[i]-1]--;
        }
        for(int i=0; i<reserve.length; i++)
        {
            num[reserve[i]-1]++;
        }                                   //체육복의 수 count,,, 0,1,2개씩
        
        for(int i=0; i<num.length; i++)
        {
            if(num[i]==0 && i+1<num.length) // i+1이 배열의 최댓값을 벗어나지 않게 제한
            {
                if(num[i+1] == 2)         //오른쪽 사람의 체육복의 개수가 2개있으면
                {
                    num[i+1]--;           //오른쪽 사람이 하나 주고
                    num[i]++;             //내가 하나 얻음
                }
            }
        }
        for(int i=0; i<num.length; i++)
        {
            if(num[i]==0 && i-1>=0)
            {
                if(num[i-1] == 2)
                {
                    num[i-1]--;
                    num[i]++;             //위와 마찬가지
                }
            }
        }
        
        int answer = 0;
        
        for(int i=0; i<num.length; i++)
        {
            if(num[i]>0)
            {
                answer++;
            }
        }
        
        return answer;
    }
}
```