##### 1. 사원이름, 사원직책, 사원급여 조회.


        select ENAME, job, sal 
        from emp

##### 2. 사수번호가 7839인 사원 번호, 이름, 입사날짜 조회.
        select DEPTNO,ENAME,HIREDATE 
        from emp

##### 3. 급여가 3000 이하인 사원의 모든 정보 조회.
      select * 
      from emp
      where sal <= 3000

##### 4. 사원이름, 부서번호, 부서이름, 부서 근무지 조회.
        select e.ENAME, e.DEPTNO, d.DNAME, d.LOC  
        from emp as e
        inner join dept as d 
        on e.DEPTNO = d.DEPTNO

##### 5. 부서별 급여합계, 부서이름 조회.
        select 
          sum(sal) as '급여합계',
          d.DNAME as '부서이름'
        from emp as e
        inner join dept as d 
        on e.DEPTNO = d.DEPTNO
        group by e.DEPTNO 

##### 6. 부서 근무지가 NEW YORK이고, 직책이 MANAGER인 
#####   사원의 이름, 급여를 조회. 
        select 
          e.ENAME as "사원이름",
          e.SAL as "급여"
        from emp as e
        inner join dept as d
        on e.DEPTNO = d.DEPTNO
        where d.LOC = "NEW YORK" and e.JOB = "MANAGER"

##### 7. 1983년 이후 입사한 사원의 보너스가 null
 #####  이면 100 주고, 사원의 이름, 부서이름, 직업을 조회. (ifnull 검색하기)
        SELECT IFNULL(COMM , 100),
          e.ENAME as "사원이름",
          d.DNAME as "부서이름",
          e.JOB as "직업"
        FROM emp as e
        inner join dept as d
        on e.DEPTNO = d.DEPTNO 
        where HIREDATE >= "1983-01-01"

##### 8.  부서명이 RESEARCH인 사원의 이름, 급여, 근무 지역 조회.
        select 
          e.ENAME as "사원이름",
          e.SAL as "급여",
          d.LOC as "근무지역"
        FROM emp as e
        inner join dept as d
        on e.DEPTNO = d.DEPTNO
        where d.DNAME = "RESEARCH"

##### 9. 보너스를 받은 사원 이름, 직책, 급여, 부서명 조회.
        select 
          e.ENAME as '사원이름',
          e.JOB as '직책',
          e.SAL as '급여',
          d.DNAME as '부서명'
        FROM emp as e
        inner join dept as d
        on e.DEPTNO = d.DEPTNO
        where e.COMM is not null

##### 10. 이름 첫글 A자를 가진 사원 이름, 직책, 부서명, 부서 위치 조회.
        select 
          e.ENAME as '사원이름',
          e.JOB as '직책',
          d.DNAME as '부서명',
          d.LOC as '부서위치'
        FROM emp as e
        inner join dept as d
        on e.DEPTNO = d.DEPTNO
        where e.ENAME like 'A%'

##### 11. 사원명, 사수번호, 사수 이름 조회.
#####           단, 사수가 없는 사원도 포함
        select 
          underling.ENAME as '사원명',
          underling.MGR as '사수번호',
          boss.ENAME as '사수 이름'

        from emp as boss
        right join emp as underling
        on boss.EMPNO  = underling.MGR

##### 12. 사원명, 사수번호, 사수 이름 조회.
#####           단, 사수가 없는 사원만
        select 
          underling.ENAME as '사원명',
          underling.MGR as '사수번호',
          boss.ENAME as '사수 이름'

        from emp as boss
        right join emp as underling
        on boss.EMPNO  = underling.MGR
        where underling.MGR is null

##### 13. 상사번호가 7698인 사원의 이름, 사원번호, 상사번호, 상사이름 조회.
        select 
          underling.ENAME as '사원명',
          underling.empno as '사원번호',
          underling.MGR as '상사번호',
          boss.ENAME as '사수 이름'

        from emp as boss
        right join emp as underling
        on boss.EMPNO  = underling.MGR
        where underling.MGR = "7698"

##### 14. 상사보다 먼저 입사한 사원의 사원이름, 사원의 입사일, 상사 이름, 상사 입사일 조회.
        select 
          underling.ENAME as '사원명',
          underling.HIREDATE as '사원 입사일',
          boss.ENAME as '상사 이름',
          boss.HIREDATE  as '상사 입사일'
        from emp as boss
        right join emp as underling
        on boss.EMPNO  = underling.MGR
        where underling.HIREDATE  > boss.HIREDATE  

##### 15. 업무가 MANAGER이거나 CLERK고 입사날짜가 1982년에 입사한
##### 사원의 사원번호, 이름, 급여, 직업, 부서명 조회.
        select 
          e.EMPNO as '사원번호',
          e.ENAME as '사원이름',
          e.SAL  as '급여',
          e.JOB as '직업',
          d.DNAME as '부서명',
          e.HIREDATE as '입사날'
        from emp as e
        inner join dept as d
        on e.DEPTNO = d.DEPTNO 
        where e.JOB = "manager" or e.JOB = "CLERK"
        having date_format(HIREDATE,'%Y') = '1982'

##### 16. 부서별 급여 총합 조회. 
#####     단, 사원이 존재하지 않는 부서도 포함해서 급여 순으로 내림차순 하시오.
        select 
          sum(e.sal) as '급여 총합' ,
          d.DEPTNO as '부서번호',
          d.DNAME as '부서이름'
        from emp as e
        right join dept as d
        on e.DEPTNO = d.DEPTNO
        group by d.DEPTNO
        order by sum(e.sal) desc

##### 17.  사원 이름, 상사 이름, 사원 부서번호, 사원 부서명, 사원 근무지역 조회. 
 #####      단, 사원이 존재하지 않는 부서번호와 부서명도 조회.
 
 
        select 	
          z.ENAME as '사원이름',
          e.ENAME as '상사 이름',
          e.DEPTNO as '사원 부서번호',
          d.DNAME as '사원 부서명',
          d.LOC as '사원 근무지역'
        from emp as e
        inner join emp as z
        on e.EMPNO = z.MGR 
        right join dept as d
        on e.DEPTNO = d.DEPTNO
        group by d.DEPTNO

##### 18. 부서 위치가 CHICAGO이고 사수 급여가 5000 미만인 
#####     사원 번호,사원 이름,사수 번호, 사수 이름, 사수 급여, 부서명을 조회.
#####     단, 사원의 입사날짜로 오름차순.
          select 
            bu.EMPNO as '사원 번호',
            bu.ENAME as '사원 이름',
            bu.MGR as '사수 번호',
            e.ENAME as '사수 이름',
            e.SAL as '사수 급여',
            d.LOC as '부서명'
          from emp as e
          inner join emp as bu
          on e.EMPNO = bu.MGR 
          inner join dept as d
          on e.DEPTNO = d.DEPTNO
          where d.LOC = 'CHICAGO'
          having e.sal < 5000
          order by e.HIREDATE 

##### 19. 입사날짜를 월별로 몇명이 입사했는지 카운트해서 조회.

          SELECT
            DATE_FORMAT(HIREDATE , '%Y-%m') as 'date',
            COUNT(*) as 'count'
          FROM emp
          GROUP BY MONTH(HIREDATE), YEAR(HIREDATE)
          ORDER BY 'date' DESC
