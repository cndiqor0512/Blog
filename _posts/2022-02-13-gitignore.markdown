---
layout: post
title: "git ignore 사용법"
date: 2022-02-13 17:28:15
categories: programming
---

gitignore란?
git repository의 관리시, 관리에서 제외할 파일(또는 폴더)를 지정하는 파일이다.

Intellij에서만 필요한 파일이나, 실제로 git repository 관리에 있어서 필요하지 않은 파일들, 보안이 필요한 파일들, 용량이 너무 큰 파일들을 제외하는 데에 사용한다.

gitignore 사용법: 

1. .ignore 플러그인 설치
<img  src="https://cndiqor0512.github.io/img/ignore.PNG">
2. 최상위 폴더에 .gitignore 파일 만들기
<img  src="https://cndiqor0512.github.io/img/ignore2.png">
3. .gitignore 파일에 git repository 관리에서 제외할 파일들 선택하기

    .gitignore
    
    .idea  
    out  
    java_project.iml
