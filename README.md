# Bank_Project


## 1. Go 설치
https://github.com/techschool/simplebank <br/>
https://dbdiagram.io/home <br/>
https://go.dev/tour/welcome/1 <br/>

### Go Install
https://go.dev/dl/

-- terminal
설치 경로 확인
go env GOPATH

경로 작성
vi ~/.bash_profile

=> export PATH=$PATH:$(go env GOPATH)/bin
현재 쉘에 로드
source ~/.bash_profile

go 파일 실행 명령어
=> go run main.go

## 2. Install Docker, Postgres, TablePlus
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


## 3. migrate
migrate install

brew install golang-migrate
---
migrate db

migrate create -ext sql -dir db/migration -seq init_schema

docker exec -it postgres12 /bin/sh

createdb --username=root --owner=root simple_bank

psql simple_bank
---
Access db

docker exec -it postgres12 psql -U root simple_bank
---

migrate -path db/migration -database "postgresql://root:secret@localhost:5432/simple_bank?sslmode=disable" -verbose up




