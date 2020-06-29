# docker-redmine
docker-compose.yml 을 이용한 redmine 서비스 구축

## You need this
* Docker Desktop  
* Docker Compose  

Official Web Site: [Docker Web Site](https://www.docker.com/products/docker-desktop)

## How to set up 
현재 프로젝트를 ~(HOME) 디렉터리 아래 설치한 것으로 간주한다.

### 환경변수 설정
.env 파일에서 주석을 참고하여 각 환경 변수들을 지정

## Execute
### docker-compose 실행
실행 주의
> docker-compose up 처음 실행 시에 레드마인이 재대로 동작하지 않는다: redmine 컨테이너보다 db 컨테이너가 먼저 실행되도록 설정이 필요하다.   
> 차후에 추가 예정.

```bash
# 현재 프로젝트의 디렉터리로 이동
cd ~/docker-redmine
# docker-compose 데몬으로 실행
docker-compose up -d
```   

### docker-compose로 실행한 Container 및 Network 삭제
```bash
docker-compose down
```

## Confirm
### Docker Container 확인
```bash
docker ps
```

### MariaDB User 확인
```bash
# maraidb 컨테이너의 bash 쉘 접속
docker exec -it mariadb /bin/bash
mysql -uroot -p

MariaDB [(none)]> use mysql
MariaDB [mysql]> select user, host from user;
# 결과 
+-------------+-----------+
| User        | Host      |
+-------------+-----------+
| redmine     | %         |
| root        | %         |
| mariadb.sys | localhost |
| root        | localhost |
+-------------+-----------+
```

### MariaDB 에 문제 발생 시 대처: 주의) 상용으로 이미 사용하는 있는 경우에는 따라하지 말 것!)
테스트를 위해 docker-compose.yml 파일을 수정하지 않고 실행하고 나서 컨테이너를 모두 종료 및 삭제 후 
docker-compose.yml 파일을 수정하고 다시 실행 했을 때 원하는 결과가 나오지 않을 수 있다. 
필자의 Case: DB User로 'redmine'은 없고 root만 존재하도록 컨테이너를 띄웠다가 docker-compose.yml 파일에 MYSQL_USER로 'redmine'을
추가하였으나 User에 'redmine'이 추가되지 않고 계속해서 root만 존재하는 상황이 발생

그 이유는 docker-compose.yml 파일에서 MariaDB의 Volume을 Host PC 에 존재하는 디렉터리(${MARIADB_STORAGE_DIR_PATH}:/var/lib/mysql)
와 연결하였기 때문이다.
Docker 컨테이너를 삭제 후 다시 띄운다고 해도 Host PC의 볼륨에 파일이 존재한다면 파일을 새로 생성하지 않고 기존에 있던 파일을 사용하기 때문에 
docker-compose.yml 에서 변경한 점이 반영되지 않을 수 있다. .env 파일에서 MARIADB_STORAGE_DIR_PATH 위치를 파악한 이후
해당 디렉터리(~/docker-redmine/mariadb/data)를 삭제 이후 `docker-compose up`으로 다시 실행하면 변경점이 반영된 것을 확인할 수 있다.

해당 문제는 Volume 맵핑 시에 데이터 뿐만 아닌 시스템 설정 값을 포함한 디렉터리인 '/var/lib/mysql' 을 맵핑하였기 때문이다.
Volume 맵핑 시에는 시스템 값을 가지고 있는 디렉터리는 피하기를 권장한다.


## Start Redmine!
### URL
웹 브라우저에서 `localhost:3000` 으로 접속

### admin 계정
처음 접속시 admin 계정 정보(ID/PW): admin/admin

### 버전 확인
좌측 최상단 메뉴에서 '관리' -> 정보

## Backup


## Restore