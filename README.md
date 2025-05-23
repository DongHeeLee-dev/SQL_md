# SQL(Structured Query Language)

- 데이터베이스 : 조직체에서 모든 응용 시스템들이 공용할 수 있도록 통합되고 저장죔으로써 언제든지 운영가능하게 공유 할 수 있는 데이터의 집합체

# DBMS (Databese Management System)

- 데이터베이스 관리 시스템 : SQL 명령어 사용하지 않고
  프로그램을 통해 데이터베이스를 효과적으로 조작

# SQL 명령의 종류

| 분류           | 명령어      | 설명                                   |
| -------------- | ----------- | -------------------------------------- |
| DDL (정의)     | `CREATE`    | 테이블, 인덱스, 뷰 등 데이터 구조 생성 |
|                | `ALTER`     | 기존 테이블 구조 수정                  |
|                | `DROP`      | 테이블, 인덱스, 뷰 등 삭제             |
|                | `TRUNCATE`  | 테이블의 모든 데이터 삭제 (구조 유지)  |
| DML (조작)     | `SELECT`    | 데이터 조회                            |
|                | `INSERT`    | 데이터 삽입                            |
|                | `UPDATE`    | 기존 데이터 수정                       |
|                | `DELETE`    | 데이터 삭제                            |
| DCL (제어)     | `GRANT`     | 사용자 권한 부여                       |
|                | `REVOKE`    | 사용자 권한 회수                       |
| TCL (트랜잭션) | `COMMIT`    | 변경 사항 확정 (저장)                  |
|                | `ROLLBACK`  | 변경 사항 취소                         |
|                | `SAVEPOINT` | 롤백을 위한 지점 저장                  |

# 인덱스

- 데이터베이스를 빠르게 조작하려고 만든 색인표나 태그. 인덱스를 지정하면 원본 테이블을 참조해 독립적인 공간에 특정 필드로 정렬한 테이블 생성

# 기본키

- Primary Key 는 테이블에서 레코드의 중복을 허용하지 않는 대표성을 가진 유일한 필드의 모음

# 참조키

- 참조키 또는 외래키(Foreign Key)는 테이블 간의 관계를 나타내는 필드의 모음

# ERD

- Entity Relationship Diagram 은 테이블 구조와 연관관계를 보여주는 도표

# 기본 명령어

## SELECT

구문 #1 | SELECT \* FROM 테이블명;  
구문 #2 | SELECT 필드명1, 필드명2..., 필드명n FROM 테이블명;  
구문 #3 | SELECT 필드명 [AS] 별명 FROM 테이블명;

## WHERE

- WHERE 구문은 SELECT 명령을 이용해 지정한 테이블에서 조건에 맞는 데이터를 검색하는 데 사용

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 조건식;
```

사용 예

```sql
WHERE CUSTOMER_NM='나경숙'
-CUSTOMER_NM 값이 '나경숙'인 데이터를 검색한다.
```

## HAVING

## 📌 SQL WHERE vs HAVING 정리

| 구문     | 용도                            | 적용 대상               |
| -------- | ------------------------------- | ----------------------- |
| `WHERE`  | 그룹화 전에 조건 필터링         | 원본 데이터             |
| `HAVING` | 그룹화(GROUP BY) 후 조건 필터링 | 집계 결과 (SUM, AVG 등) |

---

### ✅ WHERE 예시: 그룹화 전 필터링

```sql
SELECT name, score
FROM students
WHERE score >= 80; // 결과값 예시 동희 | 90, 지민 | 80

SELECT major, AVG(score) AS avg_score
FROM students
GROUP BY major
HAVING AVG(score) >= 80; // 컴퓨터공학 | 85

```

### AND

- AND 구문은 지정한 테이블에서 나열한 조건 모두 만족하는 테이블 검색하고 하나라도 만족하지 않을 시 검색하지 않는다.

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 조건식1 AND 조건식2 ;
```

### OR

