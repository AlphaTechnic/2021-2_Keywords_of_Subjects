>**강의명** : **풀스택을 위한 도커와 최신 서버 기술(리눅스, nginx, AWS, HTTPS, flask 배포) [풀스택 Part3]**
>
>https://www.inflearn.com/course/%EC%84%9C%EB%B2%84%EA%B8%B0%EC%88%A0-%ED%92%80%EC%8A%A4%ED%83%9D-3

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

