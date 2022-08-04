# Section2 : Image

### 📝 목차

	 - Image 란 ?
	 - 레이어 기반 아키텍처 ?
	 - Docker 실습 



## Image

#### Image ?

>  읽기/쓰기 액세스 권한이 있는 인스턴스를 실행하는 컨테이너의 '블루프린트'  
>
>  모든 설정 명령과 모든 코드가 포함된 공유 가능한 패키지이며 실제로 코드와 코드를 실행하는데 필요한 도구 이미지를 통해 여러 컨테이너 생성 가능하다 .  이미지는 읽기 전용이며, 한번 빌드되면 변경되지 않는다 -> 단순하게 코드를 업데이트해서 외부에서 변경하지 못하기때문에 다시 빌드해야 한다. 빌드 했을 경우, 완전 새로운 이미지이고, 닫힌 템플릿이다. 
>
> 외부 이미지 ? : Docker Hub( EX. node docker image)



#### layer ?

> 시스템을 생성, 배포, 확장하기 위한 기본 구성 요소이다.  레이어는 이미지를 구성하는 것으로 이미지를 빌드할 때 플랫폼은 파일의 각 명령에 대해 새   로운 Layer를 만든다. 



### Layered Architecture

> 각 계층은 어플리케이션 내에서의 특정 역할과 관심사(화면표시, 비즈니스 로직 수행 등 )별로 구분된다(Separation of Concern)
>
> 최종 명령 이전의 모든 명령은 이미 이미지의 일부이지만 별도의 레이어이다. 아무것도 변경 안되면 캐시를 사용하고, 하나의 레이어라도 변경되면 모든 후속 레이어도 다시 실행된다
>
> 이미지를 빌드할 때마다, 도커는 모든 명령 결과를 캐시하고 이미지를 빌드하고 변경된 것이 없으면 캐시된 결과를 사용.  레이어 기반 아키텍처 
>
> Using cache : 도커는 기본적으로 이 명령어가 이전과 동일하다고 인식하면 거칠필요가 없다고 추론함..





## 💻Docker 실습

 **- 실습 예제**

```dockerfile
FROM node # 노드 이미지 구축 


COPY package.json /app  # app 폴더에 복사해서 소스코드를 복사하기 전에 사용하여 npm install 되는 것을 막음
# npm install 이 계속해서 실행되는 것은 너무 비효율적이니까 성능이 더 좋아짐. 
RUN npm install # RUN은 이미지에 명령 
#Run node server.js # 모든 거 완료되면 서버 실행 

# 이 아래 레이어들만 실행 
COPY . /app# 두 개의 경로 지정, 첫번째는 컨테이너의 외부, 이미지의 외부 경로(이미지로 복사되어야 할 파일들이 있는 곳 )
# . 이 있음ㄴ 이는 도커에게 기본적으로 Dockerfile이 포함된 동일한 폴더를 복사해야한다고 Docker에게 알림 , Dockerfile은 제외 
# 두번째 . 은 그 파일을 저장해야 하는 이미지 내부의 경로. 
# if COPY . /app , -> Dockerfile에 모든 파일과 모든 하위 폴더가 컨테이너 내부의 /app 폴더에 복사됨. 폴더가 존재하지 않는다면, 이미지와 컨테이너에 생성 

EXPOSE 80
# 컨테이너가 시작될 때, 특정 포트를 노출하기 위해 설정 80
# 컨테이너 프로세스가 이 포트를 노출할 것임을 문서화 하는 것 
# 이 명령어를 안 쓴다면 docker run -p 80 ID 이런 식으로 포트 설정 

CMD ["node","server.js "] # 도커에게 이미지를 기반으로 컨테이너가 생성될 때마다 
# 컨테이너 내부에 node 명령을 사용해서 server.js 실행하라 뜻 
# CMD를 설정해주지않으면 base 이미지 시행 없는 경우, 에러 

docker build .# Dockerfile의 명령으로 이미지 만듦
# . 은 Dockerfile 위치가 동일한 파일에 존재하는 걸 알려줌

docker run 이미지 ID

docker run node # docker hub에 있는 공식적으로 노드 이미지를 가져와서  컨테이너를 만들어 실행하는 것 

#docker ps(프로세스) -a(도커가 생성한 모든[all] 컨테이너 프로세스 표시)

docker run -it node 
#(도커에게 컨테이너 내부에서 호스팅 머신으로 대화형 세션을 노출하고 싶다 -> 실제 노드 명령어 사용 가능 ) 노드가 생성된 컨테이너 내부에서 실행 가능
```



#### 참고자료 및 출처

[계층화 아키텍처 (Layered Architecture) (hudi.blog)](https://hudi.blog/layered-architecture/)

[What Are Docker Image Layers? | Packagecloud Blog](https://blog.packagecloud.io/what-are-docker-image-layers/#:~:text=Docker Layer Overview Docker is a containerization platform,in the kernels to run multiple isolated containers.)

