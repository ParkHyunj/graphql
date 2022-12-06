# graphql

# 1. Setup

1> npm init -y
=> node repository 초기화
2> npm i apollo-server graphql
=> apollo-server와 graphql 설치  
3> npm i nodemon -D
=> 더 나은 개발을 위해
4> npm run dev 시 nodemon은 작동중이며, server.js를 저장할 때마다 서버를 재시작 시킨다.
5> Error: Apollo Server requires either an existing schema, modules or typeDefs

# 2.1 Query Type

1> rest API는 많은 url들의 집합
2> const typeDefs = gql''(무조건 '')
=> graphql의 schema definition language
=> ''안에서는 graphql한테 data의 shape를 설명해야한다.
3> 모든 graphql API는 query를 가진다.

# 2.2 Scalar and Root Types

1> Brave 브라우저 apollo 서버 Fields가 보이지 않는 경우

1. chrome등 다른 브라우저를 사용한다.
2. Brave Shields 비활성화 (Brave 브라우저인 경우)

- apollo 서버 접속후 주소표시줄 우측 사자모양 아이콘 클릭
- 토글버튼을 클릭해서 Shields 비활성화
  2> Scalar types
  => GraphQL 객체 타입에는 이름과 필드가 있지만 이 필드는 더욱 구체적인 데이터로 해석되어야 합니다. 그 때 스칼라 타입을 사용할 수 있습니다.
  3> GraphQL은 기본 스칼라 타입 세트와 함께 제공됩니다.
  => ID : ID 스칼라 타입은 객체를 다시 가져오거나 캐시의 키로 자주 사용되는 고유 식별자를 나타냅니다.
  4>
