# Appcenter Basic Course Study _ ETC : BackEnd Programming, Code Analysis

### Spring Boot?
스프링부트는 자바를 기반으로 한 '프레임워크'이다. Spring이라는 프레임워크에서 좀 더 발전된 형태이고, 다양한 설정과 라이브러리가 있다.
~~자바공부를 열심히 하자!!!~~
Spring Boot는 DB연결이나 HTTP 서버 설정을 자동으로 처리해주고, Tomcat과 같은 내장 서버(웹프 수업의 추억..), 개발자 입장에선 딱히 초기 셋팅을 크게 건드릴게 없다고 한다.

### BackEnd의 간단한 개념 정리
웹 애플리케이션은 주로 서버-클라이언트가 상호작용하는 구조를 띄고 있다.
여기서 주로 서버를 담당하는 것이 바로 BackEnd라고 부른다. 반대로 클라이언트는 FrontEnd가 되는 부분.
가장 주요하게 다루는 개념들을 스터디 했던 개념들로 통해 간략하게 적어보자면,
- Server : 클라이언트가 요청한 데이터를 제공하는 공간. (에어컨 24시간 풀가동하고 소리 겁나 큰 7호관 4층 서버실을 생각해보면 된다. 혹은 당장 앱센터/전산원 옆에있는 서버실.. 거기에 모든 것이 담겨져있다!) 서버도 하나의 컴퓨터라고 할 수 있다. (실제로 우리가 쓰는 로컬 컴퓨터를 하나의 서버로 만들 수 있다. 하지만 포트포워딩, 도메인 할당 등 해야할것이 꽤 늘어난다)
- DataBase : 2주차 과정에서 배운 내용이다. 데이터들을 저장하는 공간으로 서버에 내장되어 있을 것이다. 백엔드는 이런 데이터베이스를 연결하여 클라이언트로부터 오는 요청들(데이터 저장[POST 등], 조회[GET])을 다룰 수 있다.
- API : 서버와 클라이언트가 상호작용(통신)하기 위한 하나의 규칙으로 정의된다. 백엔드는 이런 HTTP API를 클라이언트측에 설계하여 제공해준다고 생각하면 된다.
- HTTP Response & Request : 클라이언트가 서버로 보낸 요청(Request) <-> 서버가 클라이언트에게 요청에 맞는 응답(Response)

### Spring 백엔드 프로젝트의 구조
1. Controller
  Controller는 HTTP 요청을 처리하는 역할을 한다. 클라이언트의 요청을 받아서 서비스 단에 데이터들을 보내고, 필요한 비즈니스 로직을 수행하고, 그 결과를 클라이언트에 반환한다.
  예를 들어, /api/todos로 오는 GET 요청을 처리하고, 서비스에서 그에 맞는 Todo 목록을 반환하는 기능을 한다.

2. Service
  Service단은 비즈니스 로직을 처리하는데, 여기서 비즈니스 로직이 뭐냐 물어볼 수 있다.
  앱센터 서버분이 열심히 작성해진 코드를 통해 알아보면,

  ```java
    public TodoRes createTodo(TodoReq todoReq) {
        Todo todo = Todo.builder()
                .content(todoReq.getContent())
                .deadLine(todoReq.getDeadLine())
                .member(memberRepository.findById(todoReq.getMemberId()).get())
                .build();
        todoRepository.save(todo);

        return TodoRes.builder()
                .memberId(todo.getMember().getId())
                .content(todo.getContent())
                .deadLine(todo.getDeadLine())
                .build();
    }
  ```

  위의 코드 flow는 사용자가 todo를 생성하면 동작하게 된다.
  todo entity를 생성하여 클라이언트로부터 온 값들을 할당받은 뒤 .save를 통해 Todo Repository에 저장하고(즉, Todo DB에 저장함.) -> 이것이 제대로 저장되었는지 .builder()메소드를 컨트롤러에 값을 반환한다. 
  이렇게 클라이언트가 요청한 생성 작업, 수정 작업 등을 Service단에서 처리를 하는것이 비즈니스 로직 처리이다.
  **내가 이해한 것 : (request) -> 컨트롤러 -> 서비스(필요시 Repository 등에 접근하여 처리 후 반환) -> 컨트롤러 -> (response)**

