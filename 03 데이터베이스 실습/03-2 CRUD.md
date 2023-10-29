## CRUD 

CRUD는 컴퓨터 프로그래밍에서 데이터를 관리하는 데 가장 기본적인 네 가지 작업으로 Create(생성), Read(읽기), Update(수정), Delete(삭제)의 첫 글자를 따서 만든 약어입니다.

![image](https://github.com/velyvelylovely/Database/assets/98696925/e0e707ac-82f3-4788-ab64-0ae84fa5fa75)

## CREATE(INSERT)

새로운 데이터를 생성하거나 추가하는 작업을 말합니다. 예를 들어, 새로운 사용자 계정을 만드는 것이 이에 해당합니다.

```
\mariadb-10.6.15\bin>mysql -u testuser1 -p
Enter password: ********
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 36
Server version: 10.6.15-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use testdb1;
Database changed
2 rows in set (0.001 sec)

MariaDB [testdb1]> show tables;
+-------------------+
| Tables_in_testdb1 |
+-------------------+
| member            |
| member2           |
+-------------------+
2 rows in set (0.001 sec)
```

실행할 문장을 드래그를 하고 Ctrl + Enter를 하면 해당 쿼리가 실행됩니다.
