개념

 - select : 조회할 때 사용
 - selct <컬럼이름> from <테이블 이름>

        select ename from emp
        
 - 사원 이름, 번호 조회 
 - 1개 이상 컬럼을 조회할 때는 , (콤마) 사용


        select ename, EMPNO  from emp

 - 사원번호, 사원이름, 직책 조회


        select ENAME , EMPNO , JOB  from emp
        
 - as (별칭)


        select ENAME as'사원이름', EMPNO as '사원번호' from emp
 - 모든 컬럼조회 * (아스테리스크)


        select * from emp

 - where (필터링)
 - 20번 부서 사원 모두 조회
 - 쿼리 순서 : 1. from 2. where 3. select 


        select * from emp where deptno = 20;

 - 문제1. job 이 manager 인 사원이름, 사원번호, 직책, 입사날짜 조회하시오


            select ENAME,EMPNO,HIREDATE,JOB from emp  where JOB = 'manager';

 - 문제2. job 이 manager, SALESMAN인 사원번호, 사원이름 조회
 - or(||), and(&&) or은 둘중에 하나만 true 이면 됨 and 는 둘다 !! 


          select ENAME,EMPNO from emp where JOB = 'manager' or JOB = 'salesman';

 - 문제3. 사원이름이 allen인 사원의 이름, 직책, 입사날짜 조회


          select ENAME,JOB,HIREDATE from emp where ENAME = 'ALLEN';

 - 사원이름이 a로 시작하는 사원의 이름, 사원 번호 조회
 - LIKE : 특정 단어를 검색할 수 있다.


          select ENAME,EMPNO  from  emp where ENAME like 'A%';

 - 사원 이름에 L이 두번 들어간 사원 이름, 번호 조회 


           select ENAME,EMPNO  from  emp where ENAME like '%L%L%';

 - 보너스를 받지 못한 사원의 급여와 번호를 조회
 - is null 의 반대는 is not null


          select SAL, EMPNO from emp where COMM is null;
          select SAL, EMPNO from emp where COMM is not null;

 - 입사날짜가 1987-06-28 이상인 사람들 사원 이름, 번호, 직책 조회
 -    >= , <= , > , <


          select ENAME ,EMPNO ,JOB,HIREDATE  from emp  where HIREDATE >= '1987-06-28';

 - 문제4. 입사일이 1980-12-17 ~ 1982-01-23 사이에 입사한 사원의 이름, 번호, 날짜, 직책을 조회


          select ENAME,EMPNO ,HIREDATE,JOB  from emp where HIREDATE >= '1980-12-17' and  HIREDATE <= '1982-01-23';

 - 문제5. 직업이 manager고, 급여가 1300이상 받는 사원번호, 이름, 급여, 직업 조회


          select ENAME,EMPNO,SAL ,JOB  from emp where JOB = 'manager' and SAL >= 1300;

 - avg,count, max, min 함수 (단일행 함수)
 - 직업이 manager인 사원들의 급여 평균 조회 


          select avg(sal) as "급여 평균",JOB as "직업"  from emp where JOB ='manager';

 - 직업이 clerk인 사원 수 조회


          select count(EMPNO) as "사원 수" from emp where JOB = 'clerk';


          select max(sal)  from emp where JOB = 'clerk';
           - max
          select min(sal) ,ENAME  from emp where JOB = 'clerk';
           - min

 - 문제6. 입사날짜가 '1987-06-28' 이상인 사원들의 수와 급여 평균 조회


          select avg(SAL) as "급여 평균",count(EMPNO) as "사원들의 수" from emp where HIREDATE >= '1987-06-28';

 - 문제 7. 직책이 'manager' 가 아닌 사원이름, 직책 조회


          select EMPNO,ENAME,JOB  from emp where JOB !='manager';

 - 문제 8. 사원 이름이 'SCOTT', 'JONES'인 사원의 이름,번호,급여,입사날짜 조회
 - 방법 8-1


          select ENAME, EMPNO, SAL,HIREDATE  from emp where ENAME = 'SCOTT' or ENAME = 'JONES';
          
 - 방법 8-2


          select ENAME, EMPNO, SAL,HIREDATE  from emp where ENAME in('SCOTT','JONES');
