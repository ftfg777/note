 **Dockerfile이 필요한 이유**

#도커 

1. **환경 일관성 유지**

• 개발, 테스트, 운영 환경에서 동일한 환경을 제공함.

2. **배포 자동화**

• CI/CD와 연동하여 컨테이너 이미지를 쉽게 빌드하고 배포 가능.

3. **이동성 (Portability)**

• 한 번 빌드한 이미지를 어디서든 실행 가능 (로컬, 클라우드, 서버 등).

MSA 프로젝트에서 도커파일을 활용하면, 각 서비스별 독립적인 컨테이너 환경을 제공할 수 있음
예를 들어,
	- 스프링 부트 백엔드는 openjdk 이미지
	- 리액트 프론트엔드는 노드 이미지
	- 레디스, mysql등 데이터베이스도 도커파일을 활용해서 컨테이너로 실행 후 사용할 수 있음

---

**주요 명령어** **역할**

| WORKDIR    | 작업 디렉토리 설정                                  |
| ---------- | ------------------------------------------- |
| COPY       | 로컬 파일을 컨테이너로 복사                             |
| RUN        | 명령어 실행 (예: 패키지 설치)                          |
| CMD        | 컨테이너 실행 시 실행할 기본 명령어                        |
| ENTRYPOINT | CMD와 유사하지만 실행 가능한 기본 명령어를 고정                |
| EXPOSE     | 컨테이너에서 사용할 포트 지정 (실제 바인딩은 docker run -p 필요) |
| ENV        | 환경 변수 설정                                    |
| FROM       | 베이스 이미지 설정 (예: node:18-alpine)              |


---


도커 파일 (Gradle 환경 기준)
### 1. Gradle 빌드 환경을 위한 최신 이미지 (Gradle 8.10.2)  
FROM gradle:8.10.2-jdk17 AS build  
  
### 2. 프로젝트 파일을 컨테이너로 복사  
WORKDIR /app  
COPY . .  
  
### 3. Gradle을 사용하여 애플리케이션 빌드  
RUN gradle clean build --no-daemon  
  
### 4. 실행용 이미지를 위한 기본 OpenJDK 이미지  
FROM openjdk:17  
  
### 5. Gradle 빌드 결과물 JAR 파일을 실행용 이미지로 복사  
COPY --from=build /app/build/libs/*.jar app.jar  
  
### 6. 애플리케이션 실행  
ENTRYPOINT ["java", "-jar", "/app.jar"]

---


### 이미지 빌드 명령어
docker build -t user-service .
docker build -t order-service .


### 컨테이너 실행
docker run -p 8081:8081 user-service
docker run -p 8082:8082 order-service

### Docker Desktop Kubernetes에서 로컬 이미지 사용
docker build -t my-local-image .

yml 파일
containers: 
- name: my-container 
- image: my-local-image 
- imagePullPolicy: Never