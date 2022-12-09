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

# 2.3 Mutation Type

1> GraphQL에 대한 대부분은 데이터 fetching이지만, 서버 측 데이터를 수정할 수 있는 방법이 필요합니다.
서버 측 데이터를 수정하는 모든 작업은 mutation을 통해 보내야 한다는 규칙을 설정하는 것이 유용합니다.
2> Mutate는 DB의 상태를 변경하려고 할 때 보내는 작업입니다.
3> Query는 DB에서 데이터를 가져올 때 사용합니다.

# 2.4 Non Nullable Fields

1> ' ! '에 대해서 배우기
2> Lists and Non-Null
=> 아래 Character에 name에 string 타입을 사용하고, 느낌표 !를 추가하여 Non-Null로 표시한다.
=> Non-Null로 표시하게 되면 서버가 항상 이 필드에 대해 null이 아닌 값을 반환할 것으로 예상한다. 그래서 null 값을 얻게 되면 클라이언트에게 문제가 있음을 알린다.
3> https://graphql.org/learn/schema/#lists-and-non-null

# 2.5 Recap

1> 아폴로 서버를 실행하기 위해서는 바드시 최소 1억개의 Query가 필요하다.
2> type Quary는 가장 기본적인 타입이다.
=> 모든 graphql 서버에서 required인 type이다.
3> Query에 넣는 필드들은 request할 수 있는 것들이 됩니다.
4> !를 쓰지 않으면 해당 필드는 nullable field가 됩니다.(null값을 가질 수 있는 필드)

# 2.6 Query Resolves

1> resolver 함수는 데이터베이스에 엑세스한 다음 데이터를 반환한다.
2> args는 graphql 쿼리의 필드에 제공된 인수다.
3> https://graphql.org/learn/execution/#root-fields-resolvers

# 2.7 Mutation Resolvers

1> mutation type에 대한 resolver를 만들고 싶을 때
2> variables를 전달할 수 있도록 graphql 코드를 자동으로 만들어준다.(localhost:4000에서)

# 2.8 Type Resolvers

1> 어떤 type 내부의 어떤 field든 resolver function을 만드는 법
2> Resolver arguments
=> Resolver 함수에는 parent(root or source).args, context, info의 네 가지 인수가 순서대로 전달된다.
3> User: {
fullName: (parent, args, context, info) => {
return "hello";
},
},
4> https://www.apollographql.com/docs/apollo-server/data/resolvers/#resolver-arguments

# 2.9 Relationships

1> Users와 Tweets를 연결해 보기
2> resolvers의 첫 번째 인수 데이터가 어떻게 DB 데이터로 전달 받는지 정리

- gql에서 개발자가 정의한 type(Tweet)을 data type으로 사용하는 type(allTweet, tweet(id:ID!))에서 반환한 데이터(tweets DB)를 첫 번째 인자 (Tweet({id, text, userid}, seconParam))로 받는 것
- type resolver의 첫 번째 인자는 해당 type을 data type으로 사용하는 상위 type의 resolvers가 반환한 데이터를 전달 받는 것
- 강의 영상을 보면, author resolver가 받는 userid는 Tweet을 data type을 사용하는 모든 resolvers의 반환값의 요소로 사용되고 있으며, 모든 resolvers의 반환값이 tweets DB으로 귀결되는 걸 확인할 수 있다.
  3> 코드 챌린지
  => 트윗 생성 전에 user 데이터베이스에 userId에 해당하는 유저가 존재하는지 체크 후, 없다면 에러를 띄우거나 트윗을 생성하지 않도록 하기
  => postTweet(root, {text, userId}){
  const findUser = users.find((user) => user.id === userId);
  if(!findUser) return false;
  const newTweet = {
  id : tweets.length + 1 ,
  text
  }
  tweets.push(newTweet)
  return newTweet;
  },

# 2.10 Documentation

1> localhost:4000으로 이동하면, graphql studio로 오게 된다.
2> Schema에는 나의 API의 documentation이 있다.
3> Docstring(Schema-Reference)

- type, field 또는 argument에 대한 설명을 제공한다.
- Docstring은 apollo studio explorer를 포함한 많은 일반적인 graphql 도구에 자동으로 나타난다.

4>
"""
User에 대해 설명
"""
type User{
"""
firstName에 대해 설명
"""
firstName: String!
age (
"""
반드시 숫자여야 합니다.
"""
arg: int
)
}
5> https://www.apollographql.com/docs/resources/graphql-glossary/#docstring
6> Altair GraphQL Client

- AGC는 GraphQl queries 및 implementations을 디버그할 때 사용할 수 있다.
- 추가적으로 파일 업로드 기능을 제공
  7> https://altair.sirmuel.design/
