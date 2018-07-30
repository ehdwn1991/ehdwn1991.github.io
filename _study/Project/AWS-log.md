---
layout: post
title: AWS project 진행 과정
comments: true
description: >
  [모든 내용은 Git Hub에도있습니다.]
study: [aws]
categories: [Python]
tags: [Tensor-flow, Deep-learning, OpenCV, Django]
date: 2018-07-28
author: author2
---



## gui 변경

> 사전에 맥에 vncviewer를 설치해 줬다.
>
> 아마 대부분 유저들이 사용하는 팀뷰어 같은 앱이라고 생각하면 편하다.

설치하면서 [stackoverflow](https://stackoverflow.com/questions/25657596/how-to-set-up-gui-on-amazon-ec2-ubuntu-server)를 참고 하였다.



```bash
# aws 우분투 서버 접속후
$ sudo apt-get update
$ sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
$ sudo apt-get install ubuntu-desktop
$ sudo apt-get install vnc4server


ubuntu@ip-172-31-19-48:~$ vncserver

You will require a password to access your desktops.

Password:
Password must be at least 6 characters - try again
Password:
Password must be at least 6 characters - try again
Password:
Verify:
xauth:  file /home/ubuntu/.Xauthority does not exist

New 'ip-172-31-19-48:1 (ubuntu)' desktop is ip-172-31-19-48:1

Creating default startup script /home/ubuntu/.vnc/xstartup
Starting applications specified in /home/ubuntu/.vnc/xstartup
Log file is /home/ubuntu/.vnc/ip-172-31-19-48:1.log

$ vncserver -kill :1
$ exit

# 우분투 서버 재접속
cd /vnc
sudo vi xstartup

#insert this script-------------------------------------#
export XKL_XMODMAP_DISABLE=1
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &

gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
#-------------------------------------------------------#
```



###  연결 주소 확인

![스크린샷 2018-07-27 오후 10.46.24](assets/스크린샷 2018-07-27 오후 10.46.24.png)


```bash
# 만약 aws에서 중지를 하거나 재부팅을 했을때 동적 ip를 사용 하기 때문에
# 매번 퍼블릭 DNS가 바뀌게 된다. 그래서 aws에서 연결 주소 확인!!

# 5901은 vnc로 접속할 포트 번호이다. 다른 포트번호를 써봤지만 안됨.
# 아직 이부분은 공부가 안되어 있어서 모르겠다.
$ sudo ssh -L 5901:localhost:5901 -i "codex_aws.pem" ubuntu@ec2-13-209-3-217.ap-northeast-2.compute.amazonaws.com

Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.4.0-1060-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

56 packages can be updated.
29 updates are security updates.


$ vncserver -geometry 1920x1080
New 'ip-172-31-19-48:1 (ubuntu)' desktop is ip-172-31-19-48:1

Starting applications specified in /home/ubuntu/.vnc/xstartup
Log file is /home/ubuntu/.vnc/ip-172-31-19-48:1.log


# vnc viewer 에서 다음 입력
localhost:5901

```

![스크린샷 2018-07-27 오후 10.44.04](assets/스크린샷 2018-07-27 오후 10.44.04.png)



## 우분투 서버에 파이썬 환경 설정

```bash
# 파이썬 확인
$ python --version
Python 2.7.12
$ python3 --version
Python 3.5.2

# 파이썬이 기본적으로 설치 되어 있음
# 이제 pip3 를 설치할 차례
$ sudo apt install python-pip
$ pip install --upgrade pip
$ sudo apt install python3-pip
pip 8.1.1 from /usr/lib/python3/dist-packages (python 3.5)
# 만약 다음과 같은 에러가 나온다면 이 명령 실행
# You are using pip version 8.1.1, however version 18.0 is available.
# You should consider upgrading via the 'pip install --upgrade pip' command.
$ sudo -H pip3 install --upgrade pip

# 갑자기 에러 나오기 시작함
# pip, pip3 버전체크 하는데 둘다 똑같이 밑의 에러를 토해냄
Traceback (most recent call last):
  File "/usr/bin/pip", line 9, in <module>
    from pip import main
ImportError: cannot import name main
# 
$ sudo python3 -m pip uninstall pip && sudo apt install python3-pip --reinstall

# 이제 ipython jupyter  설치
$ pip3 install ipython
$ pip3 install jupyter

```







### Jupyter notebook execution

![스크린샷 2018-07-27 오후 9.17.27](../../assets/img/post/스크린샷 2018-07-27 오후 9.17.27.png)



### 참고 

[텐서플로우 번역 깃북](https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/) 에 MNIST, Tensor-flow 에 대한 자세한 설명이 나온다  --- 감사합니다.

[Django 번역 깃북](https://tutorial.djangogirls.org/ko/)

