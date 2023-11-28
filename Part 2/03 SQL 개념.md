## SQL

SQL이란 Structured Query Language의 약자로, '구조화된 질의 언어'라는 뜻입니다. 현업에서는 관계형 데이터베이스 관리 시스템(RDBMS)의 표준 언어로 널리 사용되며, 데이터베이스의 구조를 정의하는 DDL(Data Definition Language), 데이터를 조작하는 DML(Data Manipulation Language), 그리고 데이터의 보안과 통제를 위한 VDL(View Definition Language) 등을 포함하는 종합적인 데이터베이스 언어라고 할 수 있습니다.

### SQL 주요 용어

SQL을 이해하기 위해서는 몇 가지 주요 용어를 알아야 합니다. 우선, 관계형 데이터 모델에서 '관계(Relation)'는 SQL에서 '테이블(Table)'이라는 개념으로 대응됩니다. 그리고 '속성(Attribute)'은 '열(Column)', '튜플(Tuple)'은 '행(Row)', '도메인(Domain)'은 SQL에서도 동일하게 '도메인(Domain)'으로 사용됩니다.

### SQL에서 Relation이란?

SQL에서 'Relation'은 '테이블'이란 개념으로 이해할 수 있습니다. 이는 SQL에서 튜플의 '멀티셋(Multiset)' 또는 '백(Bag)'으로 표현되며, 중복된 튜플을 허용합니다. 즉, SQL의 테이블은 같은 형태와 데이터를 가진 행이 여러 개 존재할 수 있다는 것을 의미합니다.

### SQL & RDBMS

SQL은 RDBMS의 표준 언어이지만, 실제로는 각 RDBMS 제품마다 제공하는 SQL의 스펙이 조금씩 다르다는 점을 알아두어야 합니다. 이는 SQL 표준을 모든 RDBMS가 완벽하게 지키는 것이 아니라, 각각의 시스템이 특정 기능을 추가하거나, 일부 기능을 생략하거나, 또는 동일한 기능을 조금 다른 방식으로 구현하기 때문입니다. 예를 들어, MySQL, Oracle 등의 RDBMS는 각각 고유의 SQL 구문과 기능을 제공합니다. 이 때문에 특정 RDBMS에 익숙해진 개발자가 다른 RDBMS를 사용하려고 할 때는 해당 시스템의 SQL 스펙을 따로 학습해야 할 필요가 종종 있습니다.

## Database와 Table 만들기

데이터베이스와 테이블을 만드는 과정을 알아보겠습니다. SQL을 통해 이 과정을 진행하면서 필요한 명령어들을 하나씩 살펴봅시다.

### 데이터베이스 생성

데이터베이스를 생성하는 방법은 매우 간단합니다. `CREATE DATABASE` 뒤에 생성하고자 하는 데이터베이스의 이름을 적어주면 됩니다. 예를 들어, `company`라는 이름의 데이터베이스를 생성하고자 한다면 다음과 같이 명령합니다.

```sql
CREATE DATABASE company;
```

### 데이터베이스 리스트 확인

생성된 데이터베이스가 잘 있는지, 혹은 어떤 데이터베이스들이 존재하는지 확인하려면 `SHOW DATABASES;`를 사용하면 됩니다.

```sql
SHOW DATABASES;
```

### 사용 중인 데이터베이스 확인(지금 선택된 데이터베이스 확인)

현재 어떤 데이터베이스를 사용 중인지 확인하려면 `SELECT database();`를 사용합니다. 이 명령은 현재 선택된 데이터베이스를 반환합니다.

```sql
SELECT database();
```

### 사용할 데이터베이스 선택

작업하려는 데이터베이스를 선택하려면 `USE` 명령을 사용하면 됩니다. 예를 들어, `company` 데이터베이스를 사용하려면 다음과 같이 명령합니다.

```sql
USE company;
```

### 데이터베이스 삭제

데이터베이스를 삭제하려면 `DROP DATABASE` 뒤에 삭제하려는 데이터베이스의 이름을 적어주면 됩니다. 예를 들어, `company` 데이터베이스를 삭제하려면 다음과 같이 명령합니다.

```sql
DROP DATABASE company;
```

### 테이블 생성

테이블을 생성하려면 `CREATE TABLE` 명령을 사용합니다. 테이블 이름 뒤에 괄호 안에 각 열(Column)의 이름과 데이터 형식, 그리고 필요한 제약 조건을 적어주면 됩니다. 예를 들어 `DEPARTMENT`라는 테이블에는 `id`, `name`, `leader_id`라는 열이 있고, 각각 정수형, 문자열, 정수형 데이터를 가집니다. `id`는 기본 키(PRIMARY KEY)로 설정되고, `name`은 NULL 값을 허용하지 않으며 유일해야 합니다.

```sql
CREATE TABLE DEPARTMENT (
    id INT PRIMARY KEY,
    name VARCHAR(20) NOT NULL UNIQUE,
    leader_id INT
);
```

### 테이블 삭제

테이블을 삭제하려면 `DROP TABLE` 뒤에 삭제하려는 테이블의 이름을 적어주면 됩니다. 예를 들어, `DEPARTMENT` 테이블을 삭제하려면 다음과 같이 명령합니다.

```sql
DROP TABLE DEPARTMENT;
```

### Database vs Schema

MySQL에서는 Database와 Schema가 같은 뜻으로 사용됩니다. 즉, `CREATE DATABASE company;`와 `CREATE SCHEMA company;`는 동일한 명령입니다. 그러나 다른 RDBMS에서는 Schema의 의미가 다르게 해석될 수 있습니다.

예를 들어, PostgreSQL에서는 Schema가 Database의 namespace를 의미하며, Database 안에 Schema가 정의되고, 그 안에 Table이 정의됩니다. 반면 MySQL에서는 Database 안에서 직접 Table이 정의됩니다. 이처럼 RDBMS에 따라 Database와 Schema의 관계와 정의가 다르므로, 사용하는 시스템의 특징과 문서를 잘 이해하고 활용해야 합니다.

## Attribute Data Type

데이터베이스에서는 다양한 데이터 유형을 다룰 수 있습니다. 이러한 데이터 유형을 이해하고 올바르게 사용하는 것이 중요합니다. SQL에서는 다양한 데이터 유형을 제공하며, 대표적인 유형에 대해 살펴보겠습니다.

### 숫자

