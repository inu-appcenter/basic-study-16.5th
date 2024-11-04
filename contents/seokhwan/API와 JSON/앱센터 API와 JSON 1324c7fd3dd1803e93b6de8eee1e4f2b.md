# 앱센터 API와 JSON

추가 일시: 2024년 11월 2일 오후 6:32
강의: 앱센터_Basic_study

# API와 JSON

## HTTP 란?

---

- **H**yper**T**ext **T**ransfer **P**rotocol의 약자이다.
- 웹에서 데이터를 주고받는 서버-클라이언트 모델의 프로토콜

### HTTP

사용자가 웹사이트를 방문하면 브라우저가 웹서버로 리소스를 요청.

요청을 받은 웹서버는 HTML, CSS와 같은 리소스를 응답으로 돌려준다.

클라이언트의 요청과 서버의 응답 사이에는 여러 프록시 서버가 있다.

프록시 서버는 캐시를 보관하거나 보안을 위해 서버릐 IP 주소를 숨기는 등 다양한 역할을 한다.

이 모든 통신을 안전하게 하기 위해 TCP(Transmissin Control Protocol) 연결을 사용한다.

### HTTP와 HTTPS의 차이점

HTTP 통신에서 브라우저와 서버는 데이터를 일반 텍스트로 교환한다.

HTTP는 데이터를 암호화하지 않고 전송하기 때문에 제3자가 데이터를 가로채고 읽을 수 있다.

보안을 강화하기 위해 HTTP는 HTTPS(Hypertext Transfer Protocol Secure)로 확장되었다.

HTTPS는 이름과 같이 HTTP의 안전한 버전이다.

HTTPS에서는 브라우저와 서버가 데이터를 전송하기 전에 안 전하고 암호화된 연결을 생성한다.

HTTPS는 모든 요청 및 응답을 SSL(Secure Socket Layer) 및 **TLS(Transport Layer Security)** 프로토콜에 따라 암호화 한다.

그래서 HTTPS를 사용하면 카드 정보나 비밀번호와 같은 민감한 정보를 보호할 수 있다.

## HTTPS 주요 요소와 작동 원리

---

### URI와 BaseURL, URL의 개념

![image.png](image.png)

URI : Uniform Resource Identifier의 약자로 통합 자원 식별자를 말한다.

- inu.ac.kr은 URI로 리소스의 이름만 나타냄

URL : BaseURL : Uniform Resource Locator의 약자로 리소스의 위치를 나타내기 위한 규약.

