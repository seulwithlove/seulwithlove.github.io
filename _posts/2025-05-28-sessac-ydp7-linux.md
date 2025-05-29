---
layout: post
title: SeSAC - 리눅스 기초
date: 2025-05-28
description: SeSAC 영등포캠퍼스 풀스택 과정 공부 기록
tags: sesac linux shell vim trouble-shooting
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

# 📚 Day 1 - linux

---

# 🎯 예습

## 도커 컨테이너 Container
> 격리된 작은 가상 리눅스 시스템

- 컨테이너 안에는 운영체제 일부 + 실행 프로그램이 있음
- 컨테이너가 실행되었다고 데몬이 자동으로 켜지는건 아님
	- 컨테이너는 데몬을 실행할 수 있는 공간
	- 실제로 데몬이 실행되려면 명령어로 시작해야함

### 이미지 저장 & 실행
- 지금까지 실행한 도커에 vim도 설치하고... 작업한것들 이미지로 저장해두고 다음에 동일하게 실행!

```shell
docker ps
CONTAINER ID   IMAGE           COMMAND       CREATED        STATUS       PORTS     NAMES
414c3a0518db   centos:8        "/bin/bash"   22 hours ago   Up 6 hours             centlinux
95b8cf2166b7   ubuntu:latest   "/bin/bash"   22 hours ago   Up 6 hours             ubunlinux

docker commit ubsh ubsh_vim
Error response from daemon: No such container: ubsh # docker의 Names를 넣어야함

docker commit ubunlinux ubunlinux_vim
sha256:31ad3633369b0539df4bc3e2231e4381c69d68ab7dbd2c790b62fbea9212d210

docker images  # 갖고 있는 도커 이미지들이 나옴 : 이미지 목록 보기

docker run -it --name [NAMES] [IMAGE]  # 이미지로 컨테이너 실행

docker run -d [IMAGE]  # 백그라운드 실행
```

| 옵션       | 설명                                   |
| -------- | ------------------------------------ |
| `-it`    | 인터랙티브 모드 + 터미널                       |
| `--name` | 컨테이너에 원하는 이름 지정                      |
| `NAMES`  | 실행할 이미지 이름 (`docker images`에서 확인한 것) |
| `d`      | 백그라운드에서 실행 (detached mode)           |

### 실행중인 컨테이너 안으로 쉘 접속

```shell
docker exec -it [컨테이너명] bash  #컨테이너 안으로 들어감 (쉘 접속)
```
- `-i`: 인터랙티브 모드 (입력 가능)
- `-t`: 가상 터미널 (출력 보기 좋게)

### 실행중인 도커 종료
```shell
docker ps -q  # 실행중인 도커 목록
docker stop `docker ps -q`   # 실행중인 도커 종료
docker ps  # 도커 확인
```

### 도커 명령어들
```shell 
docker ps -a --format '{{.Names}}'  # 도커 이름만 출력
docker ps -a --format '{{.Names}} || {{.Status}}'  # names & status 
```

## vim
### 📍 edit command

u: Undo(Ctrl+z)
x: delete
X: backpace
r: change 1 char
A: insert mode at line end
o: 다음줄에 입력모드 시작
O: 윗줄에 입력모드
dd: 한줄 지우기
dw: 한단어 삭제
cw: 한단어 수정
**yy: 한줄 복사**
**p: 붙여넣기**
v: 블럭지정
D: 현재 커서위치 뒷부분 삭제

Shift+$: 제일 뒤로

**0: 줄의 맨 앞**
**^: 줄의 첫 글자**
**$: 줄의 맨 끝**
**gg: 제일 앞 문단으로**
**shift+g: 마지막 문단으로**
^: Home key(Shift+6)

