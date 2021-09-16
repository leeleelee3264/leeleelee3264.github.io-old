---
layout: post 
title: "[Linux] Linux command cheat sheet"
date: 2020-12-12 08:43:59
author: Jamie Lee
categories: Cheat
tags:	linux
cover:  "/assets/img/ubuntu.png"
pagination: 
  enabled: true
---

# Linux command 2021 

## grep with before/after num line 
```bash
# after
grep -A num "key_word" "file_name"

# before
grep -B num "key_word" "file_name"

ex)
grep -A 2 POST server.log
grep -B 2 POST server.log
``` 

grep을 쓰다 보면 딱 해당 사항의 문장들만 뽑아다 준다. 그래서 전후 상황을 알기가 어려운데 이때 -A와 -B 옵션으로 grep 조건에 맞는 문장 앞/뒤에 있는 문장들 n 행까지 출력을 할 수 있다. 



## jar 파일 내부 보기 
```bash
jar -tf "jar_name"
ex) jar -tf test.jar 
``` 

서버에 jar파일만 올리면 이 파일 안에 뭐가 들어있는지 알고 싶을 때가 있고 어떤 라이브러리의 어떤 버전을 쓰는지 알고 싶을 떄가 있다. 
이때 해당 커맨드를 사용해주면 된다. 사실 jar 파일은 java + tar 로, 리눅스에서 사용하는 파일 묶음인 tar를 자바 버전으로 만들었다고 생각하면 된다. 
단, tar 파일이 압축파일은 아니다. 그냥 여러 파일들을 한데 묶는 역할을 한다고 생각하면 된다. 



## 설치된/설치할 apk 버전 확인하기 
```bash
apt-cache policy "apk_name"
ex) apt-cache policy nginx 
```
이 커맨드를 쓰면 지금 서버에 설치된 apk의 버전도 볼 수 있고, 설치한다면 설치될 버전도 확인할 수 있다. 


## pgrep 
AKA process grep  


```bash
pgrep -a "query"
ex) pgrep -a java
```

with this, I don't have to do `ps -ef | grep java`. pgrep is ps with grep function.
<hr>
<br>

## type 
Getting more info with command. It will let you know about command such as alias, shell embeded 
```bash
type "query"
ex) type ls
```


## Related with network 
```bash
route
```

머신의 라우팅 테이블을 보여준다. 어떤 네트워크들이 열려있는지, 그 네트워크들의 브로드케스팅과 넷마스크, 인터페이스를 볼 수 있다. 
<br> 

```bash
ip a
```

제일 많이 사용하는 네트워크 정보 커맨드는 ifconfig인데 ifconfig는 net-tools를 설치해야 사용을 할 수 있다. 
ip a 를 사용하면 비슷한 정보들을 뽑아낼 수 있다. 오히려 ifconfig 보다 ip 커맨드가 더 기능이 많아보인다. 

## Related with vi 
```bash
go to end point of sentance : home key 
go to start point of sentance : end key

go to the top of file : gg
go to the bottom of file : ctrl + g
```


여태 vi 조작을 할 때 문장의 맨끝과 맨앞을 쉽게 가는 방법을 몰라서 방향키를 열심히 눌렀는데 
home 키를 누르면 문장의 바로 앞으로, end 키를 누르면 문장의 끝으로 손쉽게 갈 수 있다. 

## watch 
```bash
    watch ss -tlp

    # 한 번에 여러개 보기 
    watch "ss -tlp;df"
```

규칙적으로 값을 갱신해서 화면에 보여준다. default 값은 2초인 거 같다. 한마디로 이 커맨드를 쓰면 서버 상태를 계속 모니터링 할 수 있는 거다. 
아예 고정을 해놓고 실시간으로 업데이트를 해서 모여주니까 모니터링하기 편하다. 약간 top과 비슷하다고 할 수 있다. 

<br>

## tree 
```bash
    tree tc-admin 
    
    # 디렉터리들 지정해서 tree 만들기 
    tree tc-admin tc-admin-prod
```

이건 작업할 때 많이 쓴다기 보다는 블로그에 포스팅할 때 디렉터리 구조 보여주는데 더 많이 쓰는 것 같다. 
원래의 용도는 한 디렉터리의 구조를 deep down 하게 들어가 tree 를 만들어 보여주는 것이다. 디렉터리를 한 눈에 파악하기 좋다. 

<br>

## grep 
```bash
    
    # 키워드가 있는 문장을 제외하고 보여준다. 
    # -v 는 invert의 v 이다. 단어 그대로 결과 값을 뒤집는 것.
    grep -v "keyword" test.txt 
```
 


<br>

