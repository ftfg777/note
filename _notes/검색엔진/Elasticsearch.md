JSON형식으로 데이터를 저장하고 검색할 수 있어서 NoSQL DB처럼 활용할 수 있는 검색 엔진

MySQL 같은 RDB는 정확하고 신뢰성 있는 데이터 저장이 강점
Elasticsearch는 빠르고 강력한 검색과 분석이 강점

|            | **Elasticsearch**     | **일반적인 데이터베이스 (MySQL, PostgreSQL 등)** |
| ---------- | --------------------- | ------------------------------------- |
| **주요 역할**  | 검색 및 분석 엔진            | 데이터 저장 및 관리                           |
| **저장 방식**  | JSON 문서 기반 (NoSQL)    | 테이블 기반 (SQL)                          |
| **데이터 구조** | 동적 스키마 (Schema-less)  | 고정된 스키마 (Schema-based)                |
| **쿼리 방식**  | 검색(DSL) 및 필터링         | SQL                                   |
| **성능 최적화** | 역색인 (Inverted Index)  | 인덱스 및 조인                              |
| **주요 특징**  | 빠른 검색, 분석, 실시간 데이터 처리 | 정합성 보장, 트랜잭션 지원                       |

저장 방법
**Elasticsearch**는 JSON 문서형태로 데이터를 저장한다.

MySQL 테이블 구조
```Sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    category VARCHAR(255),
    price DECIMAL(10,2)
);
```

Elasticsearch 문서 구조
```Json
{
  "id": 1,
  "name": "MacBook Pro",
  "category": "Laptop",
  "price": 2500.00
}
```
이런 JSON 문서들이 Index 안에 저장된다

사용목적
검색과 분석이 필요한 경우에 최적화되어있다.
1. 빠른 검색이 필요할 때
	1. 쇼핑몰 상품 검색
	2. 뉴스, 블로그, 문서 검색
2. 대량의 로그 데이터를 분석할 때
	1. 서버 로그
	2. 애플리케이션 로그 저장 & 분석
3. 실시간 데이터 분석
	1. 실시간 대시보드
	2. 통계 분석 (Kibana와 함께 사용)




Elasticsearch 8.17.3 버전에서는 range()에서 바로 .field() 사용 불가**

untyped() 또는 number()를 써야 함

• untyped() → 일반적으로 사용 가능

• number() → 숫자 타입 필드에만 사용 가능

최종적으로 Query 객체를 만들어서 SearchRequest에 넣으면 됨.


데이터 1만개를 삽입해서 검색 속도를 조회해봤음

엘레스틱서치
get http://localhost:8080/elastic?category=Laptop&minPrice=100&maxPrice=500&page=0&size=10
50ms 아래로 떨어짐

jpa + mysql
get http://localhost:8080/products/search/mysql?category=Laptop&minPrice=100&maxPrice=500&page=0&size=10
100ms아래로 떨어지지 않음


발생한 오류들
Caused by: co.elastic.clients.json.JsonpMappingException: Error deserializing co.elastic.clients.elasticsearch.core.search.Hit: jakarta.json.JsonException: Jackson exception (JSON path: hits.hits[0]._source) (line no=1, column no=366, offset=-1)

원인 : Elasticsearch의 응답을 Java 객체로 역직렬화하는 과정에서 발생한 문제 hits.hits[0]._source부분에서 역직렬화 중 문제가 발생

이는 응답의 JSON 구조와 Java 객체 간의 불일치로 인해 발생한다고 한다.

이 오류를 해결하기 위해 다음 단계를 시도해볼 수 있다

1. **JSON 구조 확인**: Elasticsearch로부터 받은 JSON 응답의 구조가 Java 객체의 예상 구조와 일치하는지 확인 오류 메시지는 _source 필드에서 발생했다고 언급하고 있으므로, _source 안의 필드들이 해당 Java 클래스의 필드들과 일치하는지 점검

2. **Jackson 설정 확인**: Jackson을 사용하여 역직렬화를 처리하는 경우, Java 클래스의 필드에 대해 적절한 어노테이션 (@JsonProperty, @JsonIgnoreProperties)이 적용되어 있는지 확인 @JsonCreator를 추가하여 생성자를 이용한 역직렬화를 시도할 수도 있음

3. **JSON 응답 디버깅**: Elasticsearch에서 반환된 원본 JSON 응답을 로깅하여 어떤 값이 실제로 반환되는지 확인. 때로는 응답에서 누락된 필드나 예상치 못한 구조로 인해 문제가 발생할 수도 있음

4. **Elasticsearch 클라이언트 호환성 확인**: 사용하는 Elasticsearch Java 클라이언트 버전이 Elasticsearch 서버 버전과 호환되는지 확인 버전 불일치가 역직렬화를 일으킬 수 있음

5. **커스텀 역직렬화기 사용**: 응답 구조가 복잡하거나 변동이 있을 경우, 문제를 일으키는 필드에 대해 커스텀 역직렬화기를 구현할 필요가 있을 수 있음

6. **타입 확인**: Java 클래스의 필드 타입이 Elasticsearch 응답에서 반환되는 데이터 타입과 일치하는지 확인 예를 들어, String 타입 필드에 List나 Map 같은 다른 타입의 데이터를 역직렬화하려고 하면 문제가 발생.

먼저 응답 구조를 확인하기 위해
 curl -X GET "localhost:9200/products/_search?pretty=true"
위 명령어를 입력해 확인을 했다
![[Pasted image 20250320131831.png]]

응답 구조를 확인해 보니 _source필드엔 id, name, category, price와 같은 Java객체와 동일한 필드가 존재했지만  _class필드도 함께 포함되어 있었다

혹시 저게 문제가 아닐까 싶어서
ProductDocument 클래스 파일에
@JsonIgnoreProperties 어노테이션을 달아주었더니 성공적으로 요청이 이루어졌다!