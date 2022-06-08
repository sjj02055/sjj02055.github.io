---
title:  "[프로그래머스] 단속카메라"
excerpt: "고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.."

categories:
  - Baekjoon

toc: true
toc_sticky: true
 
date: 2021-07-23
last_modified_at: 2021-07-23
---

# 단속카메라

문제 설명
고속도로를 이동하는 모든 차량이 고속도로를 이용하면서 단속용 카메라를 한 번은 만나도록 카메라를 설치하려고 합니다.

고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.

제한사항

차량의 대수는 1대 이상 10,000대 이하입니다.
routes에는 차량의 이동 경로가 포함되어 있으며 routes[i][0]에는 i번째 차량이 고속도로에 진입한 지점, routes[i][1]에는 i번째 차량이 고속도로에서 나간 지점이 적혀 있습니다.
차량의 진입/진출 지점에 카메라가 설치되어 있어도 카메라를 만난것으로 간주합니다.
차량의 진입 지점, 진출 지점은 -30,000 이상 30,000 이하입니다.

    입출력 예
    routes	                                    return
    [[-20,15], [-14,-5], [-18,-13], [-5,-3]]	2

입출력 예 설명

-5 지점에 카메라를 설치하면 두 번째, 네 번째 차량이 카메라를 만납니다.

-15 지점에 카메라를 설치하면 첫 번째, 세 번째 차량이 카메라를 만납니다.

# 접근방법

이 문제를 처음 봤을 때 느낀건 아 고속도로를 빠져나가는 위치나 고속도로 들어가는 위치에 조작을 하면 문제 쉽게 풀 수 있겠구나 라는 생각이 들었다.

실제로 문제를 풀어보고 나니까 간단한 조작만 하면 쉽게 풀 수 있는 문제였다. 다른 분이 먼저 풀었던 블로그에서 그림을 간단히 참조하자면

다음과 같은 상황일 때,

    routes                              return
    [[-10,0], [-3,5], [-5,7], [9,11]]   2

![image](https://user-images.githubusercontent.com/64392631/126741540-265bbf0e-fd74-40e5-a15a-e38825fa139d.png)

자동차가 고속도로를 빠져나간 지점기준으로 오름차순으로 정리한 다음에 자동차가 빠져나간 지점보다 다른 자동차가 들어온 시점이 앞에 있는 지점이면 넘어간다.

하지만 그렇지 않을 경우 기준을 새로 들어온 자동차의 고속도로 나간 지점으로 재지정을 한 후 다시 찾는 것을 반복해나가는 과정을 진행하면 된다.
```java
    import java.util.*;
    class Solution {
        public int solution(int[][] routes) {
            int answer = 1;
            ArrayList<Node> list = new ArrayList<>();
            
            for(int i=0; i<routes.length; i++)
            {
                list.add(new Node(routes[i][0],routes[i][1]));
            }
            
            Collections.sort(list); // 오름차순으로 정렬
            int min=list.get(0).end; // 기준은 맨 처음 자동차의 빠져나간 지점
            
            for(Node a : list){
                if(a.start>min){ //만약 새로들어온 자동차가 기준보다 더 늦은 지점에 있다면
                    min=a.end; //기준을 새로들어온 자동차의 빠져나간 지점으로 재설정
                    answer++; // 단속카메라 설치
                }
            }
            
            return answer;
        }
        
        
        
        class Node implements Comparable<Node>{
            int start;
            int end;
            
            Node(int start, int end){
                this.start = start;
                this.end = end;
            }
            @Override
            public int compareTo(Node o){
                return this.end-o.end;
            }
        } // 오름차순 정리
    }
```