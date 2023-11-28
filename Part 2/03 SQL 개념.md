## SQL

SQL이란 Structured Query Language의 약자로, '구조화된 질의 언어'라는 뜻입니다. 현업에서는 관계형 데이터베이스 관리 시스템(RDBMS)의 표준 언어로 널리 사용되며, 데이터베이스의 구조를 정의하는 DDL(Data Definition Language), 데이터를 조작하는 DML(Data Manipulation Language), 그리고 데이터의 보안과 통제를 위한 VDL(View Definition Language) 등을 포함하는 종합적인 데이터베이스 언어라고 할 수 있습니다.

### SQL 주요 용어

SQL을 이해하기 위해서는 몇 가지 주요 용어를 알아야 합니다. 우선, 관계형 데이터 모델에서 '관계(Relation)'는 SQL에서 '테이블(Table)'이라는 개념으로 대응됩니다. 그리고 '속성(Attribute)'은 '열(Column)', '튜플(Tuple)'은 '행(Row)', '도메인(Domain)'은 SQL에서도 동일하게 '도메인(Domain)'으로 사용됩니다.

### SQL에서 Relation이란?

SQL에서 'Relation'은 '테이블'이란 개념으로 이해할 수 있습니다. 이는 SQL에서 튜플의 '멀티셋(Multiset)' 또는 '백(Bag)'으로 표현되며, 중복된 튜플을 허용합니다. 즉, SQL의 테이블은 같은 형태와 데이터를 가진 행이 여러 개 존재할 수 있다는 것을 의미합니다.

### SQL & RDBMS

SQL은 RDBMS의 표준 언어이지만, 실제로는 각 RDBMS 제품마다 제공하는 SQL의 스펙이 조금씩 다르다는 점을 알아두어야 합니다. 이는 SQL 표준을 모든 RDBMS가 완벽하게 지키는 것이 아니라, 각각의 시스템이 특정 기능을 추가하거나, 일부 기능을 생략하거나, 또는 동일한 기능을 조금 다른 방식으로 구현하기 때문입니다. 예를 들어, MySQL, Oracle 등의 RDBMS는 각각 고유의 SQL 구문과 기능을 제공합니다. 이 때문에 특정 RDBMS에 익숙해진 개발자가 다른 RDBMS를 사용하려고 할 때는 해당 시스템의 SQL 스펙을 따로 학습해야 할 필요가 종종 있습니다.