3. Repository
  Repository는 단순히 DB에서 DB를 읽고 쓰는 작업을 한다. 보통 SQL문이 아닌 메소드를 활용해서 DB를 조작하는 JPA를 이용해서 수월하게 사용한다. (JPA는 객체지향처럼 사용이 가능해서 중복되는 사항을 매핑하고, 반복적인 CRUD SQL을 대체할 수 있다.)

4. Domain(Entity)
  Domain(또는 Entity)는 데이터베이스 테이블과 매핑되는 클래스를 말한다. 예를 들어, Member나 Todo와 같은 클래스는 각각 Member 테이블과 Todo 테이블에 대응된다.
  하나의 DB 테이블과 같다고 생각하면 용이할듯한.

5. DTO (Data Transfer Object)
  클라이언트와 서버 간에 데이터를 전송할 때 사용하는 객체. 데이터베이스의 엔티티와는 다르게, 필요한 데이터만 담아서 전송합니다.
  그럼 이걸 왜써요? 싶은데, 호출의 최소화와 데이터 공간의 격리를 위해서이다. 

6. 추가
  그럼 DTO, Entity가 뭔차이지? 싶은데, MVC 아키텍쳐의 구조를 들여다보면 표현 계층 / 비즈니스 계층 / 데이터 접근 계층이 있다. DTO는 여기서 데이터를 다른 컴포넌트나 계층으로 옮겨주기 위한 표현 계층에 속하는 기능이고, Entity(Domain)는 Business Layer에 속하는 핵심 로직 중 하나이다. 둘의 관심사가 다르고, 이를 객체지향의 표현으론 SoC(Seperation of Concerns) 라고 한다.

7. 이렇게 나누는 이유가 뭐지?
  서비스단, 컨트롤러단, DTO단 등을 나누게 되면, 나중에 대규모 프로젝트를 하게되더라도, 유지보수와 확장성 부분에서 특장점을 가지고 있다. 

### Spring Boot를 통한 Request-Response Flow
- 클라이언트(웹 브라우저, 모바일 앱 등)가 HTTP 요청을 보낸다.
- Controller는 요청을 받고, 필요한 데이터를 Service로 전달한다.
- Service는 비즈니스 로직을 처리하고, Repository를 호출하여 데이터베이스에서 데이터를 가져온다.
- 데이터를 받은 Service는 그 결과를 Controller로 반환한다.
- Controller는 최종적으로 결과를 클라이언트에 응답한다.

### 코드 분석

#### Main 코드 실행단
```java
// main/StudyApplication.java
package com.basic.study;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class StudyApplication {

	public static void main(String[] args) {
		SpringApplication.run(StudyApplication.class, args);
	}
}
```
- main함수가 있는 걸 보아 이 프로그램의 시작점이라고 볼 수 있다. 해당 프로그램을 실행할 시 .run 함수가 동작하여 이 코드를 실행한다.
- 참고로 Spring Boot의 Annotation이 있는 파일들만 실행한다고 한다.

#### Controller (REST API 생성, HTTP 요청에 따른 처리)
```java
package com.basic.study.controller;

import com.basic.study.dto.TodoReq;
import com.basic.study.dto.TodoUpdateReq;
import com.basic.study.service.TodoService;
import lombok.RequiredArgsConstructor;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequiredArgsConstructor
@RequestMapping("api/todos")
public class TodoController {
    final private TodoService todoService;

    @PostMapping("")
    public ResponseEntity<?> postTodo(@RequestBody TodoReq todoReq) {
        return ResponseEntity.ok(todoService.createTodo(todoReq));
    }

    @GetMapping("")
    public ResponseEntity<?> getTodoes(@RequestParam Long memberId) {
        return ResponseEntity.ok(todoService.readTodoes(memberId));
    }

    @PutMapping("/{todoId}")
    public ResponseEntity<?> putTodo(@PathVariable Long todoId, @RequestBody TodoUpdateReq todoUpdateReq) {
        return ResponseEntity.ok(todoService.updateTodo(todoId, todoUpdateReq));
    }

    @DeleteMapping("/{todoId}")
    public ResponseEntity<?> deleteTodo(@PathVariable Long todoId) {
        return todoService.deleteTodo(todoId)
                ? ResponseEntity.ok("todo 삭제 성공")
                : ResponseEntity.ok("todo 삭제 실패");
    }
}
```
- 해당 컨트롤러 부분은 어노테이션을 부분을 바탕으로 분석해보았습니다. (멤버 컨트롤러도 이와 동일한 Structure을 띄고있음에 생략하였습니다.)
- @RestController -> REST API를 제공하는 컨트롤러임.
- @RequestMapping -> 어디서 해당하는 요청을 처리할지 URI 주소를 매핑한다. (밑에 Post, Get, Put, Delete Mapping에 해당하는 내용들을 어느 기본 URI에서 할 것인가?)
- @Post,Get,Put,DeleteMapping -> HTTP 요청 방법에 따라 Method를 처리함.
- @DeleteMapping부분을 보면 조건문을 이용한 성공/실패여부가 아닌 삼항연산자를 사용한 부분을 인상깊게 생각했다.
- 해당 매핑된 부분에 따라 Service단으로 정보를 넘겨주고, 비즈니스 로직을 실행케 한다.

