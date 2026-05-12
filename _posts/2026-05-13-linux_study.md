---
layout: post
title: 리눅스 기반 시스템 탐색 및 데이터 분석
subtitle: frontier mission
header-img: img/in-post/2020-10-07/header.jpg
header-style: text
catalog: true
tags:
  - 블로그/기술문서
  - 리서치
---

# 리눅스 기반 시스템 탐색 및 데이터 분석

---

## 목표

WSL(Windows Subsystem for Linux) 환경에서 리눅스 기본 명령어를 활용하여 파일 시스템을 탐색하고, 숨김 파일 및 특수 파일을 식별하며, 인코딩된 데이터를 해석하는 능력을 습득한다. 또한CLI(Command Line Interface) 환경에 익숙해지고, 보안 및 시스템 분석의 기초 역량을 기른다.

---

### 레벨 0

![image.png](img/bandit/image.png)

이번 목표는 ssh를 이용해서 bandit에 접속을 해 보는 것이다.

> ssh [호스트] [포트]
> 

를 입력하면 된다.

`pw: bandit0` 

---

### 레벨 0 → 1

![image.png](img/bandit/image%201.png)

단순하게 readme파일 내부에 있는 PW를 얻으면 된다.

![image.png](img/bandit/image%202.png)

접속 후 ls를 통해 파일을 확인하고 cat으로 파일 내용을 확인한다.

> ls : 현제 디렉토리에 있는 파일 확인
cat : 파일 내용 출력
> 

pw : ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

---

### 레벨 1 → 2

![image.png](img/bandit/image%203.png)

‘-’라는 파일을 열면 된다.

![image.png](img/bandit/image%204.png)

비밀번호는  ‘-‘ 라는 파일에 저장되어 있다고 한다.

보통 dash(-)는 명령어의 옵션과 arguments로 사용되기 때문에 ‘-’ 파일을 열기위해서는 cat 명령어만으로는 보이지 않는다.  ‘-’으로 시작하는 경우엔 .`/-file.txt` 를 이용한다

pw : 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

---

### 레벨 2 → 3

![image.png](img/bandit/image%205.png)

이번엔 공백이 있는 파일을 열면 된다.

![image.png](img/bandit/image%206.png)

공백이 있으면 `“name”` 형식으로 쓰면 내부에 있는 내용 전체를 이름으로 인식한다.

pw : MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

---

### 레벨 3 → 4

![image.png](img/bandit/image%207.png)

이번 문제는 디렉토리 내부 숨겨진 파일에 있는 pw를 찾는 것이다.

![image.png](img/bandit/image%208.png)

`-a` 옵션을 주면 숨겨진 모든 파일이 보인다.

pw : 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

---

### 레벨 4 → 5

![image.png](img/bandit/image%209.png)

이번엔 “사람이 읽을 수 있는” 수식어가 붙어있다.

![image.png](img/bandit/image%2010.png)

같은 방법으로 파일을 확인해 주고 `file ./*`  명령어를 통해 파일의 타입을 확인했다. 그리니 사람이 볼 수 있는 ASCII 파일이 하나 있다.

pw : 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw 

---

### 레벨 5 → 6

![image.png](img/bandit/image%2011.png)

이번엔 1033바이트라는 조건이 있다. 이럴때는 f`ind` 명령어를 활용하면 좋다.

![image.png](img/bandit/image%2012.png)

`find` 명령어에 크기 필터를 적용시켜서 찾아서 바로 찾을 수 있었다.

pw : HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

---

### 레벨 6 → 7

![image.png](img/bandit/image%2013.png)

이번에는 저건들이 더 많아 졌다. 이번엔 `grep`도 사용하면 좋을 것 같다.

![image.png](img/bandit/image%2014.png)

이렇게 작성 해 줬다. 근데 하고 보니 grep은 사용하지 않아도 됬었을 것 같다.

> 2>/dev/null은 오류 메시지들을 지우는 설정이다.
> 

pw : morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

---

### 레벨 7 → 8

![image.png](img/bandit/image%2015.png)

이번에는 진짜 grep을 쓰면 될 것 같다.

![image.png](img/bandit/image%2016.png)

짜라안

pw : dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

---

### 레벨 8 → 9

![image.png](img/bandit/image%2017.png)

