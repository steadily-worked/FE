# 프론트엔드 개발자가 알아야되는 HTTP 프로토콜

(출처: <a href="https://joshua1988.github.io/web-development/http-part1/">github 블로그</a>)

## HTTP 프로토콜이란

HTTP(HyperText Transfer Protocol)는, 웹을 개발하는 사람들이라면 누구나 알아야 하는 통신 프로토콜이다. 프로토콜이란 상호간 정의한 규칙을 의미하며, 특정 기기 간 데이터를 주고받기 위해 정의되었다. 통신 프로토콜을 쉽게 풀어보면, "나는 이렇게 줄 테니 넌 이렇게 받고 난 너가 준걸 그렇게 받을게" 정도가 될 것이다.

웹에서는 브라우저와 서버 간에 데이터를 주고받기 위한 방식으로 HTTP 프로토콜을 사용하고 있으며, 따라서 프론트엔드 개발자라면 필수적으로 알아야 되는 지식이 되었다.

## HTTP 프로토콜의 특징

HTTP 프로토콜은 상태가 없는(stateless) 프로토콜이다. 여기서 '상태가 없다' 라는 말은, 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 독립적으로 관리가 된다는 뜻이다. 좀 더 쉽게 말하면, 이전 데이터 요청과 다음 데이터 요청이 서로 관련이 없다는 뜻이다.

이러한 특징 덕분에 서버는 세션과 같은 별도의 추가 정보를 관리하지 않아도 되고, 다수의 요청 처리 및 서버의 부하를 줄일 수 있는 성능 상의 이점이 생긴다.

HTTP 프로토콜은 일반적으로 TCP/IP 통신 위에서 동작하며 기본 포트는 80번이다.

## HTTP Request & HTTP Response

HTTP 프로토콜로 데이터를 주고 받기 위해서는 아래와 같이 요청(Request)을 보내고 응답(Response)을 받아야 한다.
<img src='request-response.png'>
그리고 요청과 응답을 이해하기 위해서는 먼저 클라이언트(Client)와 서버(Server)를 이해해야 한다.

클라이언트란 요청을 보내는 쪽을 의미하며 일반적으로 웹 관점에서는 브라우저를 의미한다. 서버란 요청을 받는 쪽을 의미하며 일반적으로 데이터를 보내주는 원격지의 컴퓨터를 의미한다.

## URL

URL(Uniform Resource Locators)은 개발자가 아니더라도 이미 우리에게 익숙한 용어이다. 서버에 자원을 요청하기 위해 입력하는 영문 주소이다. 숫자로 되어 있는 IP 주소보다 기억하기가 훨씬 쉽기 때문에 더 많이 사용된다.

URL 구조는 아래와 같다.
<img src='url-structure.png'>

## HTTP 요청 메소드

앞에서 살펴본 URL을 이용하면 서버에 특정 데이터를 요청할 수 있다. 여기서 요청하는 데이터에 특정 동작을 수행하고 싶다면 어떻게 해야 할까? 바로 HTTP 요청 메소드(Http Request Methods)를 이용해야 한다.

일반적으로 HTTP 요청 메소드는 HTTP verbs라고도 불리며, 아래와 같이 주요 메소드를 갖고 있다.

- GET: 존재하는 자원에 대한 <b>요청</b>
- POST: 새로운 자원을 <b>생성</b>
- PUT: 존재하는 자원에 대한 <b>변경</b>
- DELETE: 존재하는 자원에 대한 <b>삭제</b>

이와 같이 데이터에 대한 조회, 생성, 변경, 삭제 동작을 HTTP 요청 메소드로 정의할 수 있다. 때에 따라서는 POST 메소드로 PUT,DELETE의 동작도 수행할 수 있다.

기타 요청 메소드는 다음과 같다.

- HEAD: 서버 헤더 정보를 획득. GET과 비슷하나 Response Body를 반환하지 않음.
- OPTIONS: 서버 옵션들을 확인하기 위한 요청. CORS에서 사용

## HTTP 상태 코드

앞에서 살펴본 URL과 요청 메소드가 클라이언트에서 설정해야 할 정보라면, HTTP 상태 코드(HTTP Status Code)는 서버에서 설정해주는 응답(Response)정보이다.

프론트엔드 개발자 입장에서는 더욱이 중요한 이유가 이 상태 코드로 에러 처리를 할 수 있기 때문이다. 간단한 예시를 들어 아래와 같이 사용자 목록을 받아오는 GET 메소드 요청을 날린다고 해보자.

```
http//domain.com/users
```

위 요청을 보내고 나면, 서버에서 응답으로 오는 상태 코드가 크게 2개로 나뉜다. 200(성공)과 404(실패)이다. 따라서, 이 HTTP 상태 코드로 추가적인 로직을 구현할 수 있다.

주요 상태 코드는 200번대부터 500번대까지 다양하게 있지만 주요한 상태 코드만 몇 개 살펴볼 것이다.

### 2xx - 성공

200번대의 상태 코드는 대부분 성공을 의미한다.

- 200: GET 요청에 대한 성공
- 204: No Content, 성공했으나 응답 본문에 데이터가 없음
- 205: Reset Content, 성공했으나 클라이언트의 화면을 새로고침 하도록 권고
- 206: Partial Content, 성공했으나 일부 범위의 데이터만 반환

### 3xx - 리다이렉션

300번대의 상태 코드는 대부분 클라이언트가 이전 주소로 데이터를 요청하여 서버에서 새 URL로 Redirect를 유도하는 경우이다.

- 301: Moved Permanently, 요청한 자원이 새 URL에 존재
- 303: See Other, 요청한 자원이 임시 주소에 존재
- 304: Not Modified, 요청한 자원이 변경되지 않았으므로 클라이언트에서 캐싱된 자원을 사용하도록 권고. ETag와 같은 정보를 활용하여 변경 여부를 확인

### 4xx - 클라이언트 에러

400번대 상태 코드는 대부분 클라이언트의 코드가 잘못된 경우이다. 유효하지 않은 자원을 요청했거나, 요청이나 권한이 잘못된 경우 발생한다. 가장 익숙한 코드는 404이다. 요청한 자원이 서버에 없다는 의미이다.

- 400: Bad Request, 잘못된 요청
- 401: Unauthorized, 권한 없이 요청. Authorization 헤더가 잘못된 경우
- 403: Forbidden, 서버에서 해당 자원에 대해 접근 금지
- 404: Method Not Found, 허용되지 않은 요청 메소드
- 409: Conflict, 최신 자원이 아닌데 업데이트하는 경우. ex) 파일 업로드 시 버전 충돌

### 5xx - 서버 에러

500번대 상태 코드는 서버 쪽에서 오류가 난 경우이다.

- 501: Not Implemented, 요청한 동작에 대해 서버가 수행할 수 없는 경우
- 503: Service Unavailable, 서버가 과부하 또는 유지 보수로 내려간 경우

## 다시 살펴보는 HTTP 요청과 응답

앞에서 배운 URL, 요청 메소드, 상태 코드를 조합하면 아래와 같은 구조가 나온다.
<img src='http-full-structure.png'>
