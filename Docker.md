>**강의명** : **풀스택을 위한 도커와 최신 서버 기술(리눅스, nginx, AWS, HTTPS, flask 배포) [풀스택 Part3]**
>
>[강의 링크](https://www.inflearn.com/course/%EC%84%9C%EB%B2%84%EA%B8%B0%EC%88%A0-%ED%92%80%EC%8A%A4%ED%83%9D-3)

# Background

## 모던 서버 기술 관련 **배경지식** 이해

- 최신 서버 기술 큰 그림과 로드맵 이해하기 (도커와 마이크로서비스)
  - 서버는 24시간 구동이 필요하며, 특정 목적으로 사용되는 프로그램이 많음 (웹서버)
  - 다양한 리눅스 패키지와 업데이트로, 프로그램 **설정 등이 수시로 달라짐**
  - 서버 이전 시 이전할 서버에 맞도록 재설정이 필요하게 됨
  - => 도커 출현
  - **도커는 서버 환경을 감싸서,** 도커 레벨로 서버를 다룰 수 있음 (`도커로 말았다` 라는 표현)
    - 따라서, 서버 패키지 버전 변경 등등으로 일일이 서버 설정이 불필요
    - 단순히 도커를 만들어서, 서버에서 실행만 하면 됨.
- 웹 서비스 개발과 `마이크로서비스`
  - **모놀리틱 구조**
    - 하나의 서버에 모든 기능을 넣는 구조
    - MVC 패턴으로 구조화하려는 노력은 있으나, 어쨌든 하나의 서버가 모든 기능을 담당
  - <-> **마이크로 서비스**
    - 서비스가 방대해짐에 따라, 하나의 서버에 모아놓으면, 특정 기능의 문제로 전체 시스템에 장애가 발생
    - **여러 서버에 각 기능을 분산**해놓은 후, Rest API 등으로 통신을 통해 전체 서비스를 운영

## DevOps

- **등장 배경**
  - 본래 새로운 기능을 개발팀에서 릴리즈하면, 개발팀은 운영팀에 어떻게 운영할 지 알려줘야.
    - 그러나, micro features라면, 많은 기능을 제대로 알려주기 어렵고,
    - 운영이 잘 안될 경우, 이 부분은 개발팀 역할이 아니므로 운영팀에 제대로 안 알려줌
  - => 운영 + 운영시스템 효율화 / 자동화 프로젝트를 목표로 부여
    - 개발자가 목표를 가지고 개발을 할 수 있음
    - 개발자는 micro features에 대해서도 빠르게 이해할 수 있 (다양한 기술 습득)
- **자동배포**
  - Realease System 자동화
  - 코드 리뷰, 테스트 자동화
  - 서비스 모니터링 시스템
  - 이슈 발생시 커뮤니케이션 시스템
- 각 마이크로 서비스를 도커로 개발 => **도커 개발**
- 초대용량 서비스 유지 보수를 위한 서버 핸들링 필요 (예 : 네트워크 트래픽에 따른 서버 관리) => **쿠버네티스 개발**
- 수시 릴리즈를 지원하기 위한 배포 시스템
  - 개발자가 git에 신규 코드를 릴리즈하면,
  - Jenkins/Travis CI 등으로 서버 자동 재가동
  - => **배포 자동화**
- 수시 릴리즈시, 서비스는 중단되지 않았으면 좋겠음 => **무중단 배포**



## 리눅스 역사 (별로 안 중요)

- 서버에 많이 사용되는 운영체제
- 오픈 소스 운동
- GNU / Linux



## AWS 맥에서 접속하기

```shell
chmod 400 kimjuho.pem 
```

```shell
ssh -i kimjuho.pem ubuntu@52.79.179.194
```



## 리눅스와 파일

- 모든 것은 **파일**이라는 철학을 따름

  - 모든 interaction은 파일을 읽고, 쓰는 것처럼 이루어져 있음
  - 마우스, 키보드와 같은 모든 디바이스 관련된 기술도 파일과 같이 다루어짐

- shell

  - 사용자와 컴퓨터 하드웨어 또는 운영체제간 인터페이스
  - 사용자의 명령을 해석해서, 커널에 명령을 요청해주는 역할
  - 관련된 system call을 사용해서 프로그램이 작성되어 있다.

- **하드링크와 소프트링크**

  - cp 명령 :  파일 복사

    ```shell
    cp [origin file] [new file]
    ```

  - A와 B는 각각 물리적으로 10MB 파일로 저장

  - 하위 폴더를 포함하여 복사하기

    ```shell
    cp -rf * 폴더
    ```

    

  - **하드링크**
    - `ln [origin file] [new file]`
      - A와 B는 동일한 i-node를 서로 다른 포인터로 가리키고 있는 것일 뿐
      - `[new file]`이 바로가기 파일인 셈
  - **소프트링크 (심볼릭링크)**
    - windows OS의 바로가기와 동일
    - `ls - al`하면, 소프트링크 확인 가능



## ubuntu

- 리눅스 커널 + bash shell + 다양한 프로그램의 조합에 따라 여러가지 리눅스 배포판이 있을 텐데 그 중 하나
- CentOS나 Fedora와 같은 RedHat 계열 배포판은 `RPM`이라는 패키징 시스템을 사용함
- ubuntu와 같이 데비안 계열 배포판은 deb라는 패키징 시스템을 사용함



## ubuntu 패키지 관리 실무

- ubuntu 패키지 인덱스 정보(배포판 버전에 따른 패키지 업데이트 버전 정보 등) 업데이트

  ```shell
  sudo apt-get update
  ```

- 설치된 ubuntu 패키지 업그레이드 (함부로 하지 말것)

  ```shell
  sudo apt-get upgrade
  ```

- 패키지 설치

  ```shell
  sudo apt-get install 패키지명
  ```



## VIM 에디터 이해 및 설치

- `VIM`
  - Vim은 Vi에 자동화, 시각화 메뉴 등을 추가한 프로그램
  - Vim 이외에 이맥스(Emacs)라는 유명한 에디터가 있음



# 설치

## docker 설치

1. 최신 패키지 리스트 업데이트

```shell
sudo apt update
```

2. docker 다운로드를 위해 필요한 https 관련 패키지 설치

```shell
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

3. docker repository 접근을 위한 GPG key 설정

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

4. docker repository 등록

```shell
sudo add-apt-repository "dep [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

5. 등록한 docker repository까지 포함하여 최신 패키지 리스트 업데이트

```shell
sudo apt update
```

6. docker 설치

```shell
sudo apt install docker-ce
```

7. docker 실행 중임을 확인

```shell
sudo systemctl status docker
```



## sudo 명령 없이 docker 명령어 사용하기 설정

1. 현재 사용자(ubuntu) ID를 docker group에 포함시킴

```shell
sudo usermod -aG docker ${USER}
```

2. 터미널을 끊고, 다시 ssh로 터미널 접속 (로그인을 다시 하는 것임)
3. 현 ID가 docker group에 포함되어 있는지를 확인하는 명령 (docker가 리스트에 나오면 됨)

```shell
id -nG
```

4. 이제 docker 없이 docker 명령을 바로 내릴 수 있음



## docker-compose 설치

1. release page에서 최신 버전 확인 후, 다음 링크에서 버전(1.28.2) 변경

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

2. 실행 권한을 준다.

```shell
sudo chmod +x /usr/local/bin/docker-compose
```

3. 다음 명령 실행시 버전 확인이 가능하면, 성공

```shell
docker-compose --version
```



# 도커에 대한 기본 이해

## LCX (Linux Containers)

- docker는 **리눅스 컨테이너**부터 시작된 기술임.
- 단일 컴퓨팅 시스템에 설치된 리눅스 운영체제 상에서, **다른 영역과 완전히 분리된 별도의 리눅스 시스템**을 운영할 수 있는 리눅스 커널 기술
- 리눅스 운영체제 레벨에서 영역과 자원 할당 (CPU, 메모리, 네트워크) 등을 **분리**하여, **마치 별도의 시스템**처럼 사용할 수 있는 기술을 의미함
- **docker는 리눅스 커널에 LXC 기술을 사용**해서,
  - "리눅스 컨테이너"를 만들고, (분리된 공간을 리눅스 컨테이너라고 부름)
  - 리눅스 컨테이너 상에 **별도로 구성된 파일 시스템**에 시스템 설정 및 응용 프로그램을 실행할 수 있도록 하는 기술을 정의한 것이라고 이해하면 됨.

> 초기 docker는 LXC 기술을 기반으로 구현되었으나, 최근에는 별도 컨테이너 기술을 구현하여 사용하고 있음



## Docker 주요 구성 요소

### Docker Engine

- docker는 **서버 / 클라이언트 구조**로 이루어짐
  - 서버는 docker `daemon process` (데몬 프로세스) 형태로 동작함
    - **데몬**이란, 보통 **계속 실행 중인 프로그램**으로 이해하면 됨 (계속 떠있다고도 이야기함)
  - docker daemon process에 요청하기 위해, 프로세스간 통신 기법이 필요하며, docker는 이를 위해 **Rest API**를 사용함
    - 참고 : 더 깊은 이해를 위해서는 컴퓨터공학 운영체제의 프로세스 구조와 **프로세스간 커뮤니케이션(IPC)** 부분을 이해해야 함
  - **docker command는 일종의 클라이언트**라고 이해하면 됨
    - docker command를 내리면, 결국 내부적으로 Rest API를 사용해서, docker daemon process를 호출하는 방식
    - 예 :
      - `docker ps`라고 명령하면, 내부적으로는 마치 다음 명령처럼 Rest API로 호출함
        - `http GET 'docker daemon process'/api-version/containers`



 ## docker image

- docker 컨테이너를 생성하기 위한 명령들을 가진 템플릿
- **image는 script의 집합에 불과**. 그 script의 구성이 어떻게??
  - "ubuntu를 설치하라"하는 script, 그 위에 "webserver를 설치해라" 하는 script, 그 위에 "내가 작성한 장고 코드를 도커 container에 넣어라"하는 script, ...
  - 위 처럼 여러 개의 layer를 쌓는 형태의 script가 최종적으로 하나의 image를 만든다.
  - 도커 이미지는 이렇게 레이어(layer)를 중첩하는 방식으로 생성되기 때문에, **한번 빌드된 이미지의 베이스 레이어는 캐싱되어 이후 다른 이미지를 빌드할 때 재활용**할 수 있다.
  - **=> 디스크의 용량을 효율적으로 이용한다.**
  - ex ) ubuntu 이미지에, apache 웹서버 이미지를 얹어서 이지미를 만듦
  - 이런 퍼블릭한 이미지들을 사용하면, 다양한 설정들을 프로그래머가 bottom up으로 하나씩 설정해주는 그 과정 없이 **버전의 이미지 이름만 알면** 바로 다운받아서 바로 그 공식 프로그램을 쓸 수가 있다.



