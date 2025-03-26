

GraphQL API의 주요 특징

| **특징**                        | **설명**                                |
| ----------------------------- | ------------------------------------- |
| **필요한 데이터만 요청 가능**            | Over-fetching & Under-fetching 해결     |
| **하나의 엔드포인트로 모든 요청 처리**       | /graphql 하나의 엔드포인트만 필요                |
| **강력한 타입 시스템 (Schema 기반)**    | API 명세가 명확하고 안전함                      |
| **실시간 데이터 지원 (Subscription)** | WebSocket을 통해 실시간 데이터 제공              |
| **요청 & 응답이 JSON**             | JSON 기반으로 일관성 유지                      |
| **개발자 도구 지원**                 | GraphiQL, Apollo Sandbox 등으로 테스트 가능   |
| **캐싱이 어려움**                   | REST보다 캐싱이 어렵지만, Apollo Client로 해결 가능 |

필요한 데이터를 받으려면 여러 엔드포인트를 호출해야 할 수도 있는 REST API 와는 다르게
GraphQL에서는 하나의 엔드포인트로 모든 데이터 요청이 가능하다.

graphql:
  servlet:
    mapping: /api/query
application.yml에서 엔드포인트 변경 가능

또한, 클라이언트가 원하는 데이터만 요청이 가능하다.

GraphQL은 스키마를 먼저 정의하고, 이 스키마에 따라 API가 동작한다
API가 어떤 데이터를 제공하는지, 요청 가능한 필드는 무엇인지 명확하게 알 수 있는 장점이 있다.

별도의 API 문서가 필요 없이 스키마를 보면 어떤 데이터가 반환되는지 바로 알 수 있고
클라이언트가 잘못된 요청을 보내면 GraphQL이 자동으로 에러 처리를 한다.

REST API는 보통 폴링(Polling)방식으로 실시간 데이터를 가져오는데
GraphQL의 Subscription을 사용하면 WebSocket을 통해 실시간 데이터 제공이 가능하다.

REST API처럼 여러 포맷(XMl, JSON)이 혼용되지 않고 요청도, 응답도 JSON형식으로 일관성이 있다.

다만, REST API는 GET / books/ 1 같은 URL을 기반으로 브라우저나 CDN에서 캐싱이 가능한데 GraphiQL은 요청이 동적이어서 일반적인 캐싱이 어렵다.

대신  Apollo Client 같은 라이브러리를 사용하면 클라이언트에서 캐싱 가능하다




