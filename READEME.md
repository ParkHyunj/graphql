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
