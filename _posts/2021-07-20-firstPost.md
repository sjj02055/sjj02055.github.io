---
title:  "[프로그래머스] 모의고사"
excerpt: "1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요. "

categories:
  - Programmers
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2021-07-20
last_modified_at: 2021-07-20
---


# 모의고사

import java.util.*;

class Solution {

    public int[] solution(int[] answers) {
        int[] people1 = {1,2,3,4,5};
        int[] people2 = {2,1,2,3,2,4,2,5};
        int[] people3 = {3,3,1,1,2,2,4,4,5,5};
        int count=0;
        int check[]=new int[3];
        int temp=0;

        while(count<answers.length){
            if(answers[count]==people1[count%5])
                check[0]++;
            if(answers[count]==people2[count%8])
                check[1]++;
            if(answers[count]==people3[count%10])
                check[2]++;
            count++;
        }
        temp=check[0]>=check[1] ? check[0] : check[1];
        temp=temp>=check[2] ? temp : check[2];
        count=0;
        for(int i=0;i<check.length;i++){
            if(temp==check[i]){
                count++;
            }
        }
        int[] answer = new int[count];
        count=0;
        for(int i=0;i<check.length;i++){
            if(temp==check[i]){
                answer[count]=i+1;
                count++;
            }
        }
        return answer;
    }
}