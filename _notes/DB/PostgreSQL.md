

인덱스가 제대로 활요이 되는지 확인하려면 EXPLAIN ANALYZE를 사용해서 쿼리 실행 계획을 봐야 함.

```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';
```

만약 실행 계획에서 Index Scan 또는 Index Only Scan이 나오면 인덱스가 잘 적용된 것
![[Pasted image 20250402225651.png]]
Seq Scan(Sequential Scan : 풀스캔)이 나오면 여전히 풀 스캔이 발생하는 거라서 원인을 찾아야 한다

컬럼에 UNIQUE 제약 조건이 있다면, PostgreSQL은 내부적으로 유니크 인덱스를 자동으로 생성함
즉, UNIQUE 조건은 INDEX 생성 없이도 조회 성능이 향상된다.

자주 조회되는 패턴이 있다면 패턴에 맞춰서 인덱스를 튜닝할 수 있다
이메일을 WHERE email LIKE 'test%' 이런 식으로 검색하는 경우는 일반 인덱스로 최적화가 안됨

이런 경우, GIN 또는 Hash Index를 사용할 수도 있다
```sql
CREATE INDEX idx_user_email ON users(email text_pattern_ops);
```

```sql
CREATE INDEX idx_user_email_hash ON users USING hash(email);
```
(해시 인덱스는 비교만 빠름)

email 뿐만 아니라 status 같은 컬럼도 함께 자주 검색된다면, 복합 인덱스를 생성할 수 있다
```sql
CREATE INDEX idx_user_email_status ON users(email, status);
```
이렇게 하면 WHERE email = 'test.test.com' AND status = 'ACTIVE' 같은 쿼리에 최적화된다.

인덱스는 조회 성능을 높여주지만, insert, update, delete 성능은 떨어뜨릴 수 있으니
너무 많은 인덱스를 만들면 오히려 성능이 나빠질 수 있다 잘 고려 하자.

만약 인덱스를 생성했는데 인덱스 적용이 안된다면  밑 명령어를 작성해야 함
```sql
ANALYZE users;
```
ANALYZE 역할은 테이블의 데이터 분포를 갱신한다. 새로운 인덱스가 추가되었을 때 실행하는 게 좋다
그렇지 않으면 예전 통계를 기반으로 조회가 될 수 있다.

참고! 데이터 갯수가 많지 않으면 인덱스를 추가해도 Seq Scan이 나올 수 있다
PostgreSQL은 항상 가장 빠른 실행 방법을 자동으로 선택하는데 데이터가 적을 경우, 전체 테이블을 스캔하는 비용이 인덱스를 사용하는 것보다 더 낮을 수 있다 이럴 경우엔 인덱스를 무시하고 풀스캔을 선택한다.