# Spring Batch Test

### 개발 환경
* IntelliJ IDEA Ultimate
* Java 17 (향후 21 고려)
* mysql
* spring boot 3.2.4

### 최초 생성
* lombok
* Spring Web
* Spring Batch
* Mysql Driver
* Spring Data JPA

### table 정의
* batch 관련 9개의 table 은 자동 생성
* 검증을 위한 csv 파일의 db 적재용 : customers_info
```sql
-- batch.customers_info definition
drop table if exists customers_info;
CREATE TABLE customers_info (
    customer_id int NOT NULL,
    first_name varchar(100) DEFAULT NULL,
    last_name varchar(100) DEFAULT NULL,
    email varchar(100) DEFAULT NULL,
    gender varchar(100) DEFAULT NULL,
    contact varchar(100) DEFAULT NULL,
    country varchar(100) DEFAULT NULL,
    dob varchar(100) DEFAULT NULL,
    PRIMARY KEY (customer_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
### test
* vs code의  extiontion 에 "Thunder Client" 설치
* post http://localhost:9191/jobs/importCustomers
* 이전 data 조회 및 삭제
```sql
-- csv to db 조회
SELECT * from customers_info;
DELETE FROM customers_info ;
SELECT COUNT(*) FROM customers_info WHERE country = 'United States';
-- batch success/fail 조회
SELECT * FROM BATCH_JOB_EXECUTION bje ;
```
* CustomerProcessor.java 에 조건 추가