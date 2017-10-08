---
layout: post
title:  "No directory, logging in with HOME=/ 오류에 관하여"
date:   2017-10-09 02:19:55 +0900
categories: python
---


`MySQL5.7` No directory, logging in with HOME=/ 오류에 관하여
==========================

 > [파이썬을 이용한 머신러닝, 딥러닝 실전 개발 입문](http://wikibook.co.kr/python-machine-learning/)      

- ch3 `ubuntu-mysql` 에 관하여

    

   책에서는 `Docker` 로 `Ubuntu:16.04`  Pull 해서, apt-get install로 `MySQL`  설치해
  실습하라고 되어 있다. 예제에서는  docker로 pull 받은 ubuntu는 root로 접속해서 실습하는데, 예제와 똑같이 하면 MySQL5.7에서  `No directory, logging in with HOME=/` 에러가 발생한다. user가 없으니 /home/에 user directory가 없어서 그런거 같은데, 이걸 해결하려면 여러가지 해야할 것들이 추가된다.

  하지만, 간단한 실습 하나 하고자 그러기에는 너무 귀찮다. 그래서 해당 docker image를 commit 안하고 날려버린 뒤에

  그냥 예제 내용에서 mysql를 mariaDB로 바꿨을 뿐인데

  # 너무 잘된다.  