- OR 구문은 나열한 조건에 하나라도 만족하는 데이터를 검색하고 모두 만족하지 않으면 검색하지 않는다.

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 조건식1 or 조건식2 or 조건식n;
```

### BETWEEN ..AND

- BETWEEN .. AND 구문은 지정한 범위의 데이터를 검색 필드형식으로 수치, 문자, 날짜 등 지정

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 필드명 [NOT] BETWEEN 시작값 AND 종료값 ;
```

## 비교 연산자

- 두 값의 '같다', '같지 않다', '크다', '작다' AND, OR 구문과 조합해 다양한 검색 조건을 만드는데 사용

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 조건식 ;
```

```비교연산자
 = : 같다
 <>, !=, ^= : 다르다
 A > B : A가 B보다 크다
 A < B : A가 B보다 작다
 A >=B : A가 B보다 크거나 같다
 A <=B : A가 B보다 작거나 같다
```

## LIKE

- LIKE 구문은 검색값이 필드에 포함된 데이터 검색하는데 사용
  LIKE 앞에 NOT을 지정하면 필드에 검색값이 포함되지 않는 데이터 검색

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 필드명 [NOT] LIKE '%검색값%' ;
    WHERE 필드명 [NOT] LIKE '_검색값_' ;
```

```sql
'문자%' : 문자로 시작하는 값
'%문자' : 문자로 끝나는 값
'%문자%' : 문자가 포함된 값
'_' : 지정한 위치에 1자리 문자면 무엇이든 가능
```

## IN

- IN 구문은 검색값이 필드에 포함된 데이터 검색하는데 사용
  IN 앞에 NOT 을 지정해 검색값이 필드에 포함되지 않는 데이터 검색

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 필드명 [NOT] IN LIKE (검색값, 검색값2) ;
```

```sql
WHERE REG_YEAR IN ('2018', '2019')
-REG_YEAR 값이 '2018', '2019'인 데이터를 검색한다.

WHERE REG_YEAR  NOT IN ('2018')
-REG_YEAR 값이 '2018'이 아닌 데이터를 검색한다.
```

## ORDER BY

- 나열한 필드를 기준으로 데이터를 정렬  
  기본정렬방식은 오른차순(ASC), 내림차순(DESC)

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 조건식
    ORDER BY 필드명1 [ASC|DESC]
```

## GROUP BY

- 나열한 필드를 기준으로 데이터를 묶어준다.
  묶어 놓은 필드를 대상으로 MIN(), MAX(), SUM(), AVG(), COUNT() 등의 집계함수를 이용해 그룹의 최솟값, 최댓값, 합계, 평균, 개수를 구한다.  
  HAVING 구문은 WHERE 구문과 비슷한 기능으로 그룹에 대한 검색 조건을 설정

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 조건식
    ORDER BY 필드명1 [ASC|DESC]
```

## DISTINCT

- 나열한 필드 값을 중복 없이 구함.
  SELECT 컬럼명 FROM 테이블명 : 모든 데이터를 가져옴 (중복 포함)

SELECT DISTINCT 컬럼명 FROM 테이블명 : 중복 없이 "유일한 값들"만 가져옴

```sql
SELECT 검색필드명
    FROM 테이블명
    WHERE 조건식;

SELECT DISTINCT major FROM students;
```

## JOIN

- JOIN 구문은 2개 이상 테이블의 연관정보 구함
- FROM 기준 테이블 JOIN 연관 테이블 ON 조건 형식으로 ON에는 기준 테이블과 연관 테이블의 관계를 나타내는 조건 설정

- **JOIN** : 기준 테이블과 대상 테이블에 매칭하는 필드값이 있는 경우에 검색
- **LEFT JOIN** : 기존 테이블의 모든 필드값을 보이고 대상 테이블에 매칭하는 필드값이 있는 경우에 검색하고, 그렇지 않으면 공백
- **Right JOIIN** : 대상 테이블 모든 필드값 보이고 기준 테이블에 매칭하는 필드값이 있는 경우에 검색하고, 그렇지 않으면 공백으로 보임
- **FULL OUTER JOIN** : 기준 테이블과 대상 테이블에 상호 매칭하는 필드값이 있는 경우에 검색, 그렇지 않으면 공백

```sql
구문 #1
SELECT 검색필드명
    FROM 테이블명1
    JOIN 테이블명2
    ON 테이블명1(별명1).필드명1 = 테이블명2(별명2).필드명1
    AND 테이블명1(별명1).필드명2 = 테이블명2(별명2).필드명2
    WHERE 조건식;