로그인 후 ls 로 파일 목록을 확인하고 sort 명령어를 통해 문자열을 정렬하고 유일하게 한번만 나타나는 텍스트라고 하였으니 uniq -u 를 통해 중복되지 않는 줄만 출력하도록 한다.

![image.png](img/bandit/image%2018.png)

> 
> 
> 
> sort : 문자열 정렬
> uniq -u : 중복되지 않은 줄만 출력
> Pipe () : 왼쪽 출력을 오른쪽 입력 전달한다.
> 

pw : 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

---

### 레벨 9 → 10

![image.png](img/bandit/image%2019.png)

> strings : 바이너리 파일의 문자열을 추출 출력 해줍니다.
> 

![image.png](img/bandit/image%2020.png)

짜라안

pw :  FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

---

### 레벨 10 → 11

![image.png](img/bandit/image%2021.png)

이번엔 base64로 인코딩 되있다 합니다. 디코딩을 해줘야 겠죠?

![image.png](img/bandit/image%2022.png)

`-d` 옵션을 넣어주면 디코딩이 됩니다.

pw : dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

---

### 레벨 11 → 12

![image.png](img/bandit/image%2023.png)

이번에는 rot13이 되있다고 합니다 이것도 복구를 해줘야 겠죠

![image.png](img/bandit/image%2024.png)

> tr : 문자 치환 명령어
> 

pw : 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

---

### 레벨 12 → 13

![image.png](img/bandit/image%2025.png)

이번엔 압축이 되어 있다고 합니다. 그리고 /tmp 디렉토리 밑에서 작업을 하라고 합니다.

> `mktemp -d` 는 임시 디렉터리(temporary directory)를 만드는 명령이다.
> 

![image.png](img/bandit/image%2026.png)

![image.png](img/bandit/image%2027.png)

![image.png](img/bandit/image%2028.png)

좀 초반에 많이 길을 잃긴 했는데 한번 알고 나서 계속 같은 확장자 바꾸고 압축 풀고 확장자 바꾸고 압축 풀고를 반복했습니다.

pw : FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

---

### 레벨 13 → 14

![image.png](img/bandit/image%2029.png)

이번에는 /etc/bandit_pass/bandit14에 password가 저장되있다고 합니다. 근데 ssh 개인키를 이번에 준다고 합니다.

![image.png](img/bandit/image%2030.png)

> HINT
> 
> 
> 이 레벨에서 문제가 발생하면 다음 사항을 참고하세요.
> 
> 1. 다른 모든 레벨과 마찬가지로, 이 레벨에도 정보가 있는 웹사이트가 있습니다.
> 
> [https://overthewire.org/wargames/bandit/bandit14.html](https://overthewire.org/wargames/bandit/bandit14.html)
> 2) 레벨에 오류가 있는 것이 아닙니다. 다음 링크에서 확인하세요.
> 
> [https://status.overthewire.org/](https://status.overthewire.org/)
> 3) 현재 OverTheWire 버전에서는 localhost를 통해 한 레벨에서 다른 레벨로 로그인하는 것이 불가능합니다.
> 
> 로그아웃 후 1번을 참조하세요.
> 4) 오류가 발생하면 화면에 표시되는 오류 메시지를 읽어보세요.
> 정말입니다!
> 

이렇게 힌트가 있습니다.

![image.png](img/bandit/image%2031.png)

개인키를 따로 저장을 해준 다음에 권한을 설정을 해주고 접속을 해 보면 접속이 된다.

![image.png](img/bandit/image%2032.png)

그리고 키를 획득할 수 있다.

pw : MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

---

### 레벨 14 → 15

![image.png](img/bandit/image%2033.png)

이번에는 localhost를 이용해서 포트를 전송하면 키를 얻을 수 있다고 합니다.

![image.png](img/bandit/image%2034.png)

> 
> 
> 
> netcat (nc) : TCP 연결 테스트 도구
> 
> Pipe 입력 : echo 결과를 nc로 전달
> 

pw : 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

---

### 레벨 15 → 16

![image.png](img/bandit/image%2035.png)

이번에는 보안 연결을 통해 비밀번호를 전송을 해야 합니다. 이건 저도 처음 봐서 인터넷에 찾아봐서 명령어를 찾아봤습니다.

![image.png](img/bandit/image%2036.png)

pw : kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

---

### 레벨 16 → 17

![image.png](img/bandit/image%2037.png)

이번에는 31000~32000포트 중 SSL을 지원하는 서버를 찾아서 비밀번호를 입력을 해야 한다.

