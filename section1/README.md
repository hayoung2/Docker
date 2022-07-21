# Section 1: what is Docker ? 

------

### 	📝 목차  

​         - Docker란 ? 

​         - [Window] Docker 설치

​         - Docker 실습

## Docker 🐳 

### **Container와 Docker?**

> Container : 표준화된 소프트웨어 유닛 | 코드가 포함된 패키지 | 코드를 실행하는 종속성 보관 
>
> Docker : 컨테이너를 사용하여 응용 프로그램을 쉽게 생성 ,배포, 실행 할 수 있게 하는 도구이다. 응용 프로그램과 해당 종속성을 컨테이너 내에 [바인딩]([언어 바인딩 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)](https://ko.wikipedia.org/wiki/언어_바인딩))함.

​	

#### **왜 Docker를 사용해야하는가 ?**

​    : 예를 들어, A 컴퓨터는 Node 14.5 version , B 컴퓨터는 Node 12.4 version이 설치되어 있다.  A 컴퓨터와 B 컴퓨터가 동일하게 코드 를 작성했더라도  version에 의한 오류가 발생할 수 있다. 이러한 오류로 인해 소모되는 비용과 시간을 없애기위해 바로 'Docker' 가 필요하다.   

#### **Docker의 장점?**

​	: 항상 동일한 버전으로 코드를 진행시킨다.  예를 들어 A 와 B 가 서로 협력해서 프로젝트를 할 경우, 서로의 컴퓨터를 동일한 환경으로 맞추는데 시간이 많이 사용될 것이다. 개개인이 아니라  기업 내에서 대규모 프로젝트를 진행한다면 더 큰 문제가 발생한다.  위와 같은 내용이지만, 더 큰 프로젝트가 될 수록 사용되는 시간과 소모되는 비용 Docker를 사용하여 항상 동일한 환경에서 프로젝트를 진행하게 한다.   

#### **Docker vs VM(Veritual Merchine)**

​	: [VM](https://www.ibm.com/kr-ko/cloud/learn/virtual-machines)은 기존 OS 위에 가상머신을 설치한다(= [stand-alone computer](https://www.pcmag.com/encyclopedia/term/stand-alone-pc)).  VM 같은 경우,  분리된 환경과 환경별 구성을 가질 수 있으며 안정적인 것이 장점이다.   하지만 매번 새로운 컴퓨터를 내부에 설치함으로써 공간이 낭비(Ex. 메모리, CPU, 하드 드라이브)  되거나 성능이 저하되는 단점이 발생한다.  아래 그림을 보면 Docker는  하나의 머신에 여러 대의 머신을 설치하지 않지만,  여러개의 컨테이너로 구성되며 Docker를 기반으로 컨테이너가 실행된다.  Docker는 VM에 비해 매우 가볍고 빠르며 최소한의 디스크 공간을 사용하고  컨테이너를 공유, 재구축 및 배포하는 것에 매우 용이하다. 



![Traditional vs New Gen](https://geekflare.com/cdn-cgi/image/width=796,height=342,fit=crop,quality=80,format=auto,onerror=redirect,metadata=none/wp-content/uploads/2019/09/traditional-vs-new-gen.png)





##  [[Window] Docker 설치](https://docs.docker.com/desktop/install/windows-install/) 🔨

#### WSL(windows subsystem for Linux) 이란 ?

​    : Linux용 Windows 하위 시스템. WSL 을 설치함으로써 개발자가 따로 기존 가상 머신의 오버헤드 or  듀얼 부팅 설정이 필요없다.  GNU/Linux 환경을 수정없이 Windows에서 직접 실행 가능하게 하는 것이 바로 WSL이다.

- window 10 home -> WSL2 설치 필요 

- window 10 pro, education, 11 ~ -> WSL 별도 설치 필요 X 

  

## 💻Docker 실습

​	**- <span style="background-color:#ffdce9">실습 예제</span>**

```dockerfile
# 컨테이너 이미지 설정 
FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000 # 통신 port

CMD ["node","app.mjs"]

# docker build : Dockerfile 기반으로 이미지 빌드
# docker run -p 3000:3000 [이미지 ID]: 도커 실행
# -p 포트 설정 
# docker ps : 실행 중인 모든 컨테이너 나열 
# docker stop [할당된 컨테이너 이름] : 컨테이너 실행종료
```

###### 	 *DockerFile :  Docker 이미지생성 프로세스를 자동화하는 파일. 



​	**<b>- <span style="background-color:#ffdce9">실습 결과</span></b>**

<img src="C:\Users\dudgk\Desktop\캡처.PNG" alt="실습 예제 스크린샷" style="zoom:150%;" /> 



------

#### 참조 및 추가 자료

*[Docker란 무엇입니까? | AWS (amazon.com)](https://aws.amazon.com/ko/docker/)

*[Docker vs Virtual Machine (VM) - Understanding the Differences (geekflare.com)](https://geekflare.com/docker-vs-virtual-machine/) 

*[What is a Container? - Docker](https://www.docker.com/resources/what-container/) 

*[What is Docker? | IBM](https://www.ibm.com/cloud/learn/docker)

