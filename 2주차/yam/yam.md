### 라우팅 구조

`next.js` 에서는 개별적으로 `route.js` 와 같은 파일을 만들어 라우팅을 관리하는게 아닌,
폴더구조를 이용해 라우팅을 관리한다.
`app` 폴더안의 파일과 폴더들을 인식하여 자동으로 라우팅을 해주며,
각 중첩폴더마다 `page.js` 파일이 기본값으로 반환됨

`pages/document/index.js >> localhost:8080/document`

<hr style="height:5px">

14버전 미만인 리액트와 차이점은
`index.js`가 아닌 다른 파일을 생성하면 그 주소로 접속이 되지 않았음.
무조건 page.js를 이용해야하나?

즉 아래처럼 이용해야함
13v : `pages/document/abc.js >> localhost:8080/document/abc`
14v : `pages/document/abc/page.js >> localhost:8080/document/abc`

<hr style="height:5px">

### 동적 라우팅

위 <strong>라우팅 구조</strong> 단락에서 소개한 예시들은 `정적 라우팅` 이다.
동적 라우팅이란, 사용자들이 접속하는 url의 경로를 개발자가 직접적으로 명시하는 것이 아닌,
상황에 맞게 바뀔수 있는 것을 말한다.

예를 들어
`localhost:8080/document/고기`
위 주소로 접속했을때 화면에 `고기` 라는 텍스트가 표현된다고 하자.

그럼 개발자는 `고기` 폴더를 `app` 폴더 내부에 생성했을까?
물론 그럴 가능성도 있겠지만,
document 아래에 중첩 라우팅이 가능하게 폴더/파일 을 배치하여
사용자가 접속한 경로를 보여주는 것일 수 도 있다.

동적라우팅을 하려면?
13버전과 달리 폴더이름을 대괄호로 묶어 생성해주면 됨
`localhost:8080/document/[slug]/page.js >> document/아무말`

이 방식은 13버전과 달라 조금 헷갈릴수 있겠다 싶음..
처음쓰는데도 헷갈림
그냥 파일로 해버리지.

<hr style="height:5px">

### Catch-All 라우팅 (동적 라우팅 2)

위 단락의 동적라우팅은 마지막 경로를 제외한 상위 경로가 개발자에 의해 이미 정해져있었음
즉 `a/b/c/d` 경로라면
실제 파일배치가 `a/b/c/[slug].js/page.js` 로 되어있고,
`a/b/c` 까지의 경로는 정해지게 되어버림

하지만 여러 경로를 한번에 동적으로 받고싶을때 사용하는 방법이 있음
`[slug] >> [...slug]` 로 폴더 문법을 바꾸면 됨

이렇게 바꿔버리면~~~~~
`a/page.js` 로 파일배치를 하더라도
`a/b/c/d/e` 경로로 접속하든 뭘하든 접속가능

물론 라우트에 대한 예외처리는 필요할 것.

<hr style="height:5px">

### 우선순위

위 내용을 다 읽고 나서 한가지 의문점이 들 수 있음

`a/b/c/page.js`
`a/[...slug.js]/page.js`

위 두 파일이 있다면
`a/b/c` 경로로 접속했을때 어떤 파일이 반환될까?
답은 `명시적으로 선언한 순서` 임
그래서 `a/b/c/page.js` 가 반환됩니다.

<hr style="height:5px">

### next.js 14

pages 폴더를 이용해 route를 진행한다했는데 프로젝트 생성시 pages가 보이지않고
`index.js` 가 아닌 `page.js`를 기본페이지로 잡고 서버에서 반환해줌.

버전의 차이일 수 있어 공식문서를 살펴보니 아래의 사진처럼 app안에서 진행하도록 바뀐듯
https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages
![](https://velog.velcdn.com/images/diacl4927/post/aa926c5c-5663-4414-8cec-a1c163b77428/image.png)

기존버전의 폴더가 `/pages/abc/b/index.js` 로 잡혀있었다면.
`/abc/b` 로 접근했을때 `index.js`가 반환됨.

허나 현재버전은 `/app/abc/b/page.js` 로 구조를 잡아놓아야
`/abc/b` 로 접근했을때 `page.js` 가 반환됨.

<hr style="height:5px">

소스도 작성해 올릴랬는데 딱히 올릴만한게 없네..
본문 내용으로도 충분
