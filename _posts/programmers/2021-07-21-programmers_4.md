---
title:  "[프로그래머스] 조이스틱"
excerpt: "만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요."

categories:
  - Programmers

toc: true
toc_sticky: true
 
date: 2021-07-21
last_modified_at: 2021-07-21
---

ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA

조이스틱을 각 방향으로 움직이면 아래와 같습니다.

▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동
예를 들어 아래의 방법으로 "JAZ"를 만들 수 있습니다.

- 첫 번째 위치에서 조이스틱을 위로 9번 조작하여 J를 완성합니다.
- 조이스틱을 왼쪽으로 1번 조작하여 커서를 마지막 문자 위치로 이동시킵니다.
- 마지막 위치에서 조이스틱을 아래로 1번 조작하여 Z를 완성합니다.
따라서 11번 이동시켜 "JAZ"를 만들 수 있고, 이때가 최소 이동입니다.
만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.

제한사항:
 - 알파벳은 대문자로만 이루어져 있습니다.
 - 1<=name.length()<=20
 
풀이법: char형의 경우 문자와 문자의 뺄셈을 통해 얼마나 상하이동을 해야하는지 알 수 있고, 좌우이동의 경우는 그리디 알고리즘을 통해 인덱스에 따라서 좌우 이동거리를 측정하였다.


```java
import java.util.ArrayList;

class Solution {
    
    public int solution(String name) {
        int answer = 0;
        ArrayList<Character> list = new ArrayList<>();
        
        for(int i=0; i<name.length(); i++)
        {
            list.add(name.charAt(i));
        }
        
        int min=name.length()-1;
        
        for(int i=0; i<name.length(); i++)
        {
            if('Z'-list.get(i)+1 > list.get(i)-'A')
                answer += list.get(i)-'A';
            else
                answer += 'Z'-list.get(i)+1;
            
            int next=i+1;
            
            while(next<name.length() && list.get(next)=='A')
            {
                next++;
            }
            min = Math.min(min, i + name.length() - next + i);
        }
        answer+=min;
        
        
        return answer;
    }
}
```