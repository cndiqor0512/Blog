---
layout: post
title:  "git bash, git repository에 push하기"
date:   2020-01-04 10:15:35
categories: git
---


(깃 배쉬) 깃 repository에 push하기 

$ pwd 로 자신의 현재 디렉토리를 찾는다.

    $ pwd


자신의 현재 디렉토리를 찾고 $ ls를 이용해 현재 디렉토리에 있는 파일 및 폴더를 찾아낸다.
 

    $ ls
    
$ cd를 이용해 자신이 push할 파일(폴더)를 찾는다.

    $ cd (폴더이름) (물론 괄호 빼고)

 자신의 현재 디렉토리가 맞는 파일(폴더)이라면 $git status를 사용해 그 파일에서 무엇이 바뀌었는지(코드) 확인한다. 후에 $ git add . 를 사용한다.
 

    $ git status
    $ git add . 
후에는 commit을 지정한다.

    $ git commit -m"(commit 적기)"

위와같이 commit이 지정 가능하다.
만일 후에 이런 에러가 뜬다면

    *** Please tell me who you are.
    Run
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    
    to set your account's default identity.
    Omit --global to set the identity only in this repository.

위에서 나왔듯이 git config --global user.email "자기 이메일(깃허브 내)"
							 git config --global user.name "자기이름(깃허브 내)"
							 을 각각 쳐주면 된다.

후에 $ git push origin master 입력하면 push가 끝이 난다.

    $ git push origin master