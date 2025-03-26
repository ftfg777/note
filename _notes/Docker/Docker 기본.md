#도커

````markdown
# 실무에서 자주 사용하는 도커 명령어 및 활용법

## 🚀 도커란 무엇인가?

도커(Docker)는 컨테이너(Container) 기반의 가상화 기술을 제공하는 오픈소스 플랫폼으로, 배포 및 운영 환경을 쉽게 관리할 수 있도록 해줍니다. 실무에서는 개발 환경 구성, CI/CD 파이프라인 구축, 마이크로서비스 아키텍처 운영 등에 활용됩니다.

## 📌 실무에서 자주 사용하는 도커 명령어

### 1️⃣ 컨테이너 실행 및 관리
```sh
docker run -d --name my-app -p 8080:80 nginx
````

- `-d`: 백그라운드에서 실행
- `--name my-app`: 컨테이너 이름 지정
- `-p 8080:80`: 로컬 8080 포트를 컨테이너 80 포트와 매핑

### 2️⃣ 실행 중인 컨테이너 목록 확인

```sh
docker ps
```

### 3️⃣ 모든 컨테이너 확인 (종료된 컨테이너 포함)

```sh
docker ps -a
```

### 4️⃣ 컨테이너 중지 및 삭제

```sh
docker stop my-app
docker rm my-app
```

## 📦 실무에서 자주 쓰는 Dockerfile 예제 (Spring Boot + Gradle)

```dockerfile
# OpenJDK 17 기반 이미지 사용
FROM openjdk:17-jdk-slim

# 작업 디렉토리 설정
WORKDIR /app

# Gradle 빌드 결과물 복사
COPY build/libs/my-app.jar app.jar

# 컨테이너 실행 시 실행할 명령어
CMD ["java", "-jar", "app.jar"]
```

### 도커 이미지 빌드 및 실행

```sh
./gradlew build

docker build -t my-springboot-app .
docker run -d -p 8080:8080 my-springboot-app
```

## 📌 도커 컴포즈(Docker Compose) 활용 (Spring Boot + MySQL)

실무에서는 다중 컨테이너 환경을 쉽게 관리하기 위해 `docker-compose.yml`을 사용합니다.

### 🔹 `docker-compose.yml` 예제

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://db:3306/mydb
      SPRING_DATASOURCE_USERNAME: user
      SPRING_DATASOURCE_PASSWORD: password
    depends_on:
      - db
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: mydb
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    ports:
      - "3306:3306"
```

### 🔹 실행하기

```sh
docker-compose up -d
```

## 🎯 실무에서 활용하는 도커 패턴

- **CI/CD 파이프라인에서 활용**: GitHub Actions, Jenkins와 연계하여 배포 자동화
- **마이크로서비스 운영**: Kubernetes와 함께 확장 가능하게 서비스 관리
- **로컬 개발 환경 구성**: 로컬에서 동일한 환경을 유지하며 개발 가능

📖 더 자세한 내용은 [공식 도커 문서](https://docs.docker.com/)를 참고하세요!