### 📍 colon command
:w  " save
:q  " exit
:q!  " exit without saving
:!  "커맨드 라인으로 잠깐 나갔다 들어오기(엔터 누르면 다시 들어옴)
:!명령어   "커맨드라인에서 명령어 실행하고 들어오기()
:paste
:%s/찾으려는문구/바꾸려는문구/ig 
/[찾을단어] : 커서 아래방향에서 단어를 찾음
?[찾을단어] : 커서 위 방향에서 단어를 찾음

#### vim excersice
- `vimtutor` 명령어: 터미널에서 `vim` 기본기 연습 가능
- 실습사이트: [https://vim-adventures.com/](https://vim-adventures.com/)



## shell script 
- `${var}` : 변수 var 의 값 참조 
	- 변수는 원래 $var 로도 사용할수 있지만 띄어쓰기가 있거나 분명하게 하기위해 {}로 싸는것!
- `$((expression))` : 산술계산 - 정수만 가능
- `$(command)` : command의 실행 결과를 문자열로 치환
- `$(< filename)` : 파일내용을 빠르게 읽어옴

### shell command

| 번호  | 이름         | 설명                 |
| --- | ---------- | ------------------ |
| `0` | **stdin**  | 표준 입력 (keyboard 등) |
| `1` | **stdout** | 표준 출력 (정상 출력)      |
| `2` | **stderr** | 표준 에러 출력 (에러 메시지)  |

### parameters
```vim
#!/bin/bash

echo "\$0=$0"  # self
echo "\$1=$1"  # 1st parameter
echo "\$2=$2"  # 2nd parameter
echo "\$#=$#"  # number of parameters
```

```bash
dooo@9b8ddbc79446:~/workspace$ ./s3.sh aaa bbb ccc
$0=./s3.sh
$1=aaa
$2=bbb
$3=ccc
$#=3

dooo@9b8ddbc79446:~/workspace$ ./s3.sh aaa bbb
$0=./s3.sh
$1=aaa
$2=bbb
$3=
$#=2
```

### Date
```bash
DATE=`date +%Y-%m-%d --date='1 day ago'`
DATE=`date +%Y-%m-%d --date='2 month'`

echo $DATE
2025-05-27
```

### 숫자 계산
```vim
#!/bin/bash

for i in {2..9}
do
	for j in {1..9}
	do
		echo "$i * $j = $(( $i * $j ))"  # $(( )) : 숫자 연산 가능  / expr 같은 기능
	done
	echo "---------------"
done
```

## cron
- 2 : standard error
- &1: standard out

## PuTTY
- Windows전용 ssh 클라이언트
- 윈도우에서는 기본적으로 터미널(ssh 접속기능)이 없음
- 리눅스 서버에 접속할수 있게 도와주는 외부 프로그램
	- 리눅스 서버에 SSH 접속
	- 터미널 에뮬레이터 기능

## Telnet
> 원격 접속 프로토콜 중 하나<br>
>- 로컬이 아닌 다른 컴퓨터(서버)에 **원격으로 로그인**해서 터미널 명령을 사용할 수 있게 해주는 방식

- 사용자가 텔넷 클라이언트를 실행해서 상대방 컴퓨터의 **텔넷 데몬(telnetd)에 접속**
  
### 텔넷 데몬 telnetd 
> 텔넷 접속을 기다리고 들어오는 연결을 처리하는 서버 프로그램
- 클라이언트 접속요청을 기다림
- 접속이 들어오면 사용자 인증 수행(ID/PW)
- 접속 허가 되면 쉘 환경을 열어줌
```css
[당신의 PC] -- Telnet --> [서버에 있는 telnetd (텔넷 데몬)]
                               ↓
                     로그인 후 쉘 제공
```


## port forwarding
- 외부에서 특정 포트로 요청이 오면 **내부 시스템의 다른 포트나 다른 컴퓨터(컨테이너 등)로 연결** 해주는 설정

## 데몬 Daemon
> 백그라운드에서 실행되는 요청을 기다리는 서버 프로그램

- 사용자가 요청을 보내면 반응
- *듣고있다가 반응하는 프로그램*
	- ssh server: `sshd`
	- Telnet server: `telnetd`
	- web server: `httpd`(Apache)


## `sudo` vs `su` vs `su -`
> sudo :  관리자권한으로 일시적으로 명령어 하나 실행<br>
>  su   :  해당 사용자로 전환(보통 root) - 셸만 전환 - 환경변수는 그대로 <br>
>  su - : 로그인 셸로 전환 - 완전히 해당 사용자용으로 전환 - 환경변수, 경로, 홈디렉토리 등 포함<br>

- sudo 명령어는 기록에 남고, 특정 사용자만 사용하도록 제한 가능(`/etc/sudoers`)
- `-`하이픈 : login shell로 전환한다는 의미
	- `su - user` 해당 사용자가 처음 로그인할 때 처럼 완저한 환경을 불러오는 것

```bash
su user
# => 여전히 이전 사용자의 환경이 일부 남아 있음
# 현재 디렉토리는 전 사용자 그대로, echo $HOME 하면 여전히 이전 유저 홈이 나올수 있음

su - user
# => 그 유저의 환경 설정파일 (~/.bash_profile, ~/.bashrc 등)을 새로 불러옴
# 현재 디렉토리: /home/user, echo $HOME : /home/user 로 바뀜
```

## vi & vim
> vi : 전통적인 텍스트 편집기 (1970년대 UNIX에서 시작)<br>
> vim : *"Vi iMproved"* , `vi`의 기능을 확장하고 향상시킨 버전

| 기능                          | `vi`                 | `vim`                       |
| --------------------------- | -------------------- | --------------------------- |
| 기본 제공 여부                    | 대부분의 UNIX 시스템에 기본 포함 | 리눅스 배포판마다 설치 필요할 수 있음       |
| 문법 강조 (Syntax Highlighting) | ❌ 없음                 | ✅ 있음                        |
| 멀티 Undo/Redo                | ❌ 단일 undo만 가능        | ✅ 무제한 undo/redo             |
| 파일 탐색                       | ❌ 없음                 | ✅ 기본 파일 탐색 기능 (NERDTree 등)  |
| 플러그인 시스템                    | ❌ 없음                 | ✅ 매우 풍부함 (자동 완성, lint 등 가능) |
| GUI 버전 (gvim)               | ❌ 없음                 | ✅ 있음                        |
| 도움말 (`:help`)               | 매우 간단함               | 매우 풍부함, 설명도 친절              |

## `apt` / `apt-get`
> apt-get : **기존부터 존재하는** 강력한 패키지 관리 도구 (스크립트용)<br>
> apt : `apt-get`, `apt-cache` 등을 **통합하고 개선**한 명령어 (사용자용)

|항목|`apt-get`|`apt`|
|---|---|---|
|등장 시기|오래전부터 있음 (`Debian 1.1`부터)|Ubuntu 16.04 이후 새로 등장|
|사용 대상|**스크립트, 자동화**에 적합|**사람(사용자)**에게 친절한 인터페이스|
|출력 형식|기본적인 텍스트 출력|진행률 바(progress bar), 색상 출력 등|
|기능 통합|명령어가 분리되어 있음|`apt-get`, `apt-cache`, 일부 기능 통합|
|사용 예시|`apt-get install`|`apt install`|

---

## 🛠️ Trouble shooting
### 🚧 첫번째 에러 - docker
```bash
Cannot connect to the Docker daemon at unix:///Users/seul/.docker/run/docker.sock. Is the docker daemon running?
```
- **상황**: docker-compose.yml 파일을 실행하려고하는데 에러발생
	- `docker-compose up -d` 명령어를 실행하면 \_docker-compose 로 자동 바뀜 : docker만 치고 탭 하면 docker 기본 문법이 실행됨
- **파악**: docker-compose 가 설치되어있지 않았음 
- **해결**: `brew install --cask docker`로 다시 docker 설치 -> 업데이트
	- 도커데스크탑 실행
	- 도커데스크탑 알림탭에 docker-compose가 삭제되었다는 알림과 해결 버튼 활성화 -> 설정값 변경
	- shell에서 docker-compose 명령어 인식완료

### 🚧 2 : `docker-compose up -d`
```shell
Error response from daemon: Mounts denied:
The path /Users/.../data2 is not shared from the host and is not known to Docker.
You can configure shared paths from Docker -> Preferences... -> Resources -> File Sharing.
```
- **해결** :  도커가 실행되는 path에 실행경로 추가
	- [참고](https://stackoverflow.com/questions/45122459/mounts-denied-the-paths-are-not-shared-from-os-x-and-are-not-known-to-docke)

### 🚧 3: 리눅스에서 ps -ef 명령어 못찾음
- `ps: command not found`
- **해결** : procps 설치
	- centos 계열 : `yum install -y procps`
	- debian/ubuntu : `apt update && apt install -y procps`
		- rocky linux는 centos 계열 
- [ref](https://github.com/tianon/docker-brew-debian/issues/13)


### 🚧 4: `E: Unable to locate package sudo`
```shell
apt update   # 혹은 
apt-get update
```

### 🚧 5: `E: Unable to locate package vi`
- vi 대신에 vim으로 설치
```shell
apt update
apt install apt-file
apt-file update
apt install vim # vi 는 계속 동일한 에러가 나서 vi로 했더니 완료
```
- [참고](https://littlecandle.co.kr/bbs/board.php?bo_table=codingnote&wr_id=297)

### 🚧 6: `touch: cannot touch 'qt/df.txt': Permission denied`

```shell
leecokie@95b8cf2166b7:~$ ll
total 40
drwxr-x--- 3 leecokie leecokie 4096 May 26 12:22 ./
drwxr-xr-x 1 root     root     4096 May 26 12:14 ../
-rw------- 1 leecokie leecokie  530 May 26 11:45 .bash_history
-rw-r--r-- 1 leecokie leecokie  220 May 25 18:57 .bash_logout
-rw-r--r-- 1 leecokie leecokie 3771 May 25 18:57 .bashrc
-rw-r--r-- 1 leecokie leecokie  807 May 25 18:57 .profile
-rw------- 1 leecokie leecokie 7205 May 26 10:08 .viminfo
-rw-rw-r-- 1 leecokie leecokie  113 May 26 10:08 .vimrc
drwxr-xr-x 2 root     root     4096 May 26 12:08 ttt/

leecokie@95b8cf2166b7:~$ ln -s /home/queen/test qt
leecokie@95b8cf2166b7:~$ ll
total 40
drwxr-x--- 3 leecokie leecokie 4096 May 26 14:36 ./
drwxr-xr-x 1 root     root     4096 May 26 12:14 ../
-rw------- 1 leecokie leecokie  530 May 26 11:45 .bash_history
-rw-r--r-- 1 leecokie leecokie  220 May 25 18:57 .bash_logout
-rw-r--r-- 1 leecokie leecokie 3771 May 25 18:57 .bashrc
-rw-r--r-- 1 leecokie leecokie  807 May 25 18:57 .profile
-rw------- 1 leecokie leecokie 7205 May 26 10:08 .viminfo
-rw-rw-r-- 1 leecokie leecokie  113 May 26 10:08 .vimrc
lrwxrwxrwx 1 leecokie leecokie   16 May 26 14:36 qt -> /home/queen/test
drwxr-xr-x 2 root     root     4096 May 26 12:08 ttt/

leecokie@95b8cf2166b7:~$ touch qt/df.txt
touch: cannot touch 'qt/df.txt': Permission denied

leecokie@95b8cf2166b7:~$ ls /home/queen/test
ls: cannot access '/home/queen/test': Permission denied

```
- **상황** : queen에서 test 폴더에 `chmod 777 test`로 모든 권한을 부여했지만 leecokie 계정에서는 접근불가
	- `ls` 명령어 자체가 안됨
  
- chatGPT

| Problem                                         | Solution                                    |
| ----------------------------------------------- | ------------------------------------------- |
| `/home/queen/test` not accessible to `leecokie` | Because `/home/queen` has restricted access |
| `test` has `777`, but it's not enough           | Parent folder permissions also matter       |
| `lrwxrwxrwx` means symbolic link                | Check where it's pointing using `ls -l`     |
| Fix it by changing parent folder permissions    | `chmod o+x /home/queen` (use with caution)  |
| Or move to a shared location                    | e.g., `/tmp` or `/home/shared_test`         |

- **파악** : `queen` 폴더에 대한 권한이 없기때문!
	- 결국 권한 문제 - 선생님 권한 설정과 내 설정이 같은지 확인
		- 선생님은 다른 사람도 읽고 생성하는 권한이 있는데 나는 없음
- **해결** :  r, x 권한 필요 -> 설정


### 🚧 7th error: pip3 install requests

```shell
root@8cd85de1a641:/usr/bin# pip3 install requests 
error: externally-managed-environment
× This environment is externally managed 
╰─> To install Python packages system-wide, try apt install python3-xyz, where xyz is the package you are trying to install. 

If you wish to install a non-Debian-packaged Python package, create a virtual environment using python3 -m venv path/to/venv. 
Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make sure you have python3-full installed. 

If you wish to install a non-Debian packaged Python application, it may be easiest to use pipx install xyz, which will manage a virtual environment for you. Make sure you have pipx installed. See /usr/share/doc/python3.12/README.venv for more information. 

note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages. 
hint: See PEP 668 for the detailed specification.
```
- This is a new protection mechanism in **modern Python installations (PEP 668)** that *prevents you from installing packages system-wide with pip to avoid conflicts with system packages. (chatGPT)*

#### Option 1: Use system packages (Recommended) <- **해결**
```bash
apt-get install python3-requests
```
#### Option 2: Create a virtual environment
```bash
# Install python3-venv if not already installed
apt-get install python3-venv

# Create a virtual environment
python3 -m venv myenv  # ubunenv

# Activate the virtual environment
source myenv/bin/activate

# Now you can use pip normally
pip install requests

# When done, deactivate
deactivate
```




---

### zsh-autosuggestions 비활성화
- 선생님께서 공부하는 동안에 명령어에 익숙해지도록 자동완성기능을 끄는걸 추천해주셔서 비활성화를 하려고  [zsh-users 깃허브](https://github.com/zsh-users/zsh-autosuggestions)에서 방법을 찾았다.
- zsh-autosuggestions README 파일을 보다가 key binding이 있는걸 보고 적용!

> [Key Bindings](https://github.com/zsh-users/zsh-autosuggestions#key-bindings)
 This plugin provides a few widgets that you can use with `bindkey`: 
>1. `autosuggest-accept`: Accepts the current suggestion.
>2. `autosuggest-execute`: Accepts and executes the current suggestion.
>3. `autosuggest-clear`: Clears the current suggestion.
>4. `autosuggest-fetch`: Fetches a suggestion (works even when suggestions are disabled).
>5. `autosuggest-disable`: Disables suggestions.
>6. `autosuggest-enable`: Re-enables suggestions.
>7. `autosuggest-toggle`: Toggles between enabled/disabled suggestions.

- 여러 옵션이 있는데, 이 중에서 토글을 선택 
	- 공부하는 동안엔 자동완성기능을 끄고, 작업할때는 다시 켤수 있도록 세팅
- .zshrc 파일안에 아래 줄을 추가하면 된다
	- `bindkey '{여기에 연결할 키를 입력}'` 
	- 나는 ctrl+a 조합으로 했다
- `source ~/.zshrc` 로 파일을 적용하면 끝!
```vim
bindkey '^a' autosuggest-toggle
```



---

# 📝 수업
> 수업 필기 내용을 claude로 정리 

## 메모리 구조
- **커널(Kernel)**: OS의 핵심 부분, 하드웨어와 소프트웨어 간의 인터페이스 역할
- **힙(Heap)**: 동적 메모리 할당 영역
- **스택(Stack)**: 함수 호출 시 지역변수, 매개변수 저장 영역
- **데이터(Data)**: 전역변수, 정적변수 저장 영역

## 리눅스 배포판과 패키지 관리자
### Rocky Linux
- **특징**: Red Hat 계열 리눅스 배포판
- **용도**: CentOS의 대안으로 많이 사용
- **패키지 관리자**: `yum`, `dnf` 사용
- **Ubuntu와의 차이**: Ubuntu는 Debian 계열로 `apt` 사용

### 패키지 관리자가 다른 이유
- 각 OS마다 고유한 시스템 구조에 맞게 설계
- C언어로 작성된 프로그램도 OS에 따라 다른 머신코드로 컴파일됨
- 의존성 관리 방식과 패키지 포맷이 배포판마다 다름

## 운영체제와 Shell
### macOS (Darwin)
- **커널**: Darwin 커널 사용
- **특징**: 성능이 빠름

### Shell 진화 과정
```
sh → (csh) → bash → (csh) → zsh→ warp
```
- 각 단계마다 더 많은 기능과 편의성 추가
- 모든 Shell은 커널과 상호작용

## 가상화 기술 비교

### Virtual Machine vs Docker

| 구분    | Virtual Machine           | Docker                      |
| ----- | ------------------------- | --------------------------- |
| 구조    | 호스트 OS *위*에 완전한 게스트 OS 설치 | 호스트 Linux OS *안*에서 컨테이너로 실행 |
| 자원 사용 | 무겁고 많은 자원 소모              | 가볍고 효율적                     |

### Docker 볼륨 마운트 예시
```bash
./data:/root/data
```
- 호스트의 현재 디렉토리의 `data` 폴더
- Docker 컨테이너의 `/root/data` 폴더와 연결

## 주요 리눅스 명령어
### 파일 시스템 탐색
```bash
ls -al  # a(all files including hidden), l(long format list)
find . -name "filename"  # 현재 디렉토리 하위에서 파일 검색
```

### 시스템 모니터링
```bash
vmstat 1  # 1초마다 시스템 상태 갱신
```
- **r**: 실행 대기 중인 프로세스 수
- **id**: idle 상태 (CPU 유휴 시간 비율)

```bash
sar  # 시스템 활동 리포터 - "서버와 인사하기"
```
- 정기적인 서버 상태 모니터링에 사용

### 파일 전송
- **rsync**: 서버 간 차이점만 비교해서 변경된 데이터만 전송 (효율적)
- **rcp**: 서버 전체를 복사해서 전송 (비효율적)

### 텍스트 처리
```bash
sed    # 문자열 치환 도구
awk    # 문자열 검색 및 패턴 매칭
```
- 로그 파일 분석 시 `sort`, `uniq`와 함께 활용

## 프로세스 vs 스레드
### 리눅스 vs 스프링
- **리눅스**: 프로세스 기반 처리
- **스프링**: 스레드 기반 처리

### 스레드 관리 주의사항
- 로컬에서 블록된 스레드는 즉시 종료해야 함
- 이유: 스레드는 메모리를 공유하므로 하나가 블록되면 전체 애플리케이션이 영향받을 수 있음

## 설정 파일

### Shell 설정
- **cshrc**: C Shell의 Runtime Configure 파일
- **.bashrc**: Bash Shell의 설정 파일
- **.bash_profile**: Bash 로그인 시 실행되는 설정 파일

### Docker 실행 과정
1. Docker 컨테이너 실행
2. 사용자의 Shell 타입(bash)으로 진입
3. `.bashrc`와 `.bash_profile` 자동 실행

## 디렉토리 구조
- **bin**: Binary 실행 파일들이 저장된 디렉토리
