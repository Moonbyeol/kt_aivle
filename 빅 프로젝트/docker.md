
# 1. 이미지 빌드
```
docker build -t {이미지 이름} .
```

# 2. 실행
```
docker run --name {띄울 컨테이너 이름} -d -p {외부 포트}:{컨테이너 내부 포트} {띄울 이미지 이름}

docker run --name logo -d -p 8080:8080 aimodel
```

# Dockerfile
```docker
# 베이스 이미지 설정
FROM python:3.11-slim

# 작업 디렉토리 설정(docker에서 app이라는 디렉터리를 만듦)
WORKDIR /app

# 종속성 파일 복사 및 설치
# app에 requrements txt를 ./ (즉, app 디렉터리에 복사)
COPY requirements.txt ./

# pip 업그레이드
RUN pip install --upgrade pip

# 파이썬 종속성 설치, requirements 다운로드
RUN pip install -r requirements.txt

# 나머지 애플리케이션 코드 복사
# 현재 작업 파일 기준 ./app에 있는 파일들을 도커의 /app 디렉터리에 복사
COPY ./app /app

# 8080포트로 실행
EXPOSE 8080

# 실행 명령어 0.0.0.0으로 하지 않으면 127.0.0.1로 실행되기 때문에 설정
CMD ["uvicorn", "server:app", "--host", "0.0.0.0", "--port", "8080"]

```

## 도커 명령어

### 로컬에서 주로 사용

- 도커 로그인
    - docker login
- 이미지 생성
    - docker build -t namhyong/kt5bigproject14:latest .
    - docker build -t <사용자이름>/<레포지토리>:<태그>
    - 로컬에 저장된 이미지를 태그라는 이름으로 만듦
- 이미지 푸쉬
    - docker push namhyong/kt5bigproject14:latest
    - docker push <사용자이름>/<레포지토리>:<태그>
    - 위에서 생성한 태그를(이미지를) 도커허브의 레포지토리에 푸쉬

---

### EC2 에서 주로 사용

- 이미지 pull
    - docker pull namhyong/kt5bigproject14:latest
    - docker pull <사용자이름>/<레포지토리>:<태그>
    - ec2에서 docker hub의 이미지를 태그이름으로 찾아 pull
- 도커 이미지 확인
    - docker images
- 도커 컨테이너 실행
    - docker run -d -p 8000:8000 <이미지 이름>
- 실행중인 컨테이너 확인
    - docker ps
    - docker ps -a(컨테이너 목록 보기)
- 앱 실행시 로그 보기
    - docker logs <실행중인 컨테이너에서 확인한 container id>
- 도커 컨테이너 중지
    - docker stop <실행중인 컨테이너에서 확인한 container id>
- 도커 컨테이너 삭제
    - docker rm <실행중인 컨테이너에서 확인한 container id>
- alembic 초기화 설정
    - docker-compose exec <container_name> alembic init alembic
- alembic migration 스크립트 사용
    - docker-compose exec <container_name> alembic revision --autogenerate -m "Initial migration"
    - docker-compose exec <container_name> alembic upgrade head

## docker-compose

- 여러 도커 컨테이너를 한 번에 관리하기 위해 사용

```docker
version: '3.8'

services:
# app 환경 설정
  app:
    build:
      context: .
      dockerfile: Dockerfile
    image: namhyong/langchain:latest
    container_name: langchain
    ports:
      - "8080:8080"
    depends_on:
      - redis
    environment:
      - REDIS_HOST=54.181.1.215
      - REDIS_PORT=6379
    command: >
      sh -c "uvicorn server:app --host 0.0.0.0 --port 8080"
# redis 환경 설정 
  redis:
    image: redis:latest
    container_name: redis
    ports:
      - "6379:6379"
```

### 명령어

- 도커 컴포즈 설치
    
    ```bash
    # 설치
    $ sudo curl -SL "<https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-$>(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    
    # 권한 부여
    sudo chmod +x /usr/local/bin/docker-compose
    
    # 심볼릭 링크 지정
    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
    
    # docker-compose 버전 확인
    docker-compose --version
    ```
    
- 도커 컴포즈 빌드
    
    - docker-compose build
- 도커 컴포즈 실행
    
    - docker-compose up
    - docker-compose up -d (백그라운드 실행)
- 도커 컴포즈 중지
    
    - docker-compose down
- 실행중인 서비스 확인
    
    - docker-compose ps
- 도커 컴포즈 이미지 다운
    
    - docker-compose pull

---

## mysql

1. mysql 설치 후 mysql 설정 파일 수정
    
    1. `sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`
2. bind-address 설정 확인하기
    
    ```docker
    # 모든 ip에서 접근을 허용하기 위해서 사용
    [mysqld]
    bind-address = 0.0.0.0
    ```
    
3. mysql-server 재시작
    
    1. `sudo systemctl restart mysql`
4. mysql-server 유저 생성
    
    1. `mysql -u root -p`로 mysql 접속
    2. 비밀번호 입력
    3. `CREATE USER 'root'@'%' IDENTIFIED BY 'aivle';`
5. 권한 부여
    
    1. `GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;`
    2. `FLUSH PRIVILEGES;`

## 참고

[AWS EC2 rm -rf anaconda3 삭제하기](https://parksrazor.tistory.com/473)




# 안쓰는 이미지 컨테이너 삭제 코드

```
docker system prune
```

