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
현재 프로젝트를 /home 아래 설치한 것으로 간주한다.

### docker-compose 실행
```bash
# 현재 프로젝트의 디렉터리로 이동
cd /home/docker-redmine
# run docker-compose
docker-compose up
```   

## Confirm
```bash
docker ps

```