# Useful command from Linux Pocket Guide
```bash
# file line count 
wc -l file_name

# find difference between two files
diff file1 file2

# cat with number 
cat -n file_name 

# less with number 
less -N file_name 

# get dir info, not files info in the dir 
ls -d dir_name 

# try to read binary file with human eyes
strings file 
```

`less -N file_name` is fascinating command indeed. I usually use vi to see a whole file, if I try to 
access the file from different terminal I have to conflict .swp problem. I can solve it with less. Technically, Less does not make the file open. 
It just print all lines in the file using stream. Not like cat, less is a stream so I can go back and forth. 
number + g event let you go to the number directly. `100g` means go to 100 th lines in the file. 

<br>

# vim related command 
> setting number 
<br>

```bash
: set number

# remove number 
: set nonumber 

# set number to vim permanently 
vim ~/.vimrc 
# type set number in .vimrc file 
set number 
```

<br>

# shutdown linux 
```bash
    shutdown -h now 
```


<br>

## Run Java file in Linux 
I usually works with windows. But mostly, our server env is Linux. Because of this, I have to test in local(windows) and Linux both. 
Everything is quite same, however just like downloading/making file AKA involved with path makes things harder. 
Today(2021-01-08) I have to check project dir in both env, so I wrote a short java code to run in Linux as well. 

```java
    String currnetPath = System.getProperty("user.dir"); // it will return a currnet working dir
```


```bash
    # let's say I made CurrnetPath.java which contains class CurrentPath.
    
    # compile
    javac CurrnetPath.java

    # after compiling, I'm able to find CurrnetPath.class file. It's the result of compiling and I'll run it. Basically, I run class file to execute java code. 
    java CurrnetPath
```


<br>

## service related command 
```git
1. show installed service 
service --status-all 

2. show running service 
systemctl --type=service 
```


Linux commands related to service are mostly start as 'Systemctl'. 'Service' is kind of out-dated command, so it had better using 'systemctl'

## ubuntu 18 network connection 
```git
cd /etc/netplan
sudo vi 01-network-manager-all.yaml
~ change setting ~ 
sudo netplan apply
```

In Ubuntu 18 version, network connection setting is quite different with order versions. 
Now setting file is located in /etc/netplan. It means netplan is now the commander of netwokring. 
I had not known about applying command, so I just rebooted the os when I changed something. But you'd better just using 'netplan apply' command. 
<hr>
<br>

# Linux command 2020 

<br>

## sftp connection 
```git
    # 접속 
    sftp hostId@hostName
 
    # 파일 받아오기 
    get file
 
    #파일 올리기 
    put file
 
    #디렉터리 작업 (linux 에서 자주 보이는 옵션 -r은 recursion이다. 디렉터리 속으로 들어가서 재귀적으로 다 가져온다는 뜻인가봄
    get -r file 
    put -r file 
```

<br>
<br>

## ** Command from previous blog posting  
```bash
cd -**
```

내가 현재 디렉토리로 옮기기 직전에 있었던 디렉토리로 가는 커맨드.

작업을 하다보면 cd를 써서 디렉토리를 옮기는 일이 정말 많다. 그런데 방금 있었던 디렉토리로 돌아가야 할 때 cd 경로를 다시 치는 것 보다 cd - 를 사용하면 손 쉽게 갈 수 있다. 
<br>

![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMqY2w%2FbtqCD7WXspd%2FxPTxYUxaYfRvhGHrMJhAGK%2Fimg.png)

<br>

```bash
!!
```

바로 이전의 커맨드는 사실 ↑을 이용하는데 가끔 이전의 명령 불러오기가 안되는 경우가 있다고 한다. 그때 사용하면 좋은 커맨드. !를 잘 기억해두자. 과거의 커맨드를 불러들이는데 연관이 있는 커맨드다.
<hr>
<br>

```bash
!number 
ex) !120
```

history 커맨드를 사용하면 내가 여태까지 사용한 커맨드들의 기록을 보여준다. 그때 만약 다시 실행하고 싶은 커맨드가 있다면 !12 (실행하고 싶은 커맨드 번호)를 쓰면된다. 예를 들어 보겠다.
<br>

![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdkG65l%2FbtqCF6C80cC%2Fd8zRzdzeegML0HLpK9NbW1%2Fimg.png)


history에 나와있던 28번째 커맨드를 다시 실행하고 싶어서 !28을 쳤더니 28번째 커맨드가 실행되었다! 지금 내가 사용하는 커맨드는 짧은게 많지만 나중에 긴 커맨드를 실행하고 싶을 때 아주 유용하다.
<hr>
<br>


