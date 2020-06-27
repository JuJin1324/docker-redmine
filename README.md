# docker-redmine
docker-compose.yml 을 이용한 redmine 서비스 구축

## You need this
* Docker Desktop  
* Docker Compose  

Official Web Site: [Docker Web Site](https://www.docker.com/products/docker-desktop)

## How to set up 
현재 프로젝트를 /home 아래 설치한 것으로 간주한다.

### 환경변수 설정
.env 파일에서 주석을 참고하여 각 환경 변수들을 지정

## Execute
현재 프로젝트를 (~)HOME 디렉터리 아래 설치한 것으로 간주한다.

### docker-compose 실행
```bash
# 현재 프로젝트의 디렉터리로 이동
cd ~/docker-redmine
# docker-compose 데몬으로 실행
docker-compose up -d
```   

## Confirm
```bash
docker ps

```

## Start Redmine!
### URL
웹 브라우저에서 `localhost:3000` 으로 접속

### admin 계정
처음 접속시 admin 계정 정보(ID/PW): admin/admin

