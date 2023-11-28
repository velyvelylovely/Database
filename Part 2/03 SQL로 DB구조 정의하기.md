## [SQL](https://www.youtube.com/watch?v=c8WNbcxkRhY&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=4)

SQL이란 Structured Query Language의 약자로, '구조화된 질의 언어'라는 뜻입니다. 현업에서는 관계형 데이터베이스 관리 시스템(RDBMS)의 표준 언어로 널리 사용되며, 데이터베이스의 구조를 정의하는 DDL(Data Definition Language), 데이터를 조작하는 DML(Data Manipulation Language), 그리고 데이터의 보안과 통제를 위한 VDL(View Definition Language) 등을 포함하는 종합적인 데이터베이스 언어라고 할 수 있습니다.

### SQL 주요 용어

| Relational Data Model | SQL |
| --- | --- |
| Relation | Table |
| Attribute | Column |
| Tuple | Row |
| Domain | Domain |

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

![image](https://github.com/velyvelylovely/Database/assets/98696925/f462c31f-9bd2-438c-ba42-d9ca406b52da)

### 문자열

![image](https://github.com/velyvelylovely/Database/assets/98696925/3f19dcb7-05f3-4977-a35e-095ac8d76bc8)

### 날짜와 시간

![image](https://github.com/velyvelylovely/Database/assets/98696925/7d1a4ec7-760a-4429-82ea-1f77022fe129)

### 그 외

![image](https://github.com/velyvelylovely/Database/assets/98696925/881d9e4a-377e-4f08-a990-c9680e56707b)

## Key Constraints

데이터베이스 테이블에서 '키(Key)'는 테이블의 튜플(데이터 레코드)을 고유하게 식별하는 데 사용됩니다. 키에는 여러 제약 조건이 존재하며, 그 중에서도 주요한 세 가지, 즉 'PRIMARY KEY', 'UNIQUE', 'DEFAULT'에 대해 살펴보겠습니다.

### PRIMARY KEY

'PRIMARY KEY'는 테이블의 튜플을 고유하게 식별하기 위해 사용되며 이 키는 하나 이상의 속성으로 구성됩니다. 'PRIMARY KEY'는 중복된 값을 가질 수 없으며, NULL 값을 가질 수 없습니다. 이를 통해 데이터의 정확성과 일관성을 보장합니다.

### PRIMARY KEY를 선언하는 방법

속성이 하나일 때와 두 개 이상일 때 'PRIMARY KEY' 선언 방법은 다음과 같습니다.

- 속성이 하나일 때:

```sql
CREATE TABLE PLAYER(
    id INT PRIMARY KEY,
    ...
);
```

- 속성이 두 개 이상일 때:

```sql
CREATE TABLE PLAYER(
   team_id VARCHAR(12),
   back_number INT,
    ...
    PRIMARY KEY (team_id, back_number)
);
```

### UNIQUE

'UNIQUE' 제약조건은 지정된 속성이 중복된 값을 가질 수 없음을 지정합니다. 즉, 각 튜플의 해당 속성 값은 테이블 내에서 유일해야 합니다. 하지만 NULL 값은 중복을 허용할 수도 있습니다. 이는 RDBMS마다 다르므로 해당 시스템의 문서를 참고해야 합니다.

### UNIQUE를 선언하는 방법

속성이 하나일 때와 두 개 이상일 때 'UNIQUE' 선언 방법은 다음과 같습니다.

- 속성이 하나일 때:

```sql
CREATE TABLE PLAYER(
    id INT UNIQUE,
    ....
);
```

- 속성이 두 개 이상일 때:

```sql
CREATE TABLE PLAYER (
    team_id VARCHAR(12),
    back_number INT,
    ...
    UNIQUE (team_id, back_number)
);
```

### DEFAULT

'DEFAULT' 제약조건은 속성의 기본값을 정의할 때 사용합니다. 새 튜플을 저장할 때 해당 속성에 대한 값이 제공되지 않으면, 'DEFAULT' 값이 대신 저장됩니다.

### DEFAULT를 선언하는 방법

'DEFAULT' 선언 방법은 다음과 같습니다.

```sql
CREATE TABLE Orders (
    ...
    menu VARCHAR(15) DEFAULT '짜장면',
    ...
);
```

이렇게 'DEFAULT'를 사용하면, 'menu' 속성에 대한 값이 명시적으로 제공되지 않은 경우, 새 튜플의 'menu' 속성 값은 '짜장면'으로 설정됩니다.

### CHECK

'CHECK'는 특정 속성의 값을 제한할 때 사용하는 제약 조건입니다. 이를 통해 데이터의 무결성을 보장할 수 있습니다. 예를 들어, 직원의 나이를 20세 이상으로 제한하고 싶다면 'CHECK' 제약 조건을 사용할 수 있습니다.

### CHECK를 선언하는 방법

속성이 하나일 때와 두 개 이상일 때 'CHECK' 선언 방법은 다음과 같습니다.

- 속성이 하나일 때:

```sql
CREATE TABLE EMPLOYEE (
    ...
    age INT CHECK (age >= 20),
    ....
);
```

- 속성이 두 개 이상일 때:

```sql
CREATE TABLE PROJECT (
    start_date DATE,
    end_date DATE,
    ...
    CHECK (start_date < end_date)
);
```

### FOREIGN KEY

'FOREIGN KEY'는 한 테이블의 속성이 다른 테이블의 'PRIMARY KEY' 또는 'UNIQUE KEY'를 참조할 때 사용하는 제약 조건입니다. 이를 통해 두 테이블 간의 관계를 표현할 수 있습니다.

### FOREIGN KEY를 선언하는 방법

'FOREIGN KEY' 선언 방법은 다음과 같습니다.

```sql
CREATE TABLE EMPLOYEE (
...
    dept_id INT,
    FOREIGN KEY (dept_id)
        REFERENCES DEPARTMENT(id)
        ON DELETE reference_option
        ON UPDATE reference_option
);
```

참조 옵션에는 여러 가지가 있습니다.

- **CASCADE**: 참조값의 삭제/변경을 그대로 반영합니다.
- **SET NULL**: 참조값이 삭제/변경될 경우 NULL로 변경합니다.
- **RESTRICT**: 참조값이 삭제/변경되는 것을 금지합니다.
- **NO ACTION**: RESTRICT와 유사합니다.
- **SET DEFAULT**: 참조값이 삭제/변경될 경우 DEFAULT 값으로 변경합니다.

### Constraint 이름 명시하기

제약 조건에 이름을 붙이면 어떤 제약 조건을 위반했는지 쉽게 파악할 수 있습니다. 또한, 제약 조건을 삭제하고 싶을 때 해당 이름으로 삭제할 수 있습니다.

```sql
CREATE TABLE TEST (
    ...
    age INT CONSTRAINT age_over_20 CHECK (age > 20)
    ....
);
```

이름을 붙였을 때와 생략했을 때의 차이는 다음과 같습니다.

- 이름을 붙였을 때: `Check constraint ‘age_over_20’ is violated.`
- 이름을 생략했을 때: `Check constraint ‘test_chk_1’ is violated.`

이처럼 제약 조건에 이름을 붙이면 어떤 제약 조건이 위반되었는지 쉽게 알 수 있습니다.

## ALTER TABLE

데이터베이스 테이블의 구조를 변경하고 싶을 때 'ALTER TABLE' 명령어를 사용합니다. 이를 통해 테이블의 속성을 추가하거나 이름을 변경하거나, 테이블의 이름 자체를 변경하는 등의 작업을 수행할 수 있습니다. 하지만 이미 서비스 중인 테이블의 구조를 변경하는 경우, 변경 작업이 서비스의 백엔드에 영향을 미치지 않을지 검토한 후에 변경하는 것이 중요합니다.

아래 표는 'ALTER TABLE' 명령어의 사용 예시를 보여줍니다.

| 유형 | MySQL 예제 |
| --- | --- |
| 속성 추가 | ALTER TABLE employee ADD blood VARCHAR(2); |
| 속성 이름 변경 | ALTER TABLE employee RENAME COLUMN phone TO phone_num; |
| 속성 타입 변경 | ALTER TABLE employee MODIFY COLUMN blood CHAR(2); |
| 테이블 이름 변경 | ALTER TABLE logs RENAME TO backend_logs; |
| Primary Key 추가 | ALTER TABLE log ADD PRIMARY KEY (id); |

## Database 구조를 정의할 때 중요한 점

데이터베이스 구조를 정의하려면, 만들려는 서비스의 스펙과 데이터의 일관성, 편의성, 확장성 등을 종합적으로 고려해야 합니다. 즉, 서비스의 요구사항을 충족시키면서도 데이터를 효율적으로 관리할 수 있는 구조를 설계해야 합니다. 이런 고려사항들이 반영되지 않은 데이터베이스 구조는 서비스의 성능을 저하시키고, 유지보수를 어렵게 만들 수 있습니다. 따라서, DB 스키마를 적절하게 정의하는 것은 매우 중요한 작업입니다.