```bash
! previous command 
ex) !cd
```
아까 !12와 비슷하다. 단, 여기서는 history를 볼 필요가 없다. !cd (내가 제일 마지막으로 실행했던 cd) 라는 뜻이다. 결국 !뒤에 써진 커맨드는 내가 제일 최근에 실행했던 커맨드를 다시 실행해달라는 뜻이다.
<br>
![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FskTVE%2FbtqCGRltr9s%2FaMXtyt1LOlnr2aVRCDrfj0%2Fimg.png)
<hr>
<br>


```bash
ctrl + u
```

입력된 문자 모두 지우기.

윈도우를 사용하면 ctrl+a를 누르고 backspace를 누르는데 리눅스는 소용이 없다. 그럴 때 ctrl + u를 사용하면 여태 입력했던 문자가 싹 지워진다. 어떨 때 제일 좋냐하면 CUI 환경에서 비밀번호 치다가 오타 났을 때 ctrl+c 눌러서 명령 취소 안 하고 ctrl + u 눌러서 다시 입력할 때 좋다.
<hr>
<br>


```bash
top 
htop 
```

가끔 리눅스 안에서 실행되는 프로세스들을 확인하고 싶을 때가 생긴다. 예를 들어 실행한 jar 파일이 잘 돌고 있는지, 지금 막 db 배치를 돌렸는데 일을 잘 하고 있는지 등등. 프로세스 확인에는 ps -ef를 제일 많이 사용하겠지만 mysql, java 등등 돌아가는게 한 눈에 보기 좋은 커맨드는 top 이다.

top에서 shift+ p는 cpu 많이 잡아먹는 순으로 보여주고 shift + m 은 메모리 많이 잡아먹는 순으로 보여준다.
<hr>
<br>

```bash
netstat -ntlp
```

사실 이건 고수 커맨드는 아니고 내가 자꾸 깜빡깜빡해서 넣어놨다. 운영체제 안의 몇 번 포트들이 어느 프로세스와 연결되어 열려있는지를 볼 수 있다.
<br>

![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fo39R0%2FbtqCEOpqMVd%2FvkogOiVLhgqh056fkZH4F0%2Fimg.png)

<hr>
<br>

```bash
screen
```

 대부분의 터미널은 bash 프로세스와 연결이 되어있다. 그래서 터미널을 닫아버리면 내가 실행하고 있던 프로세스가 같이 끝나버린다. (bash가 끝났으니까 거기에 올려진 프로세스들도 다 끝나는 것) 그래서 jar 실행 등 리눅스 자체가 멈추지 않는 한 계속 실행되기 바라는 작업들은 리눅스가 죽기 전 까지 죽지 않는 root 프로세스에 연결한다. nohop 커맨드가  바로 그런 역할을 한다.

 그런데 이 방법 말고도 터미널이 죽어도 작업이 죽지 않는 방법이 있다. 바로 screen 커맨드다. 사실 screen 커맨드는 하나의 터미널에 여러 tab을 만들 때 사용하면 좋다. 여기저기서 작업을 할 수 있어서 편리하다. attached/detached 개념을 사용해서 터미널에 붙어있는지 아닌지를 알 수 있다.

 이렇게 스크린을 만들어 두면 작업 도중에 회사에서 집으로 옮겼을 경우 detached된 screen을 attached해서 사용하면 회사에서 하던 작업을 그대로 할 수 있다.

```bash
screen -ls: 현재 만들어져있는 screen의 list를 보여줌

screen -S name: name이란 이름의 screen을 만들어서 실행시켜줌

ctrl + a + d: 현재 작업하고 있던 screen에서 나오기 (screen이 detached 상태가 된다)

screen -r name: detached된 name에 다시 접속

ctrl + a + c: 해당 스크린 안에서 새로운 tab(bash)를 열어줌

ctrl + a + n: 다음 tab으로 넘어가기

ctrl + a + p: 이전 tab으로 넘어가기

screen -X -S name quit : name이라는 이름의 screen을 없애버림
```


이렇게만 알고 있어도 사용에 크게 지장이 없다.
<br>

![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfTDSr%2FbtqCEOXiQdn%2FkJgFokbYtVjOKHyx9H0UA1%2Fimg.png)


그리고 screen의 환경설정을 .screenrc에서 하는데 이때 화면을 보다 보기 쉽게 만들어 줄 수 있다. 나의 추천은 아래 링크로 세팅하는 것이다. 간결해서 보기 편하다. 적용하면 밑에 그림처럼 screen창이 만들어진다.

