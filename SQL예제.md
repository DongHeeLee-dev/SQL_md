## SQL 예제

### 📌 SQL 서브쿼리

- 하나의 SELECT문 안에 포함된 또 다른 SELECT문을 말해.

- 일반적으로 괄호 ()로 감싸서 사용함.

**메인 쿼리(Main Query)**에서 서브쿼리의 결과를 사용함.

# 📘 SQL: 스칼라 서브쿼리 vs 인라인 뷰 정리

## 🔍 서브쿼리(Subquery)란?

- 하나의 SQL문 안에 포함된 또 다른 `SELECT`문
- 괄호 `()`로 감싸서 메인 쿼리에서 보조적으로 사용
- 사용 위치에 따라 **스칼라 서브쿼리**, **인라인 뷰**, **WHERE절 서브쿼리** 등으로 구분

---

## ✅ 1. 스칼라 서브쿼리 (Scalar Subquery)

### 🔹 정의

- SELECT 또는 WHERE 절에서 사용
- 반드시 **1행 1열(단일 값)**만 반환해야 함
- 반환된 값은 각 행에 대해 붙여지는 **"스칼라 값"**

### 🔹 예제 SQL

```sql
SELECT
  name,
  (SELECT department_name
   FROM departments
   WHERE departments.department_id = employees.department_id) AS dept_name
FROM employees;

| name    | department\_id | department\_name |
| ------- | -------------- | ---------------- |
| Alice   | 10             | Sales            |
| Bob     | 20             | HR               |
| Charlie | 10             | Sales            |

employees의 각 행마다 서브쿼리가 실행되어 department_name을 조회함
```

## ✅ 2. 인라인 뷰 (Inline View)

### 🔹 정의

- `FROM` 절 안에 들어가는 서브쿼리
- 마치 **임시 테이블(가상 뷰)**처럼 사용됨
- 반드시 **별칭(Alias)** 지정 필요

---

### 🔹 예제 SQL

```sql
SELECT department_id, AVG(salary),
       (SELECT department_name
        FROM departments
        WHERE departments.department_id = inline.department_id) AS department_name
FROM (
  SELECT department_id, salary
  FROM employees
) inline
GROUP BY department_id;

| department\_id | AVG(salary) | department\_name |
| -------------- | ----------- | ---------------- |
| 10             | 5250        | Sales            |
| 20             | 6000        | HR               |
employees 테이블에서 부서별로 평균 급여를 계산하고

인라인 뷰의 department_id를 기준으로 부서명을 서브쿼리로 조회함
```

| 항목               | 스칼라 서브쿼리            | 인라인 뷰                     |
| ------------------ | -------------------------- | ----------------------------- |
| **위치**           | SELECT / WHERE 절          | FROM 절                       |
| **반환 결과**      | 단일 값 (1행 1열)          | 다중 행/다중 열 (임시 테이블) |
| **사용 목적**      | 각 행마다 값 계산          | 데이터를 가공하여 요약/집계   |
| **별칭 필요 여부** | 보통 필요 없음             | 반드시 별칭(Alias) 지정 필요  |
| **실행 방식**      | 메인 쿼리 행마다 반복 실행 | 서브쿼리 결과를 한 번 계산    |
