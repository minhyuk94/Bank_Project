# Bank_Project


## 1. Go 설치
https://github.com/techschool/simplebank <br/>
https://dbdiagram.io/home <br/>
https://go.dev/tour/welcome/1 <br/>

### Go Install
```
https://go.dev/dl/

terminal 설치 경로 확인

go env GOPATH

경로 작성

vi ~/.bash_profile

=> export PATH=$PATH:$(go env GOPATH)/bin

현재 쉘에 로드

source ~/.bash_profile

go 파일 실행 명령어

=> go run main.go
```
## 2. Install Docker, Postgres, TablePlus
```
Docker

https://www.docker.com/

Postgres
=> docker pull postgres:12-alpine

docker run --name postgres12 -p 5432:5432 -e POSTGRES_USER=root -e POSTGRES_PASSWORD=secret -d postgres:12-alpine

docker exec -it postgres12 psql -U root

Postgres는 로컬에서는 기본적으로 신뢰 상태라서 비밀번호를 묻지않음.

docker logs postgres12


Tableplus
https://tableplus.com/

User : root

Password : secret

DB : root

db/init_schema.up.sql 을 통해 스키마 생성
```

## 3. migrate
```
migrate install

brew install golang-migrate
### migrate db
migrate create -ext sql -dir db/migration -seq init_schema

docker exec -it postgres12 /bin/sh

createdb --username=root --owner=root simple_bank

psql simple_bank
### Access db
docker exec -it postgres12 psql -U root simple_bank

### Makefile
makefile 명령어를 통해 간단히 실행 가능
```

## 4. Go lang CRUD
```
https://gorm.io/docs

Install sqlc
https://github.com/sqlc-dev/sqlc

brew install sqlc

1)db 디렉토리에 query, sqlc 디렉토리 생성
2)query디렉토리에 각종 sql파일 작성
3)make sqlc 를 통해서 sqlc디렉토리에 db의 go파일이 생성됨
생성된 파일은 아직 모듈초기화를 하지 않아 빨간줄로 표시될거임

모듈초기화
go mod init github.com/techschool/simplebank

주의사항
생성된 파일들을 수정하면 안되고 query디렉토리에서 만든 sql파일을 수정 후 make sqlc를 통해 다시 생성하는것

account.sql파일 작성 후 make sqlc를 통해 계정테이블에 대한 전체 crud를 생성가능
https://docs.sqlc.dev/en/latest/howto/update.html
```