[https://gist.github.com/ChrisWills/1337178](https://gist.github.com/ChrisWills/1337178)
<br>

![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoyDdq%2FbtqCEOiKEZT%2FbcMTNqm9lmeF4zBTftz5kK%2Fimg.png)
<hr>
<br>

```bash
tail
```

tail (옵션들 알아보기 -n -f -F 등등) -f는 파일이 달라지는 걸 모른는데(포인터가 달라지는 둥) -F는 파일의 변화를 안다. 내용이 바뀐다는 것보다는 파일의 포인터가 달라진다는 얘기를 하는 것 같음.

<hr>
<br>

```bash
head
```

tail 과 비슷한 커맨드인데, tail이 파일의 끝을 조작한다면 head는 파일의 시작을 조작한다. 

<hr>
<br>

```bash
touch
```


그냥 시간 업데이트 한다고 생각했는데 컴파일러와 상관이 있다. 컴파일러는 안의 내용이 바뀌지 않아도 시간이 갱신되면 아 얘 새로운 변경사항이 있구나~ 하고 다시 컴파일을 해준다. 그래서 컴파일을 다시 하고 싶은데 번거롭게 뭘 따로 하고 싶지 않으면 touch를 써서 쉽게 시간을 바꿔주면 컴파일이 된다.
<br>
<br>
그리고 파일을 만들때도 vi로 열어서 저장을 하기 보다는 touch로 먼저 파일을 만들어두고 작업을 하는 경우가 많다.
<hr>
<br>


## Command with tmux 
```bash
tmux 
```

다른 분이 알려주신 커멘드인데 정말 너무너무 잘 쓰고 있다. 예전에 이거 없이 어떻게 살았나 싶을 정도.. screen 커맨드와 비슷한데 훨씬 더 좋다. session으로 이전 작업을 기억할 뿐 아니라 화면을 나눌 수 있다.
<br>

```bash
scroll 하기 : ctrl + b + pageUp [more tmux scroll command](https://superuser.com/questions/209437/how-do-i-scroll-in-tmux)

새로운 session 열기: tmux new -s session_name

session 끝내기: tmux kill-session -t session_name

session 목록 확인: tmux ls

session 종료하기: (tmux session에 들어가있는 상태에서) exit -> 양파처럼 윈도우가 하나씩 꺼진다. 마지막으로 exit을 하면 세션이 종료된다.

session deattach 하기: ctrl+b, d

session reattach 하기: tmux attach -t session\_name

session window 새로 만들기: ctrl+b, c

화면 나누기

가로로 나누기: ctrl+b, "

세로로 나누기: ctrl+b, %

나눠진 화면 모양 바꾸기: ctrl+b, space

나눠진 화면 비율 바꾸기: ctrl+b 누른 상태로 방향키로 조정

화면 사이 이동하기: ctrl+b, 방향키
```

<br>

![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbS8PXw%2FbtqEo6PRJEO%2FDhF5pnlCsYHfPH0CSSbrHK%2Fimg.png)


새로운 운도우 만드는 커맨드가 정말 너무 안 외워져서 쓸 때마다 검색하는데 지금보니 ctrl+b, c 였던 이유가 create의 c가 아니었을까 싶다.
<hr>
<br>

```bash
nginx -t
```

갑자기 리눅스 커맨드 얘기 하다가 nginx 얘기가 나왔는데 자주 깜빡해서 써두기로 했다. nignx의 conf 파일을 바꾸고 겁도 없이 바로 systemctl reload nginx 를 하고는 했는데 그 전에 conf 파일을 바꿨으면 검사를 먼저 해줘야 한다.

sudo nginx -t 를 하면 잘 썼을 경우 ok가 나오는데 그때 systemctl reload nginx로 반영을 하자.
<hr>
<br>


```bash
ss
```

ss에 대한 포스트를 읽다보니 ss가 new netstat 라는 말을 봤는데 그런것 같다. 열린 포트를 보려고 netstat을 해야하는데 정말 안 외워지는 커맨드 같다. ss가 조금더 사용이 쉽다고 한다.
<br>
![drag%20and%20drop%20(front)%203bbcb41524264640801dce23e80eb29e/dragdrop.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcBUuD6%2FbtqEq62ra5q%2F9mf7Xel1BWHUeEWJy5KAXk%2Fimg.png)
<br>

```bash
ss: 연결된 포트가 다 나온다

ss -t : 연결된 tcp 포트

ss -u : 연결된 udp 포트

ss -x : 연결된 유닉스 포트 (시스템적으로 연결된거라서 결과가 정말 많이 뜬다)

ss -tl : 연결된 tcp 포트 중에서 LISTEN 상태인것

ss -tlp : 연결된 tcp 중 LISTEN 상태를 돌리고 있는 프로세스까지 보여준다

ss state listening : 연결된 port중 LISTEN 상태인것 (ss -l 과 동일한테 줄바꿈이 안 일어난다)

ss -n : 연결된 포트를 보는데 n: numeric 옵션이라서 포트 번호를 정확하게 보여준다.

ss dst 특정 ip : 연결된 특정 ip에 대한 정보 (ip는 peer address의 ip이다.)
```

<hr>
<br>