## docker container

- docker image가 리눅스 컨테이너 형태로 실행한 상태 (instance)를 의미함
- docker daemon에 있는 커널에서 LXC로 **리눅스 컨테이너를 생성**한 후, 해당 컨테이너에 docker image에 포함된 명령을 실행하여, **docker container를 만들고** 실행함.
- docker container는 분리된 공간이므로, docker daemon process를 통해, 접속할 수도 있고, 내부에 들어가서 코드 수정, 재실행 등도 가능함!

> 결국 docker는 image와 container를 다뤄서 작업을 한다고 이해하면 됨!



# 유니온 파일 시스템 (UFS)

> 출처 : [도커 공식문서](https://docs.docker.com/storage/storagedriver/)

> 출처 : [산티아고의 기술블로그](https://velog.io/@koo8624/Docker-%EC%9C%A0%EB%8B%88%EC%98%A8-%ED%8C%8C%EC%9D%BC-%EC%8B%9C%EC%8A%A4%ED%85%9C-Union-File-System)



- 도커가 **어떻게 이미지를 Layer 단위로 관리할까**
- **UFS**
  - **여러 개의 파일 시스템을 하나의 파일 시스템에 마운트하는 기능**
  - 여러 파일 시스템을 하나로 합치다보면, 중복되는 파일이 분명히 있다.
  - UFS는 이 경우 나중에 마운트된 파일로 덮어 써버린다. (-> 디스크에 효율을 줌)
- UFS in Docker
  - 하나의 이미지에서 생성된 컨테이너들이 동일한 파일 시스템을 **공유하고 있다면** 어떻게 컨테이너가 **독립적으로** 실행될 수 있는가?
  - 즉, "공유"와 "독립"은 양립하기에 어색한 표현은 아닌가?
  - **=> UFS의 COW(Copy on Write) 전략**
    - 하위 레이어(base layer) 위에 새로운 layer가 쌓일 경우, 하위 layer는 `READ ONLY` 상태가 된다.
    - 상위 layer에서 하위 layer를 **복사하여 사용(CoW)하기 때문에**, 상위 layer는 하위 layer에 아무런 영향을 주지 않는다.
- 도커에서 관리되는 모든 레이어와 관련된 정보는 호스트의 파일시스템 내의 `/var/lib/docker` 폴더에 저장된다.
- 이 영역을 `Docker Area` 혹은 `Backing Filesystem`이라고 부른다.

# docker 관련 명령어

### 이미지 명령

- 로그인

```shell
docker login
```

- 다운받을 이미지 검색

```shell
docker search [이미지명]

# 5개만
docker search --limit=5 [이미지명]
```

- 이미지 다운로드

```shell
docker pull ubuntu

# 특정 태그에 해당하는 버전 다운로드
docker pull ubuntu:20.10
```

- 이미지 목록 확인

```shell
docker images
# 혹은 docker image ls

# 이미지 ID만 표시 (다른 명령이랑 조합시 필요한 경우 많음)
docker images -q
# 혹은 docker image ls -q
```

- 이미지 삭제

```shell
docker rmi 이미지ID(또는 이미지 REPOSITORY)
# 또는 dockder image rm 이미지ID(또는 이미지 REPOSITORY)
```



### 컨테이너 명령

- 컨테이너 생성

```shell
docker create ubuntu

# 이름 지정 [내가원하는컨테이너이름] [이미지이름]
docker create --name myubuntu ubuntu
```

- 생성된 컨테이너 확인

```shell
# 실행중인 컨테이너 확인
docker ps

# 모든 컨테이너 확인
docker ps -a

# id만 출력
docker ps -a -q
```

- 컨테이너 삭제

```shell
docker rm [삭제할 컨테이너 이름]
```

- docker 실행

```shell
docker start [컨테이너 이름]
```

- docker run 명령
  - ubuntu 자체만으로 컨테이너를 만들 경우, 다음 명령으로 터미널 및 입력(`STDIN`)을 연결해줘야 함
  - `-it` 옵션의 의미
    - docker 컨테이너에 표준 입력을 오픈해놓고, (`-i` 옵션)
    - pseudo tty를 만들어서 (`-t` 옵션) 해당 표준 입력을 pseudo tty에 연결해놓음
    - 따라서, 키보드 입력을 pseudo tty를 통해 컨테이너의 표준 입력으로 전달할 수 있도록 하는 것

```shell
# 컨테이너 실행 후, 해당 ubuntu 내로 들어가서, 터미널로 명령을 진행할 수 있음
docker run -it ubuntu

# 컨테이너 이름을 원하는 이름으로 변경 시
docker run -it --name myubuntu ubuntu
# exit 명령으로, 종료시 컨테이너도 "중지"됨
docker ps -a

# 컨테이너 종료시 자동으로 컨테이너까지 삭제하는 옵션
docker run -it --rm --name myubuntu2 ubuntu
# exit 명령으로, 종료시 컨테이너도 "중지"됨
docker ps -a

# 컨테이너를 백그라운드로 실행하기 (실행중인 상태이지만, 터미널로 입력은 받지 않은 상태로 만들어보기)
docker run -it -d --name myubuntu3 ubuntu
# 다음 명령으로 실행 중임을 확인
docker ps
```

- 실행중인 컨테이너 종료하기

```shell
docker stop myubuntu
```

> 실행 중인 컨테이너의 실행 상태를 잠깐 먼추는 명령은 `docker pause`이며, 다시 실행은 `docker unpause`



## 웹서버로 docker run 옵션 테스트 해보기

```shell
# 웹 서버 프로그램
docker search httpd --limit=5
```

### foreground 실행

```shell
# foreground 실행
docker run httpd
```

- 위 처럼 foreground로 실행하게 되면, command line에 명령을 할 수가 없다.
  - apache 웹서버가 실행된 상태로, 해당 프로그램 로그만 화면에 보여진다.
  - `ctrl + c`로 강제 중단시킨 후, 다음과 같이 명령 (관련 컨테이너는 중지 상태에 있으므로, 삭제해줘도 됨)
  - `-d` 옵션을 주어 background에서 해당 컨테이너를 실행하면 됨.
  - 보통 컨테이너는 background로 실행하는 것이 일반적



### background 실행

```shell
# background 실행
docker run -d --name apacheweb httpd
```

- 이번에는 해당 웹서버에 어떻게 접속해야할지 알 수가 없음
  - **=> 포트 포워딩**이 필요함
  - docker를 실행한 PC를 `Host PC`라고 함
  - docker 컨테이너가 실행되면, `172.17.0.0/16`(서브넷이 `255.255.0.0`)인 private IP가 할당 됨.
    - `/16`은 16비트까지 IP할당이 된다는 의미로, `172.17.0.0` ~ `172.17.255.255`까지 동일 네트워크 상에 IP 주소를 가질 수 있음을 의미함
  - 호스트 PC IP에 특정 port로 access시, 해당 port를 docker 컨테이너의 특정 private IP의 특정 포트로 변환해줄 수 있음.
  - 이를 **NAPT(Network Address Port Translation)** 기술이라고 함
  - 이를 지원해주는 옵션이 `-p` 옵션
    - 다음과 같이 작성하면, `apacheweb2` 컨테이너는 apache 웹서버 프로그램을 실행하고, 호스트 PC에 9999 포트로 접속하면, 자동으로 이를 해당 컨테이너의 80 포트에 연결해주겠다라는 의미

```shell
docker run -d -p 9999:80 --name apacheweb2 httpd
```

위와 같이 실행 후, 크롬 웹브라우저 상에서 localhost:9999를 접속하면 내부 웹서버가 동작함을 확인할 수 있음

- 나만의 웹서비스 docker 만들기 (`-v` 옵션 이해하기)
  - 'It works'는 httpd 이미지의 apache 웹서버 기본 설정에 의해, `/usr/local/apache2/htdocs` 폴더에 있는 `index.html`에 적혀 있는 html 태그임
  - 따라서, 해당 폴더를 내가 원하는 `index.html` 파일로 교체한다면 나의 웹페이지를 보여줄 수 있음
  - 호스트 PC 상에 나만의 index.html 파일이 있다면, `-v` 옵션을 사용해서, 호스트 PC의 특정 폴더를 docker 컨테이너의 특정 폴더에 심을 수 있음 (동기화)

```shell
# -v 옵션만 적용한다면 다음과 같이 작성
docker run -v [호스트_PC의_절대경로]:[도커_컨테이너_절대경로] httpd

# 다른 옵션과 함께 사용한 예 (호스트 PC 경로에 한글이나 띄어쓰기가 있다면 따옴표로 묶어줘야 함)
docker run -d -p 9999:80 -v /home/ubuntu/2021_DEV_HTML:/usr/local/apache2/htdocs --name apacheweb2 httpd
```

> 현업 팁 : docker 명령을 직접 내릴 때는 명령이 매우 길기 때문에, 보통 메모장 등에 명령셋들을 저장한 후, 복사 / 붙여넣기로 하나씩 실행하는 경우가 많다고 함.



## docker 용량 issues

- 추후 docker가 사용하는 저장매체 공간이 이슈가 될 수 있다.

```shell
docker system df
```



- **docker와 alpine**
  - docker 이미지는 여러개의 이미지가 계층(layer)로 쌓인 형태로 작성이 됨
    - 예를 들면, C 라이브러리 이미지를 쌓고, 여기에 bash와 같은 shell 프로그램 이미지를 쌓고, 여기에 응용 프로그램 이미지를 쌓는 방식
    - 통상 리눅스 사용시, 다양한 기능을 가진 ubuntu 등의 리눅스 패키지를 사용하지만, docker 컨테이너의 경우는 특정 응용 프로그램 실행을 목적으로 하는 경우가 많기 때문에, 다양한 기능을 모두 포함할 필요가 없는 경우가 많다.
    - 동일한 기능을 수행한다면, 도커 이미지 / 컨테이너 사이즈가 작으면 작을 수록 좋다.
  - 대부분의 docker 이미지에 가장 기본이 되는 이미지는 ubuntu가 아니라, alpine인 경우가 많음
    - alpine이란?
      - `musl libc`라는 임베디드 리눅스를 위한 C/POSIX library와
      - `BusyBox`라는 운영체제 운영에 필요한 가장 기본이 되는 유틸리티(시스템 프로그램)만 모아 놓은 리눅스 패키지
      - C/POSIX library
        - C 언어를 위한 기본 함수 및 POSIX 라는 표준 규격에 맞춘 기본 함수를 포함한 라이브러리

- http와 alpine
  - httpd도 태그 중에 alpine 기반 태그가 있음
    - https://hub.docker.com/_/httpd?tab=tags&page=1&ordering=last_updated
  - http:alpine 실행해보기

```shell
# 다른 옵션과 함께 httpd:alpine 태그 사용 예
docker run -d -p 80:80 -v "/home/ubuntu/2021_DEV_HTML":/usr/local/apache2htdocs --name apacheweb2 httpd:alpine
```



- 실행중인 컨테이너 사용 리소스 확인하기
  - 실행 중인 컨테이너의 **시스템 리소스 사용현황**을 확인할 수 있음

```shell
docker container stats
```



## 컨테이너를 다루는 다양한 옵션

- **컨테이너가 실행 중일 때에만 다음 명령을 실행할 수 있음**

```shell
docker exec [옵션] [컨테이너_ID] [명령 인자]
```

- 아래 명령 설명
  - `-it` : docker run에서 설명한 표준입력 (`-i`), 터미널(`-t`) 옵션이며, docker exec에서도 사용 가능
  - 다음과 같이 명령하면, `/bin/sh` 쉘 프로그램을 실행하면서, 터미널에 연결되므로, 컨테이너 안으로 들어갈 수 있음.
    - `/bin/bash`가 아닌 `/bin/sh`를 쓴 이유는 `/bin/bash`는 alpine 리눅스에 들어있지 않기 때문
    - alpine은 꼭 필요한 프로그램만 들어가 있다.

```shell
docker exec -it apacheweb /bin/sh
```



- **실행 중인 컨테이너에 연결하기**

```shell
# background로 실행
docker run -dit --name myubuntu ubuntu
```

```shell
docker attach myubuntu
```

> `exec`은 컨테이너에 신규 명령을 실행하는 명령이고, `attach`는 컨테이너에 연결하는 명령



- 모든 컨테이너 삭제하기 ( + 모든 docker 이미지 삭제하기)
  - 모든 컨테이너를 한번에 지우고 싶은 경우가 있으며, 다음과 같은 명령 조합으로 가능

```shell
# 모든 컨테이너 삭제를 위해, 우선 컨테이너를 모두 중지 시키고
docker stop $(docker ps -a -q)

# 모든 컨테이너 삭제
docker rm $(docker ps -a -q)
```

```shell
# 모든 docker 이미지 삭제
docker rmi $(docker images -q)
```

- for 복붙

```shell
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker rmi -f $(docker images -q)
```



- 별도로 다음과 같은 명령도 사용 가능 (많이 안쓰임)

```shell
docker container prune  # 정지된 컨테이너 삭제
docker image prune  # 실행 중인 컨테이너 image 외의 이미지 삭제
docker system prune  # 정지된 컨테이너, 실행 중인 컨테이너 이미지 외의 이미지, 볼륨, 네트워크 삭제
```



# Dockerfile

## 개념과 기본 문법

- 개념
  - docker 이미지를 작성할 수 있는 기능
  - Dockerfile 문법으로 이미지 생성을 위한 **스크립트**를 작성할 수 있고, 이를 기반으로 이미지를 생성
  - 배포를 위해서도 활용
- 기본 문법
  - `명령 + 인자`로 이루어짐
  - 명령은 통상적으로 대문자로 작성
  - 주석 사용 가능

## Dockerfile 주요 명령

| 명령       | 설명                                                         |
| ---------- | ------------------------------------------------------------ |
| FROM       | 베이스 이미지 지정 명령                                      |
| LABEL      | 버전 정보, 작성자 따위의 이미지 설명을 작성하기 위한 명령    |
| CMD        | docker 컨테이너가 시작할 때, 실행하는 쉘 명령을 지정하는 명령.<br />`RUN`과 비슷하지만, `RUN`은 이미지 작성 시 실행하는 명령.<br />`CMD`는 컨테이너를 시작할 때 실행하는 명령 |
| RUN        | shell 명령을 실행하는 명령 (예 : `RUN ["apt-get", 'install', 'nginx']`)<br />`RUN`은 이미지 작성시 실행되며, 새로운 이미지 layer를 만드는 역할을 함 |
| ENTRYPOINT | docker 컨테이너가 시작할 때, 실행하는 shell 명령을 지정하는 명령.<br />docker run 커맨드 실행시, 별도 명령어도 넣을 수 있는데, 이 때 `CMD` 명령은 해당 명령으로 덮어씌워짐<br />`ENTRYPOINT`로 지정한 명령은 docker run 커멘드 실행시 함께 넣어진 별도 명령어가 있더라도, 덮어씌워지지 않고 실행됨 |
| EXPOSE     | docker 컨테이너 외부에 오픈할 포트 설정 (예 : `EXPOSE 8080`) |
| ENV        | docker 컨테이너 내부에서 사용할 **환경변수** 지정 (예 : `ENV PATH /usr/bin:$PATH`) |
| WORKDIR    | docker 컨테이너에서의 작업 디렉토리 설정                     |
| COPY       | 파일 또는 디렉토리를 docker 컨테이너에 복사.<br />ADD와 달리 URL은 지정할 수 없으며, 압축 파일을 자동으로 풀어주지 않음 (예 : `COPY test.sh /root/test.sh`) |



### FROM

- 베이스 이미지 지정 명령
- 반드시 Dockerfile에 작성해야하는 명령

```dockerfile
# Dockerfile 파일명으로 다음과 같이 작성

# 경령화된 linux 시스
FROM alpine
```



### Dockerfile로 이미지를 작성 - build

```
docker build [옵션] [Dockerfile 경로]
```

- 주요 옵션

| 옵션              | 설명                                                         |
| ----------------- | ------------------------------------------------------------ |
| `-t` 또는 `--tag` | 이미지 이름 설정.<br />이미지 이름은 `저장소(DockerHub ID)/이미지이름:태그`와 같이 작성할 수 있음<br />저장소 이름 및 태그 이름은 작성하지 않아도 되며, 태그 이름이 없을 경우, 디폴트로 `latest`가 태그로 붙여짐 |
| `-f`              | 이미지 빌드시 디폴트로 `Dockerfile`파일명으로 된 파일을 찾아서, 이미지를 빌드함. <br />**그 외의 파일명으로 이미지를 빌드**할 경우 해당 옵션을 사용해서 **파일명을 지정**할 수 있음 |
| `--pull`          | FROM으로 지정된 이미지는 한번 다운로드 받으면, 이미지 생성시마다 새로 다운로드 받지 않고, 다운로드 받은 이미지를 사용함.<br />해당 옵션은 이미지 생성시마다 **새로 다운로드를 받으라**는 옵션.<br />`--pull=true`와 같이 작성하여, 사용함.<br />Dockerhub에 베이스 이미지를 수시로 업데이트하고, 이를 기반으로 새로운 이미지 생성시 자주 사용할 수 있는 옵션 |

- 테스트
  - 위에서 작성한 dockerfile이 있는 동일 경로에서 다음과 같이 명령
  - `--tag test`는 이미지 이름을 test로 설정한 것이므로, 디폴트 태그가 붙어서 `test:latest`로 작성됨
  - 마지막의 '`.`'는 현재 폴더를 나타내는 것이고, 즉 현재 폴더에 Dockerfile 파일이 있음을 의미함

```shell
docker build --tag test ./
```

- `f` 옵션 테스트

```shell
cp Dockerfile test_dockerfile
docker build --tag test2_image -f test_dockerfile .
docker images
```



### LABEL

- `<key>=<value>` 형식으로 메타 데이터를 넣을 수 있는 기능
- 보통 아래와 같은 정보를 넣음
  - 저자
  - 버전
  - 설명
  - 작성일자



### COPY

- Dockerfile 생성
  - 하부 폴더 2021_DEV 폴더에 이미지에 추가할 파일들을 넣어 놓은 상태에서 다음과 같이 Dockerfile 작성

```dockerfile
FROM httpd:alpine

LABEL maintainer="alphatechnicist@gmail.com"
LABEL version="1.0.0"
LABEL description="A test docker image to understand Docker"

# Dockerfile이 있는 그 위치 기준 상대경로
COPY ./2021_DEV /usr/local/apache2/htdocs
```



### CMD

- 다음 예에서 echo 명령만 달랑 써줄 경우, shell에서 실행하지 않고, 직접 해당 명령이 실행됨 
- shell에서 실행할 때, shell의 환경 변수등이 적용이 되지 않음
- 따라서, 정확하게는 명확히 shell까지 지정해서 명령을 실행해 주는 것이 좋다.
- `/bin/sh -c` 명령은 `/bin` 디렉토리에 있는 `sh` 프로그램 (기본 shell 프로그램)을 실행하되,
  - `-c` 옵션은 shell 명령을 터미널 상에서 받지 않고, 인자로 받겠다라는 의미임
  - 따라서, `/bin/sh -c echo`라고 하면, `echo`라는 명령을 `sh` 프로그램 상에서 실행하겠다라는 의미

- 쌍따옴표로 써야 함 (홀따옴표를 쓰면 안 됨)



- CMD 명령을 적는 3가지 형태

```dockerfile
# 1. 리스트에
CMD ["executable", "param1", "param2", ...]

CMD ["/bin/sh", "-c", "echo", "Hello"]

# 2. ENTRYPOINT 명령어에 인자를 리스트처럼 작성
CMD ["param1", "param2", ...]

# 3. shell 명령처럼 작성하는 형태
CMD <command> <param1> <param2> ...
```

>`CMD`는 하나의 Dockerfile에서 한 가지만 설정되며, 만약 `CMD` 설정이 여러 개일 경우, 맨 마지막에 설정된 `CMD` 설정만 적용됨.



- 가끔 사용하는 docker 명령1 : `logs`
  - 컨테이너 에러 또는 출력 결과 확인

```shell
docker logs [컨테이더ID 또는 이름]

# 예
docker logs httpdweb1
```

- 가끔 사용하는 docker 명령2 : `stop`, `kill`
  - 컨테이너 중지하기
  - `docker stop` : 현재 실행중인 단계까지는 기다린 후에 중지
  - `docker kill` : 즉시 컨테이너를 중지시킴



- base 이미지의 CMD를 덮어버리기

```dockerfile
FROM httpd:alpine

LABEL maintainer="alphatechnicist@gmail.com"
LABEL version="1.0.0"
LABEL description="A test docker image to understand Docker"

# Dockerfile이 있는 그 위치 기준 상대경로
COPY ./2021_DEV /usr/local/apache2/htdocs

CMD ["/bin/sh"]
```

```shell
# 이미지 생성
docker build --tag myimage .

# -dit 옵션으로 터미널 붙이고, 포트 오픈하고, 백그라운드 실행, 컨테이너 중지시 삭제
docker run -dit -p 9999:80 --name myweb2 --rm myimage
```

- 위와 같이 실행한 후, localhost:9999 접속시, 접속 실패



- Dockerfile의 CMD 명령을 shell 명령에서 덮어버리기

```shell
docker run -dit -p 9999:80 --name myweb2 --rm myimage /bin/sh -c httpd-foreground
```



### ENTRYPOINT

- `ENTRYPOINT`는 docker run 시에 함께 넣어지는 `CMD` 명령에 덮어씌워지지 않고, 반드시 실행해야 하는 명령을 기입할 때 사용
- 이 때, docker run 시 함께 넣어지는 명령은 `ENTRYPOINT`에 작성된 명령의 인자로 넣어지게 됨
- 따라서, `ENTRYPOINT`에 컨테이너 실행시 반드시 실행되어야 하는 명령을 넣고
  - 별도로 각 컨테이너 생성시 필요한 인자를 `CMD`에 넣는 식으로 활용하기도 함 

```dockerfile
FROM httpd:alpine

LABEL maintainer="alphatechnicist@gmail.com"
LABEL version="1.0.0"
LABEL description="A test docker image to understand Docker"

# Dockerfile이 있는 그 위치 기준 상대경로
COPY ./2021_DEV /usr/local/apache2/htdocs

ENTRYPOINT ["/bin/sh"]
```

```shell
# 이미지 생성
docker build --tag myimage .

# -dit 옵션으로 터미널 붙이고, 포트 오픈하고, 백그라운드 실행, 컨테이너 중지시 삭제
docker run -dit -p 9999:80 --name myweb2 --rm myimage
```



### RUN

- docker 는 이미지 생성시, 각 단계를 **layer**로 나누어 작성함
  - 이를 통해 특정 단계 변경시, 전체 이미지를 다시 다운로드 받지 않아도 됨
- RUN 명령은 이미지 생성시, 일종의 layer를 만들 수 있는 명령으로, 보통 베이스 이미지에 패키지(프로그램)을 설치하여, 새로운 이미지를 만들 때 많이 사용

```dockerfile
...

# 한국 시간으로 설정
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul
RUN apt-get install -y tzdata

RUN git clone -b be --single-branch https://github.com/POPPY-MAIL/dev.git

...

```



- test

```dockerfile
FROM ubuntu:18.04

LABEL maintainer="alphatechnicist@gmail.com"
LABEL version="1.0.0"
LABEL description="A test docker image"

RUN apt-get update
# apache2와 함께 apt-utils(설치관련 유틸리티를 가진 프로그램)도 설치
RUN apt-get install -y apache2 apt-utils

COPY ./2021_DEV_HTML /var/www/html/

ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

```shell
docker run -dit -p 9999:80 --name httpdweb5 --rm myweb4
```



### EXPOSE

- docker 컨테이너의 특정 포트를 외부에 오픈하는 설정
- docker run -p 옵션으로 설정할 수도 있음
  - docker run -p 옵션은 컨테이너의 특정 포트를 외부에 오픈하고, 해당 포트를 호스트 PC의 특정 포트와 매핑시킴
  - 이에 반해, `EXPOSE`는 컨테이너 생성시, 특정 포트를 외부에 오픈하는 것만 설정하는 것.
  - 따라서, 독립적으로 실행시는 `EXPOSE` 옵션을 넣는다고 해서, 호스트 PC에서 해당 컨테이너에 포트번호로 접속할 수 있는 것은 아님

### ENV

- 컨테이너 내의 환경 변수 설정
- 설정한 환경 변수는 RUN, CMD, ENTRYPOINT 명령에도 적용됨

```dockerfile
# 한국 시간으로 설정
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul
RUN apt-get install -y tzdata
```



### WORKDIR

- `RUN`, `CMD`, `ENTRYPOINT` 명령이 실행될 디렉토리

```dockerfile
WORKDIR /home/dev/BACKEND/

RUN pip install -r requirements.txt
```





# Docker 조사하기

## docker history

- 이미지 히스토리 확인
- 어떤 layer가 해당 이미지를 만드는 데 활용이 되었는지 확인할 수 있는 명령



## docker cp

- 컨테이너에서 특정 파일을 호스트 PC로 가져오는 명령
- 특정 파일 확인을 위해 활용할 수 있다.

```shell
docker cp [컨테이너이름]:/etc/apache2/sites-available/000-default.conf ./
```



- 반대로 호스트 PC에서 컨테이너에 특정 파일을 넣을 수도 있음

```shell
docker cp ./000-default.conf [컨테이너이름]:/etc/apache2/sites-available/000-default.conf
```



## docker commit

- 컨테이너 안에서 실행한 작업 내용을 layer로 추가하여 역으로 새로운 image를 만들 수 있다.
- 컨테이너 변경사항을 이미지 파일로 생성

```shell
# 컨테이너 내부에서 vim을 설치한 후에
docker commit -m "add vim" [변경사항이일어난컨테이너이름] [새로운이미지명]

# 변경사항 확인
docker history [새로운이미지명]
```



## docker diff

- 컨테이너가 실행되면서, **본래의 이미지와 비교**해서 변경된 파일 목록 출력

```shell
docker diff [컨테이너이름]
```



# docker link 실습

## docker로 jupyter notebook 띄우기

- 컨테이너 내부에서 jupyter notebook이 실행되는 폴더인 `/home/jovyan` 폴더를 호스트PC의 현재 폴더로 만듦
- host PC에서 docker를 실행하는 폴더에 있는 주피터 노트북 파일 작업이 가능하도록 함

```shell
docker run --rm -d -p 8888:8888 -v /home/ubuntu/2021_LEARN:/home/jovyan/work jupyter/datascience-notebook
```



- token을 입력하여 jupyter notebook 실행



## 컨테이너와 컨테이너 연결

- docker run 옵션으로 `--link` 옵션을 사용하여 연결
- `--link [본래 컨테이너 이름]:[컨테이너를 가리킬 이름]`

```dockerfile
FROM mysql:5.7

# mysql 슈퍼관리자인 root ID에 대한 password 란에 원하는 패스워드 설정
ENV MYSQL_ROOT_PASSWORD=password
ENV MYSQL_DATABASE=dbname
```

- 데이터베이스 컨테이너 생성

```shell
# docker 이미지 작성하기
docker build --tag mysqldb -f Dockerfile_MYSQL .

# 컨테이너 생성하기 3306 포트에 연결하고, volume 옵션 설정
docker run -d -p 3306:3306 --name mydb -v /home/ubuntu/mysqldata:/var/lib/mysql mysqldb
```

- `--link` 옵션을 사용해서 주피터 노트북 컨테이너 실행하기

```shell
# --link 컨테이너이름:연결할컨테이너를지칭할이름
docker run --rm -d -p 8888:8888 -v /home/ubuntu/2021_LEARN:/home/jovyan/work --link mydb:myupyterdb jupyter/datascience-notebook
```



