### HTTP란? (Hyper Text Transfer Protocol)

HPPT 프로토콜의 의미
- 인터넷에서 데이터를 주고받을 수 있는 프로토콜이다.
HTTP와 HTTPS의 차이

|-------------------------------|
|    HTTP      |      HTTPS     |
|-------------------------------|
| 암호화 X      | 암호화 O       | 
|-------------------------------|
|보안 레벨 낮음 | 보안 레벨 높음 |
|-------------------------------|
=> HTTP는 중간에서 데이터를 가로탤 수 있지만 HTTPS는 암호화로 가로채기 어려움  

### HTTP 주요 요소와 작동원리

- URI와 BaseURL, URL 의 개념

- URI (Uniform Resurce Identifier) : 네트워크 상에서 자원을 가르키는 고유 식별자(ID).
- BaseURL : 웹 애플리케이션에서 공통적으로 사용되는 URL의 기본 경로
- URL (uniform Resource Identifiers) : Web에서 접근하고자 하는 자원의 위치를 나타내기 위해서 사용한다. 
ex) 동영상, 문서, 이미지, 이메일 ..

- 엔드포인트(EndPoint)란?

- 엔드포인트 : 컴퓨터 네트워크에 연결되는 모든 장치
ex) 데스크탑 컴퓨터, 스마트폰, 노트북, IOT(사물인터넷)..
- HTTP 요청과 응답 방식
    - 헤더와 바디
    1) 헤더는 클라이언트와 서버의 요청 또는 응답으로 부가적인 정보를 전송하도록 도움.
    Host : 서버의 도메인 네임
    -> 반드시 하나가 존재해야함.
    User-Agent : 가장 흔하게 사용하는 헤더
    -> 현재 사용자가 어떤 클라이언트를 통해 요청 보냈는지 알 수 있음.
    Cookie : 웹서버가 클라이언트에 쿠키를 저장했다면 쿠키의 저오를 이름-값을 웹서버에 전송함

    2) 바디는 메시지 본문(Payload)을 통해 표현(요청이나 응답에서 전달하는 데이터) 데이터 전달 
    - HTTP Status Code ( 200, 201, 400, 404, 500 … )
    HTTP Status Code(상태 코드) : 클라이언트가 보낸 HTTP 요청에 대한 응답을 알려주는 숫자코드

    ![alt text](image.png)

    1xx(Information) : 요청이 수신되어 처리중이며, 계속해서 프로세스 진행
    2xx(Successful) : 요청을 성공적으로 수신했으며, 정상 처리
    3xx(Redirection) : 요청을 완료하려면 추가적인 행동(리소스)이 필요
    4xx(Client Error) : 클라이언트 오류, 잘못된 문법/요청 등으로 서버가요청을 수행할 수 없음
    5xx(Server Error) : 서버가 정상 요청을 처리 X

    - HTTP Method ( GET, PUT, POST, PATCH, DELETE) 의 역할과 사용 방식
    
    1) GET : 리소스 조회, 데이터 요청
    => URL, 브라우저로 요청

    2) PUT : 리소스 대체 
    =>  리소스를 새로 만들거나 기존 리소스를 교체하기 위해 URL과 요청 본문을 사용

    3) POST : 요청 데이터 처리
    =>  데이터를 본문에 포함하여 전송

    4) PATCH : 리소스 부분 변경
    => JSON, XML 등의 데이터를 본문에 포함하여 서버에 전송

    5) DELETE : 서버에서 특정 리소스를 삭제
    => 주로 ID나 특정 식별자를 사용하여 삭제할 리소스를 명시

### API(Application Programming Interface)란?
- 다른 프로그램이나 서비스가 서로 소통하고 데이터를 주고받을 수 있도록 돕는 도구

### REST API란?

- REST : 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것
- REST 구성요소 / 특징

1) 구성요소 : 자원, 표현, 상태, URI, HTTP Wethod(verb)
2) 특징 : 무상태성, 계층 구조,  자원 기반 ..

- REST의 장단점

장점 
1) 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화
2) 서버와 클라이언트의 역할을 명확하게 분리

단점 
1) 표준이 자체가 존재하지 않아 정의가 필요하다
2) HTTP Method 형태가 제한적이다



### HTTP와 REST API의 관계성

- REST API설계에서 HTTP 메서드 활용 예시
회원 목록 /member-> Get
회원 등록 폼 /member/new -> Get
회원 등록 /member/new,/members -> Post
회원 조회 /members/{id} -> Get
회원 수정 폼 /member/{id}/edit -> Get
회원 수정 /members/{id}/edit,/members/{id} -> Post
회원 삭제 /members/{id}/delete -> Post

- RESTful 하게 API 설계하는 방법
1) 자원 중심의 URL 설계
2) HTTP 메소드 활용
3) 상태 코드 반환
4) 일관된 데이터 형식 : JSON 형식으로 데이터 반환, 클라이언트가 이해하기 쉽게 통일된 응답 구조 유지
5) 무상태성 유지 : 각 요청은 독립적으로 처리
6) URI 설계

- 둘의 관계성이 어떻게 되는지 말해주세요!
RESTful API는 REST의 원칙을 따르는 구체적인 구현체이다.

### XML과 JSON 이란 ?

- XML의 기본 구조 및 태그 사용방식
XML이란 공유 가능한 방식으로 데이터를 정의하고 저장하도록 도움

-기본 구조-
· XML 선언부DTD
· XML 스키마 선언 네임스페이스 선언
· XML 태그와 데이터

-태그 사용 방식-
1) 시작 태그와 종료 태그로 구성.
ex) <title>XML 기본 태그</title>
2) 중첩 구조
3) 속성 사용
4) 빈 태그 : 내용이 없는 태그는 닫는 태그 대신 self-closing 형식으로 사용

- XML의 특징과 장점
XML은 <태그> 형식을 사용
작성하기 번거로움

- JSON의 기본 구조 및 표현 방식
1) JSON 데이터는 이름과 값의 쌍, key : value 형식으로 구성, 중괄호({})로 둘러쌓아 표현
![alt text](image-1.png)

2) JSON 데이터는 쉼표(,)로 나열
- JSON의 특징과 장점
훨씬 눈에 잘 들어오고 코드량도 XML에 비해 적은 것을 볼 수 있음
간결하고 작성하기 쉽게 때문에 많은 분야에서 쓰이는 XML을 대체
![alt text](image-2.png)

- REST API 에서는 어떤걸 기준으로 사용할까요?

· 자원 중심
· HTTP 메서드
· URL 설계
· HTTP 상태 코드
· 자원 표현
· 무상태성