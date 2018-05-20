# DataBase(MySql) 성능 개선

## 분산 데이터베이스

* 여러 곳으로 분산되어있는 데이터베이스를 하나의 가상 시스템으로 사용할 수 있도록 한 데이터베이스


* 논리적으로는 동일한 시스템에 속하지만, 물리적으로는 네트워크를 통해 분산되어 있는 데이터들의 모임
* 물리적 Site 분산, 논리적으로 사용자 통합 공유

## 데이터베이스 성능 개선

![[ê·¸ë¦¼ 5-3-1] ì±ë¥ ì í ìì¸](http://www.dbguide.net/publishing/img/dbguide/edu/071107_c_1.gif)

* ​

![[ê·¸ë¦¼ 5-3-2] ì±ë¥ ê°ì  ì ê·¼ ë°©ë²](http://www.dbguide.net/publishing/img/dbguide/edu/071107_c_101.gif)

* ​

## 테이블 최적화

1. Backup(백업)

2. Check(체크) : 테이블 무결성 검사

   ```
   CHECK TABLE {table name};
   ```

3. Optimize(최적화) : 단편화 제거 작업

   사용하지 않은 공간을 회수할 수 있다.

   InnoDB 엔진의 경우 내부적으로 ALTER TABLE 문을 실행하여 MySql 서버에 대해 테이블과 인덱스를 재성성하도록 요청한다.

   InnoDB라면 결과에 "Table does not support optimize, doing recreate + analyze instead"

   ```
   OPTIMIZE TABLE {table name};
   ```

4. Analyze(분석)

   인덱스를 재생성하여 성능을 최적화, 키를 재분배한다.

   ```
   ANALYZE TABLE {table name};
   ```

   출처 : http://blog.syszone.co.kr/3333

## SQL 쿼리문

## 인덱스 설정

## 클러스터링 인덱스

* Primary Key값이 비슷한 레코드끼리 묶어서 저장
* 프라이머리 키값에 의해 레코드의 저장 위치가 결정
* 프라이머리 키값이 변경된다면 그 레코드의 물리적인 저장 위치가 바뀌어야 한다.

## Sharding(샤딩)

- 단일의 논리적 데이터셋을 다수의 데이터베이스에 쪼개고 나누는 방법

- 데이터셋이 단일 데이터베이스에서 저장하기에 너무 클때 필수적이다.

- 샤딩은 데이터베이스 클러스터가 데이터베이스의 데이터와 트래픽 증가와 함께 스케일을 확장할 수 있게 한다.

  ![img](http://cfile1.uf.tistory.com/image/2724CE4F582ADE5B014BED)

  ### Vertical Sharding

  - 도메인 특화

  ### Horizontal Sharding

  - 튜플 특화
  - 같은 타입의 데이터를 다수의 테이터베이스에 쪼개서 저장하는 것

## 파티션

* MySql 서버의 입장에서는 데이터를 별도의 테이블로 분리해서 저장하지만 사용자 입장에서는 여전히 하나의 테이블로 읽기와 쓰기를 할 수 있게 해주는 솔루션

  ​