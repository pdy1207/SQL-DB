### !!!! SQL 순서 1. from 1-1 join 2. where 3. group by 4. having 5. select 6. order by !!!!

    	데이터 베이스 (db)

 	- 관계형 데이터 베이스 (Oracle, Mysql ....) 그 중 공부하고있는것... : 관계가 있다. 관계 (==join) , 삭제가 엄격함
	- 비관계형 데이터베이스 (MongoDB, NoSQL, DynamoDB) : 말 그대로 관계가 없다.
	- 빅데이터 데이터베이스 (하둡)	 
	- 시계열 데이터베이스 

### SQL 

    DML(not auto commit) : 
	SELECT , UPDATE, DELETE, INSERT

	* 디비버, 워크벤치 프로그램은 
	  DML이 오토커밋으로 설정되어 있어 
	  해제하고 작업해야 함. 
	  (!!!dbeaver auto commit 해제!!!)

	DDL(auto commit) : 
		CREATE, ALTER, DROP
	DCL(auto commit) : 
		GRANT, REVOKE

    
### SQL 실행 순서!!!


     having 과 where 차이점
	1. SQL 실행 순서가 다르다. 
	2. where 조건에 집계함수(count, max, min, avg ...) 으로 비교 불가능
	3. having은 집계함수 비교가능 
	-- group by된 결과를 필터링 하고싶을 때 사용
	* WHERE랑 HAVING을 헷갈리는 경우
	WHERE는 그룹화 하기 전이고, HAVING은 그룹화 후에 조건
	-- order by : 특정 컬럼을 정렬할 때 사용(항상 마지막에 실행)