#### Service
```java
// TodoService.java

package com.basic.study.service;

import com.basic.study.domain.Todo;
import com.basic.study.dto.TodoReq;
import com.basic.study.dto.TodoRes;
import com.basic.study.dto.TodoUpdateReq;
import com.basic.study.repository.MemberRepository;
import com.basic.study.repository.TodoRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.List;

@Service
@RequiredArgsConstructor
public class TodoService {
    final private MemberRepository memberRepository;
    final private TodoRepository todoRepository;

    // CRUD
    public TodoRes createTodo(TodoReq todoReq) {
        Todo todo = Todo.builder()
                .content(todoReq.getContent())
                .deadLine(todoReq.getDeadLine())
                .member(memberRepository.findById(todoReq.getMemberId()).get())
                .build();
        todoRepository.save(todo);

        return TodoRes.builder()
                .memberId(todo.getMember().getId())
                .content(todo.getContent())
                .deadLine(todo.getDeadLine())
                .build();
    }

    public List<TodoRes> readTodoes(Long memberId) {
        List<Todo> todoList = todoRepository.findAllByMemberId(memberId);
        ArrayList<TodoRes> todoResList = new ArrayList<>();

        for (Todo todo : todoList) {
            TodoRes todoRes = TodoRes.builder()
                    .memberId(todo.getMember().getId())
                    .content(todo.getContent())
                    .deadLine(todo.getDeadLine())
                    .isCompleted(todo.getIsCompleted())
                    .build();
            todoResList.add(todoRes);
        }
        return todoResList;
    }

    public TodoRes updateTodo(Long todoId, TodoUpdateReq todoUpdateReq) {
        Todo todo = todoRepository.findById(todoId).get();
        todo.update(todoUpdateReq);
        todoRepository.save(todo);
        return TodoRes.builder()
                .memberId(todo.getMember().getId())
                .content(todo.getContent())
                .deadLine(todo.getDeadLine())
                .isCompleted(todo.getIsCompleted())
                .build();
    }

    public boolean deleteTodo(Long todoId) {
        if (todoRepository.existsById(todoId)) {
            todoRepository.deleteById(todoId);
            return true;
        }
        return false;
    }
}
```
- TodoService부분을 보면 Create, Update, Delete, Read가 모두 구현된 것을 볼 수 있다. 이와 같이 CRUD의 세부적인 로직을 구현하는 부분이 서비스단이다
- 멤버레포지토리, 투두레포지토리는 레포지토리와 상호작용하기 위해 선언되었으며, 해당 레포지토리를 통해 DB에 접근하고 조회하는것을 용이하게 한다.
- createTodo를 이용해서 TodoReq로 요청받은 객체 엔티티를 생성, 결과를 TodoRes로 반환한다. (DTO로부터 객체를 생성하고 반환)
- readTodoes를 이용해서 투두 리스트를 조회하고, todoRepository.findAllByMemberId(memberId)를 통해 특정 회원의 모든 Todo를 가져오며, 반복문을 통해 Todo를 TodoRes로 변환-반환 한다.
- updateTodo에서는 update 메서드를 호출하여 필요한 필드만 수정하는 PATCH 기능을 수행한다.
- deleteTodo는 우선 투두ID가 정상적으로 존재하는건지 식별하고, 존재하면 삭제하고, 아니면 false를 반환한다.
- 이렇게 DTO를 사용함으로써 엔티티 객체를 외부로 노출하지 않는 보안성이 있고, JPA를 통한 DB 접근, 각 메서드를 통해 서비스계층에서의 역할을 정상적으로 수행하였다.


