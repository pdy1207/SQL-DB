### SQL?
    SQL은 관계형 데이터베이스 데이터를 관리하기 위한 명령어 혹은 프로그래밍 언어.
    명령어로 데이터를 저장, 삭제, 수정, 조회함.

### 데이터베이스
    데이터베이스는 크게 관계형 데이터베이스와 비관계형 데이터베이스가 존재.


### 서브 쿼리(메인쿼리 안에 서브쿼리가 옴)
    서브쿼리란? 하나의 쿼리 문장 내에 포함된 또 하나의 쿼리 문장.
    서브 쿼리가 오는 위치 (== 많이 사용하는 위치)
    
     1. select(스칼라 서브쿼리)
     2. from (*** 인라인 뷰)
     3. where(중첩 서브쿼리) 

        SELECT COUNT(empno) AS "empCount",
        (SELECT ROUND(AVG(sal)) FROM emp) AS "empSalAvg",
        (SELECT COUNT(DEPTNO)  FROM dept) AS "deptCount",
        (SELECT ROUND(SUM(comm))  FROM emp) AS "empCommSum"	
        FROM emp
