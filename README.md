# SQL
```bash
PS C:\Users\Minfy> psql -U midhilesh -d minfy
Password for user midhilesh:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "midhilesh"
PS C:\Users\Minfy> psql -U midhilesh
Password for user midhilesh:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "midhilesh"
PS C:\Users\Minfy> psql -U midhilesh
Password for user midhilesh:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "midhilesh"
PS C:\Users\Minfy> psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# create user midhilesh with password "Y@mini!23"
postgres-# create user midhilesh with password "Y@mini!23";
ERROR:  syntax error at or near ""Y@mini!23""
LINE 1: create user midhilesh with password "Y@mini!23"
                                            ^
postgres=# create user midhilesh with password 'Y@mini!23';
CREATE ROLE
postgres=# create database minfy owner midhilesh;
CREATE DATABASE
postgres=# grant all privileges on database minfy to midhilesh;
GRANT
postgres=# \q
PS C:\Users\Minfy> psql -U midhilesh -d minfy
Password for user midhilesh:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

minfy=> psql -U postgres
minfy-> psql -U postgres;
ERROR:  syntax error at or near "psql"
LINE 1: psql -U postgres
        ^
minfy=> use user postgres;
ERROR:  syntax error at or near "use"
LINE 1: use user postgres;
        ^
minfy=> \l
                                                              List of databases
   Name    |   Owner   | Encoding | Locale Provider |      Collate       |       Ctype        | Locale | ICU Rules |    Access privileges
-----------+-----------+----------+-----------------+--------------------+--------------------+--------+-----------+-------------------------
 minfy     | midhilesh | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =Tc/midhilesh          +
           |           |          |                 |                    |                    |        |           | midhilesh=CTc/midhilesh
 postgres  | postgres  | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           |
 template0 | postgres  | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres            +
           |           |          |                 |                    |                    |        |           | postgres=CTc/postgres
 template1 | postgres  | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres            +
           |           |          |                 |                    |                    |        |           | postgres=CTc/postgres
(4 rows)


minfy=> set role postgres
minfy-> set role postgres;
ERROR:  syntax error at or near "set"
LINE 2: set role postgres;
        ^
minfy=> select current_user,session_user;
 current_user | session_user
--------------+--------------
 midhilesh    | midhilesh
(1 row)


minfy=> \du
                             List of roles
 Role name |                         Attributes
-----------+------------------------------------------------------------
 midhilesh |
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS


minfy=> set role postgres;
ERROR:  permission denied to set role "postgres"
minfy=> create role mike;
ERROR:  permission denied to create role
DETAIL:  Only roles with the CREATEROLE attribute may create roles.
minfy=> \du
                             List of roles
 Role name |                         Attributes
-----------+------------------------------------------------------------
 midhilesh |
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS


minfy=> \q
PS C:\Users\Minfy> psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# create role mike;
CREATE ROLE
postgres=# \du
                             List of roles
 Role name |                         Attributes
-----------+------------------------------------------------------------
 midhilesh |
 mike      | Cannot login
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS


postgres=# set role mike;
SET
postgres=> select current_user,session_user;
 current_user | session_user
--------------+--------------
 mike         | postgres
(1 row)


postgres=> \q
PS C:\Users\Minfy> psql -U midhilesh -d minfy
Password for user midhilesh:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

minfy=> create table student (
minfy(> student_id integer, first_name varchar(20), last_name varchar(20), email varchat(50), date_of_birth date);
ERROR:  type "varchat" does not exist
LINE 2: ...st_name varchar(20), last_name varchar(20), email varchat(50...
                                                             ^
minfy=> create table stduents(student_id integer, first_name varchar(20), last_name varchar(20), email varchar(50), date_of_birth date);
CREATE TABLE
minfy=> select * from students;
ERROR:  relation "students" does not exist
LINE 1: select * from students;
                      ^
minfy=> select * from student;
ERROR:  relation "student" does not exist
LINE 1: select * from student;
                      ^
minfy=> select * from stduents;
 student_id | first_name | last_name | email | date_of_birth
------------+------------+-----------+-------+---------------
(0 rows)


minfy=> rename stduents new name students;
ERROR:  syntax error at or near "rename"
LINE 1: rename stduents new name students;
        ^
minfy=> alter table stduents rename to students;
ALTER TABLE
minfy=> select * from students;
 student_id | first_name | last_name | email | date_of_birth
------------+------------+-----------+-------+---------------
(0 rows)


minfy=> \d
           List of relations
 Schema |   Name   | Type  |   Owner
--------+----------+-------+-----------
 public | students | table | midhilesh
(1 row)


minfy=> \l
                                                              List of databases
   Name    |   Owner   | Encoding | Locale Provider |      Collate       |       Ctype        | Locale | ICU Rules |    Access privileges
-----------+-----------+----------+-----------------+--------------------+--------------------+--------+-----------+-------------------------
 minfy     | midhilesh | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =Tc/midhilesh          +
           |           |          |                 |                    |                    |        |           | midhilesh=CTc/midhilesh
 postgres  | postgres  | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           |
 template0 | postgres  | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres            +
           |           |          |                 |                    |                    |        |           | postgres=CTc/postgres
 template1 | postgres  | UTF8     | libc            | English_India.1252 | English_India.1252 |        |           | =c/postgres            +
           |           |          |                 |                    |                    |        |           | postgres=CTc/postgres
(4 rows)


minfy=> \d students
                        Table "public.students"
    Column     |         Type          | Collation | Nullable | Default
---------------+-----------------------+-----------+----------+---------
 student_id    | integer               |           |          |
 first_name    | character varying(20) |           |          |
 last_name     | character varying(20) |           |          |
 email         | character varying(50) |           |          |
 date_of_birth | date                  |           |          |


minfy=> alter table students add column enrolment_date date;
ALTER TABLE
minfy=> alter table students drop column enrolment_date date;
ERROR:  syntax error at or near "date"
LINE 1: alter table students drop column enrolment_date date;
                                                        ^
minfy=> alter table students drop column enrolment_date;
ALTER TABLE
minfy=> alter table students rename column email to mail;
ALTER TABLE
minfy=> \d students
                        Table "public.students"
    Column     |         Type          | Collation | Nullable | Default
---------------+-----------------------+-----------+----------+---------
 student_id    | integer               |           |          |
 first_name    | character varying(20) |           |          |
 last_name     | character varying(20) |           |          |
 mail          | character varying(50) |           |          |
 date_of_birth | date                  |           |          |


minfy=> alter table students rename column mail to email;
ALTER TABLE
minfy=> alter table students alter column email type varchar(100);
ALTER TABLE
minfy=> \d students
                         Table "public.students"
    Column     |          Type          | Collation | Nullable | Default
---------------+------------------------+-----------+----------+---------
 student_id    | integer                |           |          |
 first_name    | character varying(20)  |           |          |
 last_name     | character varying(20)  |           |          |
 email         | character varying(100) |           |          |
 date_of_birth | date                   |           |          |


minfy=> alter table students add column phone_number varchar(20);
ALTER TABLE
minfy=> \d students;
                         Table "public.students"
    Column     |          Type          | Collation | Nullable | Default
---------------+------------------------+-----------+----------+---------
 student_id    | integer                |           |          |
 first_name    | character varying(20)  |           |          |
 last_name     | character varying(20)  |           |          |
 email         | character varying(100) |           |          |
 date_of_birth | date                   |           |          |
 phone_number  | character varying(20)  |           |          |


minfy=> alter table students drop column phone_number;
ALTER TABLE
minfy=> \d students;
                         Table "public.students"
    Column     |          Type          | Collation | Nullable | Default
---------------+------------------------+-----------+----------+---------
 student_id    | integer                |           |          |
 first_name    | character varying(20)  |           |          |
 last_name     | character varying(20)  |           |          |
 email         | character varying(100) |           |          |
 date_of_birth | date                   |           |          |


minfy=> alter table students rename column date_of_birth to dob;
ALTER TABLE
minfy=> \d students;
                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(20)  |           |          |
 last_name  | character varying(20)  |           |          |
 email      | character varying(100) |           |          |
 dob        | date                   |           |          |


minfy=> create table mike(name varchar(20));
CREATE TABLE
minfy=> \d mike;
                       Table "public.mike"
 Column |         Type          | Collation | Nullable | Default
--------+-----------------------+-----------+----------+---------
 name   | character varying(20) |           |          |


minfy=> drop table mike;
DROP TABLE
minfy=> \d mike;
Did not find any relation named "mike".
minfy=> \d students;
                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(20)  |           |          |
 last_name  | character varying(20)  |           |          |
 email      | character varying(100) |           |          |
 dob        | date                   |           |          |


minfy=> drop table mike;
ERROR:  table "mike" does not exist
minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
minfy->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 2
minfy=> \d students;
                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(20)  |           |          |
 last_name  | character varying(20)  |           |          |
 email      | character varying(100) |           |          |
 dob        | date                   |           |          |


minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


minfy=> select first_name,dob from students;
 first_name |    dob
------------+------------
 Alice      | 2003-05-15
 Bob        | 2002-08-22
 Charlie    | 2003-01-10
(3 rows)


minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob) values (4,"Midhilesh","Polisetty", "midhil@gmail.com",'2004-04-30');
ERROR:  column "Midhilesh" does not exist
LINE 1: ..._id, first_name, last_name, email, dob) values (4,"Midhilesh...
                                                             ^
minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob) values (4,'Midhilesh','Polisetty', 'midhil@gmail.com','2004-04-30');
INSERT 0 1
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
(4 rows)


minfy=> select * from students where dob>'2003-01-10;
minfy'> '
minfy-> ;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15
          4 | Midhilesh  | Polisetty | midhil@gmail.com        | 2004-04-30
(2 rows)


minfy=> select * from students where name='Bob';
ERROR:  column "name" does not exist
LINE 1: select * from students where name='Bob';
                                     ^
minfy=> select * from students where first_name='Bob';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


minfy=> select * from students where dob>'1995-01-10' and dob<'2002-01-01';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


minfy=> select * from students where dob>'1995-01-10' and dob<'2002-012-01';
ERROR:  invalid input syntax for type date: "2002-012-01"
LINE 1: ...ct * from students where dob>'1995-01-10' and dob<'2002-012-...
                                                             ^
minfy=> select * from students where dob>'1995-01-10' and dob<'2002-12-01';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


minfy=> select * from students where first_name like'B%';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


minfy=> select * from students where first_name like'b%';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


minfy=> select * from students where first_name ilike'b%';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


minfy=> select * from students where student_id=2;
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


minfy=> select * from students where dob<'2003-01-01';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


minfy=> select * from students where first_name like'b%' or 'c%';
ERROR:  invalid input syntax for type boolean: "c%"
LINE 1: select * from students where first_name like'b%' or 'c%';
                                                            ^
minfy=> select * from students where first_name like'b%' or like 'c%';
ERROR:  type "like" does not exist
LINE 1: ...lect * from students where first_name like'b%' or like 'c%';
                                                             ^
minfy=> select * from students where first_name like'b%' or like'c%';
ERROR:  type "like" does not exist
LINE 1: ...elect * from students where first_name like'b%' or like'c%';
                                                              ^
minfy=> select * from students where first_name like'b%';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


minfy=> select * from students where first_name ilike 'b%';
 student_id | first_name | last_name |          email          |    dob
------------+------------+-----------+-------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com | 2002-08-22
(1 row)


minfy=> select * from students where first_name ilike ('B%' or 'C%');
ERROR:  invalid input syntax for type boolean: "B%"
LINE 1: select * from students where first_name ilike ('B%' or 'C%')...
                                                       ^
minfy=> select * from students where first_name like 'B%' or first_name like 'C%';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


minfy=> select * from students where email like '%example.com';
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


minfy=> select * from students where email=null;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


minfy=> INSERT INTO students (student_id, first_name, last_name, dob) VALUES (4, 'Diana', 'Prince', '2001-11-01');
INSERT 0 1
minfy=> select * from students where email=null;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


minfy=> select * from students where email is null;
 student_id | first_name | last_name | email |    dob
------------+------------+-----------+-------+------------
          4 | Diana      | Prince    |       | 2001-11-01
(1 row)


minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          4 | Diana      | Prince    |                           | 2001-11-01
(5 rows)


minfy=> UPDATE students
minfy-> SET email = 'alices@example.net'
minfy-> WHERE student_id = 1;
UPDATE 1
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          4 | Diana      | Prince    |                           | 2001-11-01
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
(5 rows)


minfy=> alter table students alter column student_id where first_name='Diana' to student_id=5
minfy-> ;
ERROR:  syntax error at or near "where"
LINE 1: alter table students alter column student_id where first_nam...
                                                     ^
minfy=> update students set student_id=5 where first_name='Diana';
UPDATE 1
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          5 | Diana      | Prince    |                           | 2001-11-01
(5 rows)


minfy=> update students set dob='2003-02-15' where first_name='Charlie';
UPDATE 1
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          5 | Diana      | Prince    |                           | 2001-11-01
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
(5 rows)


minfy=> update students set email='diana.prince@example.org' where first_name='Diana';
UPDATE 1
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
(5 rows)


minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy-> VALUES (100, 'Temp', 'User', 'temp@example.com', '2000-01-01');
INSERT 0 1
minfy=> select * from students where student_id=100;
 student_id | first_name | last_name |      email       |    dob
------------+------------+-----------+------------------+------------
        100 | Temp       | User      | temp@example.com | 2000-01-01
(1 row)


minfy=> delete from students where student_id=100;
DELETE 1
minfy=> select * from students where student_id=100;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
(5 rows)


minfy=>
minfy=> SELECT * FROM students ORDER BY last_name ASC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
(5 rows)


minfy=> SELECT * FROM students ORDER BY student_id ASC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
(5 rows)


minfy=> SELECT * FROM students ORDER BY dob DESC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
(5 rows)


minfy=> SELECT * FROM students ORDER BY last_name, first_name;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
(5 rows)


minfy=> SELECT * FROM students ORDER BY dob ASC;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
(5 rows)


minfy=> SELECT * FROM students ORDER BY last_name DESC, first_name;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
(5 rows)


minfy=> SELECT * FROM students ORDER BY dob ASC limit 2;
 student_id | first_name | last_name |          email           |    dob
------------+------------+-----------+--------------------------+------------
          5 | Diana      | Prince    | diana.prince@example.org | 2001-11-01
          2 | Bob        | Johnson   | bob.johnson@example.com  | 2002-08-22
(2 rows)


minfy=> SELECT * FROM students ORDER BY student_id limit 2 offset 1;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
(2 rows)


minfy=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
(5 rows)


minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy-> VALUES (5, 'Eve', 'Smith', 'eve.smith@example.com', '2004-07-01');
INSERT 0 1
minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob)
minfy-> ;
ERROR:  syntax error at or near ";"
LINE 2: ;
        ^
minfy=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
          5 | Eve        | Smith     | eve.smith@example.com     | 2004-07-01
(6 rows)


minfy=> select distinct last_name from students;
 last_name
-----------
 Smith
 Polisetty
 Johnson
 Prince
 Brown
(5 rows)


minfy=> select distinct last_name from students order by dob;
ERROR:  for SELECT DISTINCT, ORDER BY expressions must appear in select list
LINE 1: select distinct last_name from students order by dob;
                                                         ^
minfy=> select distinct last_name order by dob from students;
ERROR:  syntax error at or near "from"
LINE 1: select distinct last_name order by dob from students;
                                               ^
minfy=> select distinct last_name from students;
 last_name
-----------
 Smith
 Polisetty
 Johnson
 Prince
 Brown
(5 rows)


minfy=>
minfy=> SELECT COUNT(*) AS total_students FROM students;
 total_students
----------------
              6
(1 row)


minfy=> INSERT INTO students (student_id, first_name) values (10,"Mike");
ERROR:  column "Mike" does not exist
LINE 1: ...T INTO students (student_id, first_name) values (10,"Mike");
                                                               ^
minfy=> INSERT INTO students (student_id, first_name) values (10,'Mike');
INSERT 0 1
minfy=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
          5 | Eve        | Smith     | eve.smith@example.com     | 2004-07-01
         10 | Mike       |           |                           |
(7 rows)


minfy=> SELECT COUNT(email) AS students_with_email FROM students;
 students_with_email
---------------------
                   6
(1 row)


minfy=> SELECT COUNT(*) AS total_students FROM students;
 total_students
----------------
              7
(1 row)


minfy=> SELECT COUNT(email is null) AS students_with_email FROM students;
 students_with_email
---------------------
                   7
(1 row)


minfy=> SELECT COUNT(email is not null) AS students_with_email FROM students;
 students_with_email
---------------------
                   7
(1 row)


minfy=> SELECT COUNT(email) AS students_with_email FROM students;
 students_with_email
---------------------
                   6
(1 row)


minfy=> select count(distinct last_name) as unique_last_names from students;
 unique_last_names
-------------------
                 5
(1 row)


minfy=> SELECT * FROM students;
 student_id | first_name | last_name |           email           |    dob
------------+------------+-----------+---------------------------+------------
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          4 | Midhilesh  | Polisetty | midhil@gmail.com          | 2004-04-30
          1 | Alice      | Smith     | alices@example.net        | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-02-15
          5 | Diana      | Prince    | diana.prince@example.org  | 2001-11-01
          5 | Eve        | Smith     | eve.smith@example.com     | 2004-07-01
         10 | Mike       |           |                           |
(7 rows)


minfy=> select first_name, count(*) as total_students from students group by first_name order by student_id;
ERROR:  column "students.student_id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: ...udents from students group by first_name order by student_id...
                                                             ^
minfy=> select first_name, count(*) as total_students from students group by students.first_name order by student_id;
ERROR:  column "students.student_id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: ...om students group by students.first_name order by student_id...
                                                             ^
minfy=> select first_name, count(*) as total_students from students group by students.first_name order by students.student_id;
ERROR:  column "students.student_id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 1: ...om students group by students.first_name order by students.s...
                                                             ^
minfy=> select first_name, count(*) as total_students from students group by first_name order by total_studnets;
ERROR:  column "total_studnets" does not exist
LINE 1: ...udents from students group by first_name order by total_stud...
                                                             ^
minfy=> select first_name, count(*) as total_students from students group by first_name order by total_students;
 first_name | total_students
------------+----------------
 Mike       |              1
 Eve        |              1
 Midhilesh  |              1
 Alice      |              1
 Bob        |              1
 Charlie    |              1
 Diana      |              1
(7 rows)


minfy=> select last_name, count(*) as total_students from students group by last_name order by total_students;
 last_name | total_students
-----------+----------------
           |              1
 Polisetty |              1
 Johnson   |              1
 Prince    |              1
 Brown     |              1
 Smith     |              2
(6 rows)


minfy=> select last_name, count(*) as total_students from students group by last_name order by total_students desc;
 last_name | total_students
-----------+----------------
 Smith     |              2
           |              1
 Polisetty |              1
 Johnson   |              1
 Prince    |              1
 Brown     |              1
(6 rows)


minfy=> select last_name, count(*) as total_students from students group by last_name having count(*)>1 order by total_students desc;
 last_name | total_students
-----------+----------------
 Smith     |              2
(1 row)


minfy=> select extract(year from dob) as birth_year, count(*) as number_of_births from students where dob is not null group by birth_year order by number_of_births
minfy-> ;
 birth_year | number_of_births
------------+------------------
       2002 |                1
       2001 |                1
       2003 |                2
       2004 |                2
(4 rows)


minfy=> select extract(year from dob) as birth_year, count(*) as number_of_births from students where dob is not null group by birth_year order by birth_year;
 birth_year | number_of_births
------------+------------------
       2001 |                1
       2002 |                1
       2003 |                2
       2004 |                2
(4 rows)


minfy=> select extract(year from dob) as birth_year, count(*) as number_of_births from students where dob is not null group by birth_year order by number_of_births desc;
 birth_year | number_of_births
------------+------------------
       2003 |                2
       2004 |                2
       2002 |                1
       2001 |                1
(4 rows)


minfy=> drop tsble if exists students;
ERROR:  syntax error at or near "tsble"
LINE 1: drop tsble if exists students;
             ^
minfy=> drop table if exists students;
DROP TABLE
minfy=> create table students(student_id integer unique, first_name varchar(30) not null, last_name varchar(30)not null,email varchar(100) unique, dob date,enrollment_status varchar(10) check(enrollment_status in ('enrolled','graduated','dropped')));
CREATE TABLE
minfy=> INSERT INTO students (student_id, last_name, email, dob) VALUES (1, 'Test', 'test@test.com', '2000-01-01'); -- Fails (first_name is NULL)
ERROR:  null value in column "first_name" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (1, null, Test, test@test.com, 2000-01-01, null).
minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob) VALUES (1, 'Test', 'User', 'test@test.com', '2000-01-01');
INSERT 0 1
minfy=> INSERT INTO students (student_id, last_name, email, dob) VALUES (1, 'Test', 'test@test.com', '2000-01-01');
ERROR:  null value in column "first_name" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (1, null, Test, test@test.com, 2000-01-01, null).
minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob) VALUES (2, 'Another', 'User', 'test@test.com', '2001-01-01');
ERROR:  duplicate key value violates unique constraint "students_email_key"
DETAIL:  Key (email)=(test@test.com) already exists.
minfy=> INSERT INTO students (student_id, first_name, last_name, email, dob, enrollment_status) VALUES (2, 'Another', 'User', 'another@test.com', '2001-01-01', 'pending');
ERROR:  new row for relation "students" violates check constraint "students_enrollment_status_check"
DETAIL:  Failing row contains (2, Another, User, another@test.com, 2001-01-01, pending).
minfy=> drop table if exists students;
DROP TABLE
minfy=> create table students(student_id serial primary key, first_name varchar(30) not null, last_name varchar(30)not null,email varchar(100) unique, dob date,enrollment_status varchar(10) check(enrollment_status in ('enrolled','graduated','dropped','pending')));
CREATE TABLE
minfy=> create table studen(student_id serial primary_key, first_name varchar(30) not null, last_name varchar(30)not null,email varchar(100) unique, dob date,enrollment_status varchar(10) check(enrollment_status in ('enrolled','graduated','dropped','pending')));
ERROR:  syntax error at or near "primary_key"
LINE 1: create table studen(student_id serial primary_key, first_nam...
                                              ^
minfy=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
minfy-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
INSERT 0 1
minfy=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
minfy-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
INSERT 0 1
minfy=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
minfy-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
INSERT 0 1
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob     | enrollment_status
------------+------------+-----------+---------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22 | enrolled
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10 | pending
(3 rows)


minfy=> create table courses(course_id serial primary key, course_name varchar(100) not null unique, credits integer check(credits>0 and credits<10));
CREATE TABLE
minfy=> \q
PS C:\Users\Minfy> psql -U midhilesh -d minfy
Password for user midhilesh:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

minfy=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
minfy=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4),('Web Development', 3),('Data Structures', 4);
INSERT 0 3
minfy=> select * from courses;
 course_id |     course_name     | credits
-----------+---------------------+---------
         1 | Introduction to SQL |       3
         2 | Database Design     |       4
         3 | Web Development     |       3
         4 | Data Structures     |       4
(4 rows)


minfy=> create table enrollments (enrollment_id serial primary key, student_id integer not null, course_id integer not null, enrollment_date date default current_date, grade char(1) check (grade in ('a', 'b', 'c', 'd', 'f', 'w', null)), constraint fk_student foreign key (student_id) references students(student_id) on delete cascade, constraint fk_course foreign key (course_id) references courses(course_id) on delete restrict, unique (student_id, course_id));
CREATE TABLE
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob     | enrollment_status
------------+------------+-----------+---------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15 | enrolled
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22 | enrolled
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10 | pending
(3 rows)


minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (6, 1, 'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_student"
DETAIL:  Key (student_id)=(6) is not present in table "students".
minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 11, 'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_course"
DETAIL:  Key (course_id)=(11) is not present in table "courses".
minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 2);
ERROR:  INSERT has more target columns than expressions
LINE 1: INSERT INTO enrollments (student_id, course_id, grade) VALUE...
                                                        ^
minfy=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1
minfy=> select * from enrollment;
ERROR:  relation "enrollment" does not exist
LINE 1: select * from enrollment;
                      ^
minfy=> select * from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             3 |          1 |         1 | 2025-05-30      | A
             4 |          1 |         2 | 2025-05-30      |
(2 rows)


minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (2, 1,'B');
INSERT 0 1
minfy=> select * from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             3 |          1 |         1 | 2025-05-30      | A
             4 |          1 |         2 | 2025-05-30      |
             5 |          2 |         1 | 2025-05-30      | B
(3 rows)


minfy=> select * from students where student_id=1;
 student_id | first_name | last_name |          email          |    dob     | enrollment_status
------------+------------+-----------+-------------------------+------------+-------------------
          1 | Alice      | Smith     | alice.smith@example.com | 2003-05-15 | enrolled
(1 row)


minfy=> select * from enrollment where student_id=1;
ERROR:  relation "enrollment" does not exist
LINE 1: select * from enrollment where student_id=1;
                      ^
minfy=> select * from enrollments where student_id=1;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             3 |          1 |         1 | 2025-05-30      | A
             4 |          1 |         2 | 2025-05-30      |
(2 rows)


minfy=> select * from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             3 |          1 |         1 | 2025-05-30      | A
             4 |          1 |         2 | 2025-05-30      |
             5 |          2 |         1 | 2025-05-30      | B
(3 rows)


minfy=> delete * from students where student_id=1;
ERROR:  syntax error at or near "*"
LINE 1: delete * from students where student_id=1;
               ^
minfy=> delete from students where student_id=1;
DELETE 1
minfy=> select * from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             5 |          2 |         1 | 2025-05-30      | B
(1 row)


minfy=> select * from students where student_id=1;
 student_id | first_name | last_name | email | dob | enrollment_status
------------+------------+-----------+-------+-----+-------------------
(0 rows)


minfy=> select * from enrollments where student_id=1;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
(0 rows)


minfy=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
minfy-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
INSERT 0 1
minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_student"
DETAIL:  Key (student_id)=(1) is not present in table "students".
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob     | enrollment_status
------------+------------+-----------+---------------------------+------------+-------------------
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22 | enrolled
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10 | pending
          4 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15 | enrolled
(3 rows)


minfy=> update students set student_id=1 where first_name='Alice';
UPDATE 1
minfy=> select * from students;
 student_id | first_name | last_name |           email           |    dob     | enrollment_status
------------+------------+-----------+---------------------------+------------+-------------------
          2 | Robert     | Johnson   | robert.j@example.com      | 2002-08-22 | enrolled
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10 | pending
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15 | enrolled
(3 rows)


minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
minfy=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 2);
ERROR:  INSERT has more target columns than expressions
LINE 1: INSERT INTO enrollments (student_id, course_id, grade) VALUE...
                                                        ^
minfy=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1
minfy=> select * from enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             5 |          2 |         1 | 2025-05-30      | B
             7 |          1 |         1 | 2025-05-30      | A
             8 |          1 |         2 | 2025-05-30      |
(3 rows)

```
