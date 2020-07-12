FROM mariadb

RUN apt-get update && apt-get install -y cron
COPY backup-plan .

# TODO: backup-plan에 파이썬 스크립트 가져오고 아래 사이트 참고해서 cronjob 등록하기
# https://stackoverflow.com/questions/37458287/how-to-run-a-cron-job-inside-a-docker-container