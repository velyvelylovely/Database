## (Windows) MariaDB 설치 및 환경 설정
>[!NOTE]
> 경로 : \mariadb-10.6.15\bin
>
> MariaDB 설치 시스템 유틸리티에 대한 도움말 정보 확인
```bash
mariadb-install-db --help
```

>[!NOTE]
>명령 프롬프트 관리자 권한으로 실행

```bash
mariadb-install-db -S {서비스 이름을 지정} -p {비밀번호}
```
- mariadb-install-db : MariaDB를 초기화하고 데이터베이스를 생성
- -S : MariaDB 서버를 Windows 서비스로 설치하고, 그 서비스의 이름을 지정하기 위해 사용되는 옵션
- -p : root 사용자의 비밀번호를 설정하기 위해 사용되는 옵션

## 서비스 관리 명령어

>[!NOTE]
> Windows 서비스로 데이터베이스 서버를 등록하면 다음과 같은 명령어로 데이터베이스를 실행할 수 있음

#### 서비스 시작

```bash
sc start {서비스 이름}
```

#### 서비스 중지

```bash
sc stop {서비스 이름}
```

#### 서비스의 상태 정보 조회

```bash
sc query {서비스 이름}
```

## 데이터베이스 접속

```bash
mysql -u root -p
```

- mysql : MySQL 클라이언트 프로그램을 실행하는 명령어
- -u : 사용자 이름 지정
- -p : 비밀번호를 통해 접속

## SQL 쿼리

#### 현재 MySQL 서버의 버전 정보 확인
```mysql
select version();
```

#### 현재 MySQL 서버에 존재하는 모든 데이터베이스의 목록 반환
```mysql
show databases;
```

#### 현재 작업할 데이터베이스 선택

```mysql
use {데이터베이스 이름}
```

#### 현재 선택한 데이터베이스 내에 있는 모든 테이블의 이름 반환

```mysql
show tables;
```
