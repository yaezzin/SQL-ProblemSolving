# SQL-ProblemSolving

## Note

|Command|Description|
|-------|----------|
|`IFNULL(A, B)` | A가 NULL일 경우 B를 출력|
|`A IS NULL`|컬럼 A가 NULL이라면 (WHERE절에 주로 사용)|
|`A IS NOT NULL`|컬럼 A가 NULL이 아니라면 (WHERE절에 주로 사용)|
|`DISTINCT`|중복된 데이터를 제거하고 데이터를 조회|
|`LIMIT N`|N개의 데이터만 조회 (맨 마지막 줄에 사용)|
|`LIMIT N, M`|N부터 M까지의 데이터만 조회 (맨 마지막 줄에 사용)|
|`LIKE 'A%'`|A로 시작하는 문자 찾기|
|`LIKE '%A'`|A로 끝나는 문자 찾기|
|`LIKE '%A%'`|A를 포함하는 문자 찾기|
|`COUNT(A)`|- A의 개수를 리턴 </br> - Null은 숫자로 세지X|
|`AVG(A)`|A의 평균을 리턴|
|`SUM(A)`|A의 합을 리턴|
|`MAX(A)`|- A의 최대값을 리턴 </br> - DATETIME 컬럼을 넣을 경우 가장 최신 날짜를 리턴|
|`MIN(A)`|- A의 최솟값을 리턴 </br> - DATETIME 컬럼을 넣을 경우 가장 오래된 날짜를 리턴|
|`ROUND(N, M)` |- 숫자(컬럼) N을 소수점 M째 자리에서 반올림 </br> - 반올림할 위치에 아무것도 적지 않으면 첫째 자리에서 반올림을 하며, 1을 적을경우부터 둘째자리에서 반올림|
|`CEIL(N)`|숫자(컬럼) N의 소수점 값 상관없이 올림|
|`FLOOR(N)`|숫자(컬럼) N의 소수점 값 상관없이 내림|
|`TRUNCATE(N, M)`|- 숫자(컬럼) N을 M번째짜리 자릿수 '아래'로 버림! </br> - 자릿수를 지정하지 않으면 오류 발생!|
|`DATE_FORMAT(D, F)` | - 날짜 D를 형식 F에 맞게 리턴 </br> - ex) **DATE_FORMAT(NOW(),'%Y-%m-%d')**|
|`YEAR(D)`|날짜 D의 '연도' 값을 리턴|
|`MONTH(D)`|날짜 D의 '월' 값을 리턴|
|`DAYOFMONTH(NOW()`|날짜 D의 '일' 값을 리턴|

#### ⭐ 쿼리 실행 순서

* `FROM` - `WHERE` - `GROUP BY` - `HAVING` - `SELECT` - `ORDER BY`

#### ⭐ 쿼리 적는 순서

* `SELCET` - `FROM` - `WHERE` - `GROUP BY` - `HAVING` - `ORDER BY` - `LIMIT`


## GROUP BY

> 같은 값을 가진 행을 그룹짓는 SQL 명령어

* GROUP BY는 COUNT(), MAX(), MIN(), SUM(), AVG() 등 집계 함수와 함께 사용
* DISTINCT처럼 그룹화하는 과정에서 중복이 제거되는 기능도 하나, 중복제거만을 위해서라면 DISTINCT를 사용하는 것이 좋음

## HAVING

> GROUP BY절에 의해 그룹핑한 행에 대해 원하는 조건에 부합하는 데이터만 보고자 할 때 사용
* WHERE절은 행들이 그룹핑되기 전 단일 행들을 필터링하는 데 사용 = WHERE 절이 GROUP BY 전에 적힘
* HAVING 절은 행들이 그룹핑된 후의 행들을 필터링하는 데 사용 = HAVING 절이 GROUP BY 후에 적힘

#### example) 중복값 조회하기

```sql
SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(USER_ID) > 1 AND COUNT(PRODUCT_ID) > 1
```
1. 중복값이 존재하는지 확인하고 싶은 열을 기준으로 GROUP BY를 실행해 열을 합침
2. HAVING절 안에 COUNT 함수 사용하여 그룹핑된 값의 개수가 1개보다 많은지 확인

## ORDER BY

* 첫번째 컬럼으로 정렬 후 2, ..., N번째 컬럼으로 정렬
* 디폴트는 ```오름차순(ASC)```으로 정렬하며 내림차순 정렬을 할 경우 ```DESC```

## WHERE

|NOT | Description         |
|----|---------------------|
|```!=``` 또는 ```NOT =```| - 조건이 하나인 경우에는 != 또는 NOT col = val 를 사용하자! </br> - 조건을 여러 개 명시할 경우 OR를 사용하는데 OR의 비교가 선형적이라 조건이 많아질수록 효율이 떨어짐|
|```NOT IN()```| - IN에 명시한 값들을 정렬하고 이진 탐색으로 값을 찾기 때문에 훨씬 효율적|

## UNION

> 둘 이상의 테이블의 결과를 결합

* `UNION`의 결과 집합에는 중복 행이 포함되지 않지만 `UNION ALL`의 결과 집합은 두 테이블의 모든 행을 반환(중복값 포함)