> **`nmap` — 네트워크 스캐너**
> 

`-sV` 옵션으로 각 포트가 echo 서버인지 SSL 서버인지 파악한다. SSL이 적용된 포트 중 비밀번호를 입력했을 때 그대로 반환하지 않는 포트를 찾아야 한다.

![image.png](img/bandit/image%2038.png)

이렇게 얻은 키를 위에 키를 입력해서 접속하는 방법

`ssh -i sshkey.private [bandit14@bandit.labs.overthewire.org](mailto:bandit14@bandit.labs.overthewire.org) -p 2220`

로 접속을 하면 된다.

---

### 레벨 17 → 18

![image.png](img/bandit/image%2039.png)

그리고 설명해서 “암호는 **passwords.new 파일에 있으며, passwords.old와 passwords.new 파일** 사이에서 변경된 유일한 줄입니다.”라고 했기 때문에 

> `diff [비교할 파일1] [비교할 파일2]`
> 

![image.png](img/bandit/image%2040.png)

pw : x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

---

### 레벨 18 → 19

![image.png](img/bandit/image%2041.png)

 **.bashrc 파일** 을 수정하여 SSH로 로그인할 때 로그아웃되도록 설정했다 되있습니다.

![image.png](img/bandit/image%2042.png)

접속을 하면 Byebye ! 가 뜨면서 로그아웃 된다. 이럴땐 접속할때 실행할 명령어를 적어주면 된다.,

![image.png](img/bandit/image%2043.png)

pw : cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

---

### 레벨 19 → 20

![image.png](img/bandit/image%2044.png)

다음 레벨로 진입하려면 홈 디렉터리에 있는 setuid 바이너리를 사용해야 한다고 합니다.

> 
> 
> 
> **SetUID:**
> 
> 파일을 실행할 때 실행한 사람의 권한이 아니라 파일 소유자의 권한으로 실행되게 하는 특수 권한
> 
> `rws r-x r-x` 형태로 표시됨
> 

![image.png](img/bandit/image%2045.png)

pw : 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

---

### 레벨 20 →21

![image.png](img/bandit/image%2046.png)

setuid 바이너리가 지정한 포트의 localhost에 연결하여 bandit20 비밀번호를 확인하고, 맞으면 bandit21 비밀번호를 전송하는 문제인데 흠 어렵네요..

Netcat과 suconnect 동작 정리

1. Netcat(nc)이란?

`Netcat`은 네트워크 연결을 확인하거나 간단한 서버/클라이언트를 구성할 때 사용하는 도구이다.

TCP 또는 UDP 통신 테스트에 자주 사용되며, 특정 포트에서 데이터를 주고받는 기능을 제공한다.

이번 문제에서는 특정 포트에서 연결 요청을 기다리는 서버 역할로 사용하였다.

```bash
nc -lvp 8888
```

---

1. 사용한 옵션

| 옵션 | 설명 |
| --- | --- |
| `-l` | 연결 요청을 기다리는 listen 모드 |
| `-v` | 접속 정보를 자세하게 출력 |
| `-p` | 사용할 포트 번호 지정 |

위 명령은 8888번 포트에서 외부 연결을 기다리는 상태가 된다.

---

1. 파이프(|)를 이용한 데이터 전달

```bash
echo "password" | nc -lvp 8888
```

파이프(`|`)는 앞 명령의 출력 결과를 뒤 명령의 입력으로 전달한다.

따라서 위 명령에서는 `echo`가 출력한 문자열이 `nc`로 전달되며,

클라이언트가 접속했을 때 해당 문자열이 그대로 전송된다.

즉, 접속한 대상은 `"password"` 문자열을 받게 된다.

---

1. 백그라운드 실행 이유

```bash
echo "password" | nc -lvp 8888 &
```

명령어 끝에 `&`를 붙이면 프로세스가 백그라운드에서 실행된다.

이번 문제에서는 `nc`가 계속 포트를 열어둔 상태여야 했기 때문에 백그라운드 실행을 사용하였다.

이렇게 하면 현재 터미널을 계속 사용할 수 있어 이후 `suconnect` 명령을 같은 창에서 실행 가능하다.

---

1. 전체 동작 과정

전체 흐름은 아래와 같다.

```
echo → nc(8888 포트 대기)
             ↑
      suconnect 8888
```