#### Domain과 DTO
##### Domain
```java
// Todo.java
package com.basic.study.domain;

import com.basic.study.dto.TodoUpdateReq;
import jakarta.persistence.*;
import lombok.AccessLevel;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import java.time.LocalDate;

@Entity
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Todo {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String content;

    private LocalDate deadLine;

    private Boolean isCompleted;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "member_id")
    private Member member;

    @Builder
    private Todo(String content, LocalDate deadLine, Member member) {
        this.content = content;
        this.deadLine = deadLine;
        this.isCompleted = false;
        this.member = member;
    }

    public void update(TodoUpdateReq todoReq) {
        this.content = todoReq.getContent();
        this.deadLine = todoReq.getDeadLine();
        this.isCompleted = todoReq.getIsCompleted();
    }
}
```
```java
// Member.java
package com.basic.study.domain;

import jakarta.persistence.*;
import lombok.AccessLevel;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import java.util.List;

@Entity
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "member_id")
    private Long id;

    private String email;

    private String password;

    @OneToMany(mappedBy = "member", cascade = CascadeType.ALL)
    private List<Todo> todoes;

    @Builder
    private Member(String email, String password) {
        this.email = email;
        this.password = password;
    }
}
```
- 코드를 보면 알 수 있듯이, Member 엔티티와 Todo 엔티티는 **일대다 관계**이다.
- 하나의 Member는 여러 Todo를 가질 수 있지만, Todo는 멤버 하나만 가질 수 있다. 그러므로 일대다 관계라고 볼 수 있다.
- Todo엔티티를 보면 JoinColumn 어노테이션이 있는데, 이는 member_id를 Foreign Key(외래키)로 가지며 Member엔티티와 관계를 가짐을 알 수 있다.
- Member엔티티는 회원 정보를 가지며, email과 password를 필드로 가지며, @builder를 통해 멤버 객체를 생성한다.
- Todo엔티티에서는 Todo 정보를 나타내며, content(할 일 내용), deadLine(마감기한), isComplete(끝냈는지에 대한) 정보를 필드로 가진다.
- update메소드를 통해 할 일 정보를 수정하는 비즈니스 로직이 담겨져있다.

##### DTO
* TodoReq/Res와 MemberReq/Res가 동일한 구조이므로 TodoReq/Res에 대한 부분만 기술하였습니다.
```java
// TodoReq
package com.basic.study.dto;

import com.basic.study.domain.Member;
import lombok.AccessLevel;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Getter;

import java.time.LocalDate;
import java.time.LocalDateTime;

@Getter
@Builder
@AllArgsConstructor(access = AccessLevel.PRIVATE)
public class TodoReq {
    private Long memberId;

    private String content;

    private LocalDate deadLine;
}
```
``` java
// TodoRes
package com.basic.study.dto;

import lombok.AccessLevel;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Getter;

import java.time.LocalDate;
import java.time.LocalDateTime;

@Getter
@Builder
@AllArgsConstructor(access = AccessLevel.PRIVATE)
public class TodoRes {
    private Long memberId;
    private String content;
    private LocalDate deadLine;
    @Builder.Default
    private Boolean isCompleted = false;
}
```
- DTO는 따로 로직이 필요 없고, Getter와 Setter만 존재하는 데이터 운반체이다.
- TodoReq는 클라이언트에서 전달되는 요청 데이터를 담는 객체 / TodoRes는 서버에서 클라이언트로 보내는 응답 데이터를 담는 객체이다.
- 참고로 이메일 양식의 유효성 검사, 패스워드값 특수문자 혼용 등의 필드 제한 조건은 Controller단에서 처리할 수 있다. (리팩토링시에 참고할 부분)
- TodoReq는 할 일을 생성할때 memberID, Content, DeadLine등의 필수 정보들을 포함하고, TodoRes는 Todo엔티티의 데이터를 담아 클라이언트에게 전달한다.
- HTTP 요청으로 받은 body의 데이터값을 DTO로 매핑하여 각 계층으로 전달하는 매개체가 되는 RESTful한 APi 셋팅이 되는거다.

#### DTO와 HTML Body 영역의 관계
- 클라이언트 → 서버(Request):
  클라이언트는 HTML Body 영역에 데이터를 JSON 형식으로 담아 요청한다.
  서버는 DTO(TodoReq)를 통해 이 데이터를 처리.

- 요청 JSON
```http
POST /api/todos HTTP/1.1
Content-Type: application/json

{
  "memberId": 1,
  "content": "Buy milk",
  "deadLine": "2024-11-20"
}
```