구문 #2
SELECT 검색필드명
    FROM 테이블명1 (별명1),
    JOIN 테이블명2 (별명2)
    WHERE 테이블명1(별명1).필드명1 = 테이블명2(별명2).필드명1(+);

```

## CASE

- CASE 구문은 조건에 만족하는 결과값 반환
- '조건대상'에 대한 '비굣값'을 WHEN 구문에 지정하고, 조건 만족한 경우 THEN구문에서 지정한 '결과' 반환
- 만일 어떤 조건도 만족하지 않으면 ELSE 구문값 반환

```sql
CASE 조건대상 WHEN 비굣값 1 THEN 결과 1
            WHEN 비굣값 2 THEN 결과 2
           ELSE 결과가 없을 때
           END


```

## ROWNUM

- ROWNUM 구문은 레코드 검색 시 생성되는 행 번호
- '조건대상'에 대한 '비굣값'을 WHEN 구문에 지정하고, 조건 만족한 경우 THEN구문에서 지정한 '결과' 반환
- 만일 어떤 조건도 만족하지 않으면 ELSE 구문값 반환

## 🔢 Oracle ROWNUM 정리

- `ROWNUM`은 결과 행에 번호를 매기는 가상 컬럼
- 1부터 시작하며, **정렬 전에 먼저 적용**됨
- 상위 N개를 추출할 때 자주 사용
- ROWNUM은 정렬보다 먼저 처리됨
- 정렬 후 ROWNUM을 쓰고 싶다면 반드시 서브쿼리 사용

### ✅ 사용 예

```sql
-- 정렬 없이 상위 3개
SELECT *
FROM students
WHERE ROWNUM <= 3;

-- 정렬 후 상위 3개 (정석)
SELECT *
FROM (
  SELECT *
  FROM students
  ORDER BY score DESC
)
WHERE ROWNUM <= 3;
```

## UPDATE

- UPDATE 명령은 조건식 만족하는 데이터 필드값 변경

```sql
UPDATE 테이블명
SET 필드명1 = 값1, 필드명2 = 값2 ...,
WHERE 조건식;

```

## 트랜잭션 이해

- 데이터베이스 작업에서 하나로 묶을 수 있는 업무

```sql
## 💼 고객 포인트 입력 트랜잭션 프로세스

### 🔄 작업 흐름

1. **작업 시작**
   - `트랜잭션 시작 (BEGIN)`

2. **포인트 정보 입력**
   - ✅ 정상: 포인트 정보 입력 진행
   - ❌ 오류 발생: 작업 이상 종료 → `ROLLBACK` (트랜잭션 종료)

3. **누적 포인트 정보 갱신**
   - ✅ 정상: 누적 포인트 업데이트 진행
   - ❌ 오류 발생: 작업 이상 종료 → `ROLLBACK` (트랜잭션 종료)

4. **작업 종료**
   - ✅ 모든 작업 정상 처리 시 → `COMMIT` (트랜잭션 종료)

```

## 서브쿼리

## 🔍 서브쿼리 예시: 특정 조건 만족하는 고객만 조회

### ✅ 의미

- B 테이블 고객 중
- TB_POINT에 포인트 기록이 있는 고객만 조회

### ✅ 쿼리 예시

```sql
SELECT *
FROM B
WHERE CUSTOMER_CD IN (
  SELECT CUSTOMER_CD
  FROM TB_POINT
);
```