1. `nc`가 8888번 포트에서 연결 대기
2. `suconnect`가 해당 포트로 접속
3. `nc`가 전달받은 비밀번호 문자열 전송
4. `suconnect`가 비밀번호를 검사
5. 인증 성공 시 다음 단계 비밀번호 출력

결과적으로 `nc`는 비밀번호를 전달하는 간단한 서버 역할을 수행한 것이다.

<aside>
💡

여기 부분은 공부하면서 저도 처음보고 신기해서 조사를 많이 하게 되었습니다.

</aside>

![image.png](img/bandit/image%2047.png)

pw : EeoULMCra2q0dSkYj561DX7s1CpBuOBt

---

### 레벨 21 → 22

![image.png](img/bandit/image%2048.png)

> 
> 
> 
> `crontab -l    # 목록 보기
> crontab -e    # 편집
> crontab -r    # 삭제`
> 

![image.png](img/bandit/image%2049.png)

해석:

- 서버 부팅 시 실행
- 매 1분마다 실행
- 실행 계정: bandit22
- 실행 파일: /usr/bin/cronjob_bandit22.sh

즉 1분마다 bandit22 권한으로 특정 스크립트가 실행된다.

![image.png](img/bandit/image%2050.png)

![image.png](img/bandit/image%2051.png)

pw : tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q

---

### 레벨 22 → 23

![image.png](img/bandit/image%2052.png)

이전 레벨과 동일한 접근으로 `cronjob_bandit23.sh`을 분석 해보자ㅏㅏ

![image.png](img/bandit/image%2053.png)

코드를 보면 `echo I am user bandit23 | md5sum | cut -d ' ' -f 1` 의 결과를 파일명으로 사용하여 `/tmp/$mytarget`에 비밀번호를 저장하는 것 같다. 그럼 파일명 그리고 pw순으로 알아내면 될 거 같다.

![image.png](img/bandit/image%2054.png)

pw : 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga

---

### 레벨 23 → 24

![image.png](img/bandit/image%2055.png)

![image.png](img/bandit/image%2056.png)

```c

#!/bin/bash #bash 쉘을 사용한다 

myname=$(whoami) #bandit24

cd /var/spool/$myname #이동 
echo "Executing and deleting all scripts in /var/spool/$myname:" 
for i in * .*; #모든파일에 대하여 밑에 것 반복 
do 
    if [ "$i" != "." -a "$i" != ".." ];  #파일 이름이 "." 현재디렉토리가 아니고&& ".." 상위 디렉토리가 아니면 
    then 
        echo "Handling $i" 
        timeout -s 9 60 ./$i  #60초 이내에 실행해라 60초를 초과하면timout 그 프로세스를 죽이겠다.-s 9  
        rm -f ./$i  #프로그램 강제-f 제거 rm
    fi 
done 
```

이렇게 해석 할 수 있다. 따라서, bandit24의 비밀번호를 읽어와 다른 곳에 저장하는 스크립트의 파일을 /var/spool/bandit23/foo에 저장하여 그 파일을 실행시켜 비밀번호를 얻어낼 수 있다

![image.png](img/bandit/image%2057.png)

```c
pass.sh

#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/wawa
chmod 644 /tmp/wawa
```

pw : gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8

---

### 레벨 24 →25

![image.png](img/bandit/image%2058.png)

**bandit24 비밀번호 + 4자리 PIN**을 30002번 포트로 전송하면 bandit25 비밀번호를 받을 수 있다. PIN은 0000~9999까지 **브루트포스**해야 한다.

![image.png](img/bandit/image%2059.png)

![image.png](img/bandit/image%2060.png)

```c
#!/bin/bash
PASSWORD="gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8"
for i in {0000..9999}
do
    echo "$PASSWORD $i"
done | nc localhost 30002 > /home/bandit24/wawa
```

코드로 그 전 키와 9999까지를 브포해서 넣는 것을 만들어준다. 사실 저렇게 만들었다 Permission denied가 떠서 그냥 지워서 엄청 뜨게 됐다.

pw : iCi86ttT4KSNe1armKiwbQNmB3YJP3q4

---

## 후기

bandit이란걸 알고는 있었고 초반까지도 했었는데 기억상 10번때 중반 이후로는 한적이 없었는데 이번에 해보게 되니 생각보다 어려운 것도 있고 근데 생각보다 도움이 되는 것 같았다.
