---
title:  "[Jekyll] 블로그 포스팅하는 방법"
excerpt: "md 파일에 마크다운 문법으로 작성하여 Github 원격 저장소에 업로드 해보자. 에디터는 Visual Studio code 사용! 로컬 서버에서 확인도 해보자. "

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2020-05-25
last_modified_at: 2020-05-25
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