- 서버 → 클라이언트(Response):
  서버는 처리 결과를 DTO(TodoRes)로 만들어 클라이언트에 JSON 형식으로 응답한다.
  응답 데이터는 HTML Body 영역에 포함.

- 응답 JSON
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "memberId": 1,
  "content": "Buy milk",
  "deadLine": "2024-11-20",
  "isCompleted": false
}
```

### 추가적인 공부 : HTTP요청은 동시에 일어나는가?
- 프론트엔드부분 예습을 하다가 로그인을 하면 메인화면으로 넘어가는 것을 알 수 있는데, 그럼 이 상황에선 POST와 GET이 동시에 일어나는건가? 라는 의문이 들었다.
- 보통 POST와 GET이 순차적으로 일어난다.
```
1. POST (회원가입)
회원가입 화면에서 아이디와 비밀번호를 입력한 후 "회원가입" 버튼을 클릭하면 POST 요청이 서버로 전송.
이 요청은 사용자가 입력한 데이터(아이디, 비밀번호 등)를 서버로 보내어 새로운 회원을 등록하는 작업을 처리.
서버는 해당 데이터를 받아서 회원가입을 처리한 후, 성공적으로 회원가입이 완료되면 응답을 반환.

2. GET (메인화면)
회원가입이 성공하면, 사용자를 메인화면으로 리디렉션이 가능하다. 이를 위해 서버에서 응답을 보낼 때 HTTP 상태 코드 302 (Found) 또는 301 (Moved Permanently)을 사용하여 클라이언트(브라우저)에게 다음 URL로 이동하라는 지시를 내린다.
이때 브라우저는 서버의 응답에 따라 GET 요청을 해당 메인화면 URL로 자동으로 보내게 됩니다. 즉, POST 요청은 회원가입 처리만 하고, 그 이후에 GET 요청으로 메인화면을 띄웁니다.

==흐름 예시==
회원가입 화면에서:
사용자가 아이디와 비밀번호를 입력 후 회원가입 버튼을 클릭.
POST 요청: 아이디와 비밀번호를 서버로 전송.

서버에서:
회원가입을 처리하고, 성공 시 HTTP 302 응답을 전송
응답에 "Location: /main"과 같은 리디렉션 URL을 설정하여 메인화면으로 이동하도록 한다.

브라우저(Client):
서버의 응답을 받고, GET 요청을 자동으로 보내어 메인화면을 로드한다.

==결론==
회원가입을 처리하는 POST 요청이 먼저 일어나고, 그 후에 GET 요청이 일어나면서 메인화면으로 이동하게됨.
POST와 GET은 순차적으로 발생하며, 동시에 일어나지는 않는다.
```
애초에 HTTP는 클라이언트와 서버 간의 통신 프로토콜이므로, 각 요청은 **독립적이고 순차적**으로 처리된다.

#### 추가적인 개념 : 동시성(Concurrency)과 병렬성(Parallelism)
비록 HTTP 요청 자체는 기본적으로 순차적으로 처리되지만, 동시성(Concurrency)이나 병렬성(Parallelism) 개념을 사용하면 여러 요청을 동시에 처리하는 것처럼 보이게 할 수 있다.

**동시성 (Concurrency):**
동시성은 하나의 프로세서나 스레드가 여러 작업을 처리하는 방식이다. 여러 요청을 처리하는 것처럼 보이지만, 사실은 CPU가 각 작업을 조금씩 번갈아 가며 처리하는 방식입니다. 예를 들어, 네트워크 요청을 기다리는 동안 다른 요청을 처리하는 방식이다.

웹 애플리케이션에서 HTTP 요청을 비동기적으로 처리하거나, 여러 스레드를 사용하여 요청을 동시에 다룰 수 있다. 하지만 이 역시 각 요청은 여전히 순차적으로 처리되며, 비동기적으로 작업을 처리할 뿐이다.

**병렬성 (Parallelism):**
병렬성은 여러 CPU나 프로세서에서 완전히 독립적으로 작업을 동시에 처리하는 방식이다. 예를 들어, 서버가 여러 개의 요청을 동시에 처리할 수 있는 여러 서버나 스레드를 사용하는 경우이다.

웹 서버는 여러 요청을 병렬로 처리할 수 있지만, 각 HTTP 요청은 여전히 하나씩 처리된다. 여러 요청을 동시에 보내도, 각각의 요청은 독립적으로 처리되고, 서버는 이를 병렬로 처리할 수 있는 환경을 제공함.