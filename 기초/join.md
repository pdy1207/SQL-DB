 - join
   - 관계형 데이터베이스(my SQL, oracle, Tibero ...)를 사용하면 join은 무조권 사용한다
   - depno : 부서 번호 dname : 부서 이름 loc : 부서 위치
   - 조인은 컬럼이름이 같다고 해서 되는게 아니라, 데이터 타입이 서로 같아야한다.
   - 컬럼 이름이 같은 이유는 사용자(개발자) 편리성을 위해서 같게 해준다.

 - join 문법
   - 테이블 이름에도 as를 사용할 수 있다.

 
 
          select e.ENAME,e.DEPTNO , d.DNAME  from emp as e
          inner join dept as d
          on e.DEPTNO  = d.DEPTNO 
        
        
 - 방법2. (추천 x)
    - where 조건으로도 사용할 수 있지만 
    - where가 나온 목적은 연산자(비교)를 이용해서 필터링을 하는게 목적이다.
    - 때문에 아래 방법보다는 방법1로 join을 사용하자.


        select e.ENAME,e.DEPTNO , d.DNAME  from emp as e,
        dept as d
        where e.DEPTNO = d.DEPTNO 
        
        
==========================================================================
 - 사원번호가 7788인 사원의 이름, 직책, 부서번호, 부서이름, 근무지역 조회하시오


     - 조인 팁 : 두 테이블 교집합 컬럼을 찾자


            select e.EMPNO ,e.ENAME , e.JOB ,d.DEPTNO , d.DNAME ,d.LOC 
            from emp as e
            inner join dept as d
            ON e.DEPTNO = d.DEPTNO 
            where e.EMPNO = 7788

  - 부서별로 그룹핑을 하고 부서번호와 부서이름을 조회하시오.
      - join문법은 from과 where 사이에 온다.


            select e.DEPTNO , d.DNAME  
            from emp as e
            inner join dept as d
            ON e.DEPTNO = d.DEPTNO 
            group by e.DEPTNO 

 - 직책이 manager인 사원들의 이름과 부서 이름, 부서 위치를 조회


          select e.ENAME as "사원이름"
              ,d.DNAME as "부서 이름"
              ,d.LOC  as "부서 위치"
          from emp as e
          inner join dept as d 
          on e.DEPTNO = d.DEPTNO
          where e.JOB = 'MANAGER'
          
          
- inner join에서 순서는 상관 없지만
    - right join과 left join은 상관 있다.
        - left join(차집합), right join : 아우터(outer) 조인


 - 40번 부서만 조회


          select * from dept where DEPTNO = 40;
          
          
- 만약에 emp테이블에 없는 부서번호 조회


          select * from emp as e
          right join dept as d 
          on d.DEPTNO = e.DEPTNO 
          where e.EMPNO is null

- self join (inner join하고 같음)
    - 그러나 자기 자신을 조인함. 즉 , 1개 테이블을 사용
    - boss : 상사 , underling : 부하

          select boss.EMPNO  as '상사 번호',
          boss.ENAME as '상사 이름',
          underling.EMPNO  as '부하 직원 번호',
          underling .ENAME  as '부하 직원 이름'
          from emp as boss
          inner join emp as underling
          on boss.EMPNO = underling.MGR 

- emp에 insert 하기


          insert into emp (empno, ename,job,sal,HIREDATE)
          values (8000, '손흥민','SALESMAN',7000, now());


- 문제. 아우터 조인(left or right) 이용하기
    - 부서에 소속되어 있지 않은 사원 번호, 이름 ,입사날짜 조회


          select e.EMPNO as '사원번호',
               e.ENAME as '사원이름',
               e.HIREDATE as '입사날짜'
          from emp as e 
          left join dept as d 
          on e.DEPTNO = d.DEPTNO 
          where d.DEPTNO is null

- 사원번호가 8000인 사원의 급여를 8000으로 업데이트하시오
      -  delete 는 from 사용 update는 사용 x 


          update emp 
          set sal = 8000
          where EMPNO = 8000