- [http://inu.ac.kr](http://inu.ac.kr)  리소스 + 위치

BaseURL

- 사이트의 기본경로
- 사이트 안의 모든 상대 URL이 사용할 기준

### 엔트포인트(EndPoint)란?

커뮤니케이션 채널의 한 쪽 끝

URL 경로

데이터전송의 최종지점(?) 으로 이해함

### HTTP 요청과 응답 방식

![image.png](image%201.png)

- HTTP Header
    - 클라이언트와 서버가 요청 또는 응답으로 부가적인 정보를 전송할 수 있도록 합니다.
    - 헤더는 크게 요청(Request) 헤더와 응답(Response) 헤더로 나뉘어집니다.

- HTTP Body
    - 요청에 대한 실제 메시지/내용을 전송합니다.

F12 누르면 볼 수 있음

- HTTP Status Code ( 200, 201, 400, 404, 500 … )
    - 1XX : 요청을 받았으며 포로세스를 계속함
    - 2XX : 요청을 성공적으로 받았으며 인식했고 수용했음
    - 3XX : 클라이언트의 요청에 대해 적절한 위치를 제공하거나 대안의 응답을 제공
    - 4XX : 클라이언트의 잘못된 요청
    - 5XX : 정상적인 클라이언트의 요청에 대해 서버의 문제로 인해 응답할 수 없음

| 200 | OK | 요청을 정상적으로 처리함 |
| --- | --- | --- |
| 201 | Created | 성공적으로 생성에 대한 요청을 받았으며 서버가 새 리소스를 작성함 |
| 400 | Bad Request | 잘못된 문법으로 요청을 보내고 있어 서버가 이해할 수 없음 |
| 404 |  Not Found | 요청한 URI를 찾을 수 없음 |
| 500 | Internal Server Error | 서버의 문제로 응답할 수 없음 |

- HTTP Method ( GET, PUT, POST, PATCH, DELETE) 의 역할과 사용 방식
    - `GET`: 리소스 조회
    - `PUT`: 리소스 대체, 수정, 생성
    - `POST`: 데이터 추가, 등록
    - `PATCH`: 리소스 부분 변경(수정)
    - `DELETE`: 리소스 삭제

## API란?

---

- API(Application Programming Interface) 두 애플리케이션이 통신하는 방법

- 클라이언트가 요청을 보내면, 서버에서 요청에 상응하는 응답을 보내주는 시스템

![image.png](image%202.png)

## REST API란?

---

REST(Representational State Transfer) API는 표준 HTTP 프로토콜을 사용하는 API 아키텍처이다.

일반적으로 JSON 데이터 형식을 사용해서 브라우저와 호환성이 좋다.

HTTPS 및 SSL 프로토콜과 함께 사용하면 데이터를 안전하게 보호할 수 있다.

REST API의 특징

- 편리함 : HTTP 프로토콜을 따라서 표준화된 인터페이스를 제공
- 무상태(Statelessness) : REST API는 모든 요청을 독립적으로 처리해서 API의 확장성이 좋다
- 빠른 속도 : REST API는 요청을 캐시할 수 있어서 클라이언트가 응답을 더 빠르게 받을 수 있다.

REST API의 요청

- `request`: API 메서드이다.  `GET`, `POST`, `PUT`, `DELETE` 메서드가 있다.
- `url`: API 엔드포인트이다.  요청을 어디로 보내는지 정의한다.
- `header`: 서버에게 정보를 전달. 인증, 데이터 타입에 대한 내용이 들어간다.
- `data`: 서버에게 보내는 정보. 바디(Body), 메시지라고 불리기도 한다. `GET` 메서드에는 데이터를 보내지 않는다.

## HTTP와 REST API의 관계성

---

### REST API설계에서 HTTP 메서드 활용 예시

- **GET** : 특정 리소스 조회.
    - `GET /users`는 사용자 목록을 조회, `GET /users/{id}`는 특정 사용자의 정보를 조회.

- **POST** : 서버에 새로운 리소스를 생성하는 데 사용.
    - `POST /users`는 새로운 사용자를 생성.

- **PUT** : 기존 리소스를 수정하거나 전체 업데이트를 수행하는 데 사용.
    - `PUT /users/{id}`는 특정 사용자의 정보를 업데이트.

- **PATCH** : 부분 업데이트에 사용.
    - `PATCH /users/{id}`는 특정 사용자의 일부 속성을 업데이트.

- **DELETE**: 특정 리소스를 삭제하는 데 사용.
    - `DELETE /users/{id}`는 특정 사용자를 삭제.

### RESTful 하게 API 설계하는 방법

1. 엔드포인트에서는 동사 대신 명사를 사용 → HTTP 메소드들이 이미 GET, PUT, PATCH, DELETE 동작을 (Create, Read, Update, Delete) 동사의 형태로 나타내기 때문
2. 복수명사 사용 [https://inu.ac.kr/post/123](https://inu.ac.kr/post/123) 와 같은 엔드포인트가 있다면 put, patch 등의 요청을 통해 갱신이 가능하다. 그러나 사용자는 다른 게시물들이 있는지 알아채기 힘들 수 있기 때문에 복수 명사를 사용하는 것을 권장한다.

~~이 외의 RESTFUL한 설계 방법이 있지만 이해가 안 되는 부분이 많다.~~

~~직접 해봐야 느낄 수 있는 부분인듯??~~

### HTTP 메서드와 RESTful 설계의 관계

- RestFul 설계는 HTTP 메서드의 표준화된 사용으로 클라이언트 요청의 의도를 명확하게 이해할 수 있도록 함.
- HTTP 메서드의 명확한 활용이 RestFul 설계의 기본
- RESTful API에서는 URL 구조와 HTTP 메서드 사용이 클라이언트에게 리소스의 접근 방식을 자연스럽게 전달하도록 설계되며, 이로 인해 클라이언트와 서버 간의 효율적이고 직관적인 상호작용이 가능하다.

## XML과 JSON 이란?

---

### XML 기본 구조와 테그방식

- 구조
    1. XML 선언부
    2. DTD, XML 스키마 선언, 네임스페이스 선언
    3. XML 태그와 데이터

```jsx
<guests>

  <guest>

    <firstName>John</firstName> <lastName>Doe</lastName>

  </guest>

  <guest>

    <firstName>María</firstName> <lastName>García</lastName>

  </guest>

  <guest>

    <firstName>Nikki</firstName> <lastName>Wolf</lastName>

  </guest>

</guests>
```

~~HTML과 비슷한 듯?~~

### XML의 특징과 장점

- 다향한 데이터 범주에 대한 네임스페이스가 있는 트리 구조로 데이터를 저장한다.
- XML 태그 구조는 쓰고 읽기가 더 복잡하고 파일 용량이 크다.

### JSON의 기본 구조 및 표현 방식

- JOSN은 키-값 페어를 사용한다.

```jsx
{"guests":[

  { "firstName":"John", "lastName":"Doe" },

  { "firstName":"María", "lastName":"García" },

  { "firstName":"Nikki", "lastName":"Wolf" }

]}
```

### JSON의 특징과 장점

- JSON은 간결하고 읽고 쓰기 쉽다.
- 숫자, 객체, 문자열 및 부울 배열을 지원
- 파일 크기가 작고 데이터 전송 속도가 더 빠름

### REST API 에서는 어떤걸 기준으로 사용할까요?

주로 JSON을 사용할 것 같다.

JSON은 XML에 비대 데이터 구조가 간결하고 테이터의 전송속도가 빠르기 때문이다.

또한 가독서이 높고 자바 스크립트와의 호환성이 좋다.