---
layout: post
title:  "mysql workbench 사용법"
date:  2022-01-09 22:00:33
categories: springboot
description: "mysql workbench 사용법"
---


## **mysql workbench**
mysql workbench를 처음 실행하면 다음과 같은 화면이 나타날 것이다.
<img src="https://cndiqor0512.github.io/img/mysql_workbench1.PNG">
mysql connections로 들어간 후, 하단의 Schemas를 누른다.
<img src="https://cndiqor0512.github.io/img/mysql_workbench2.PNG">
Schemas를 누른 뒤 빈 공간에 우클릭을 하면 새로운 Schema를 만들 수 있다.
새로운 Schema를 만들고 Tables에서 Table을 생성할 수 있다.  만든 Table에 커서를 갖다 대면, 몽키스패너 모양의 아이콘을 찾을 수 있다. 
<img src="https://cndiqor0512.github.io/img/mysql_workbench4.png">
그것을 누르면-
<img src="https://cndiqor0512.github.io/img/mysql_workbench4.5.png">
다음과 같은 화면으로 넘어가진다.
화면에서 Table이름을 정하고, Column을 추가해준다(첫 번째 Column은 id로 해야하고, 다음과 같은 속성을 가지고 있어야한다.).
그 후 만든 Table을 우클릭하여 선택해주면..
<img src="https://cndiqor0512.github.io/img/mysql_workbench5.png">

    SELECT * FROM test.user; 

라는 문구가 적혀있을 것이다. 이는 test.user 테이블의 모든 Column(*)을 선택한다는 뜻이다.

이러한 테이블에 값을 추가하기 위해서는 INSERT문을 사용한다.

    INSERT INTO table_name (column1, column2, column3, ... )	
    VALUES (content1, content2, content3, ... );

이것이 기본 구조이며, 이것을 실제에 대입하면, 
<img src="https://cndiqor0512.github.io/img/mysql_workbench6.PNG">
다음과 같이 된다.
<img src="https://cndiqor0512.github.io/img/mysql_workbench7.PNG">

<img src="https://cndiqor0512.github.io/img/mysql_workbench8.PNG">
이런 방법으로 총 11명의 정보를 입력했다.
하지만 이번엔 다른 방법으로 SELECT를 해볼 것이다.
<img src="https://cndiqor0512.github.io/img/mysql_workbench8.5.PNG">
이것은 16살인 사람의 이름과 생일만을 선택한다는 뜻이다. where을 통하여 조건을 추가할 수 있다.

이와 같은 방법으로 where을 사용하여 정보를 업데이트하고 삭제할 수도 있다.

    UPDATE user SET name = "Jinho" where id = 1;
이러한 코드는 id가 1인 column의 이름을 Jinho로 바꿀 것이고,

    DELETE FROM user where id = 1;


이러한 코드는 id가 1인 column을 삭제할 것이다.
