---
title:  "[프로그래머스] H-index"
excerpt: "논문 n편중 h번이상 인용된 논문이 h편 이상이고 나머지가 h편 이하일 때, H-Index의 최댓값은 h다. "

categories:
  - Baekjoon

toc: true
toc_sticky: true
 
date: 2021-07-21
last_modified_at: 2021-07-21
---


제한사항:
- 1<=citation.length<=1,000
- 0<=citation[i]<10,000

예시:
[3,0,6,1,5] -> return:3

풀이법:
answer을 count로 생각한 뒤, count보다 작은 citation[i]들을 삭제하고 citations.length와 count가 같아지면 그 count가 최댓값 h가 된다.

```java
import java.util.*;

class Solution {
    
    public int solution(int[] citations) {
        int answer = 0;
        ArrayList<Integer> list = new ArrayList<>();
        
        for(int i=0;i<citations.length;i++)
            list.add(citations[i]);
        
        Collections.sort(list); //오름차수로 정렬
        
        while(answer<list.size()) //count가 list크기와 같아지면 끝
        {
            while(list.get(0)<=answer)  //list원소가 count보다 작으면 삭제
            {
                list.remove(0);
                if(list.isEmpty())  //[0,0,0......0]이 원소로 나오면 while문에서 전부 0을 삭제하여 결국 list가 비어있는 상태가 되어서 Null을 access하게됨.
                    break;
            }
            if(answer==list.size())
                break;
            answer++;
        }
        
        
        return answer;
    }
}
```