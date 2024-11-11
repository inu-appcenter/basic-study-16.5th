# Appcenter Basic Course Study 2 : DataBase (1)

### 데이터베이스(Database, DB)란?
간단하게 말해서, 데이터를 보존하는 그릇이라고 볼 수 있다.
** e.g. 쇼핑 사이트에서의 구매 이력, 어디선가 날라오는 스팸메일들 -> 다 Database에 등록되어서 관리된다.
엑셀 실무에서 만드는 표나, 하나의 주소록같은 개념이라 생각하면 이해가 쉽다. 

요즘같은 데이터화 시대에서는 DB의 개념이 필수이다.
대량의 데이터가 오고가며 이를 한번에 관리하려면 골치가 아프다.
이를 가장 효율적으로 관리할 수 있는 것으로 고안된 것이 바로 Database이다.

Software Layer(운영체제 / 미들웨어 / 애플리케이션)에서 보통 DB는 미들웨어쪽에 속한다. 

### Database의 종류와 특징은 무엇이 있을까?
Database의 종류로는 우선 관계형 데이터베이스와 비관계형 데이터베이스가 있다. 관계형 데이터베이스는 SQL언어를 이용하고, 비관계형 데이터베이스는 NoSQL언어를 이용한다. 밑에서 SQL과 NoSQL의 차이 부분에서 자세히 다뤄보겠다. NoSQL에 대해 살짝만 설명해보자면, NoSQL은 관계형DB의 일부 기능을 버리기 때문에 퍼포먼스 측면에서 유리하다.

일단 Database의 펀더멘탈한 기능들을 보면, 첫 번째로 Data의 검색과 갱신이다. 검색은 당연히 가장 중요한 부분이고, 갱신이란 등록, 수정, 제거를 말한다. 

그 다음은 동시성 제어이다. Database를 만약 나 혼자가 아니라 다수의 개발자가 개발하는 상황이라면, 복수의 사용자가 동시에 접근(공유, 이용)하기 위해서는 Data 갱신에 대한 제어가 필수적이다.

세 번째는 장애 대응이다. 데이터를 다중화해서 Data를 분산된 환경에 나눠 보관하는 것이다.

마지막으로는 보안이다. 당연하겠지만 데이터베이스가 다른 사용자들에게 노출된다면 최악의 상황에 직면하게 된다. DataBase에 보존된 Data를 어떻게 은닉할 것인가가 중요하게 보여지겠다.

보안에 대해 잠깐 자세하게 얘기해보자면, 어떠한 웹 서비스나 애플리케이션을 프로그래밍 할 때는 반드시 SQL Injection이라는 공격에 대비해야한다. SQL Injection이란, 보통 웹사이트를 예시로 들어서 설명해보자면, 입력 필드는 무조건 있을 것이다. 단순하게 로그인 화면도 하나의 입력 필드라고 볼 수 있다. 이러한 입력필드에 SQL 쿼리문을 날려보는 것이다. 만약 보안이 제대로 갖춰지지 않은 입력필드가 존재한다면, SQL문이 그대로 서버에 전송되면서 서비스의 DB에 접근이 가능해지게 되는 것이다. 간단한 쿼리문으로 예시를 보자.

```sql
SELECT * FROM users WHERE username = 'minjunseong' --' AND password = '입력한_비밀번호';
```
주석처리된 뒷 부분이 무시되면서 패스워드 없이 minjunseong이라는 계정에 접속할 수 있다. ~~이 계정은 이제 제껍니다.~~

이 외에도 DROP TABLE user;와 같은 쿼리문을 전송해버리게 된다면 유저의 정보가 몽땅 날라가버리는 대참사가 일어날 수 있다. 이러한 공격 방식을 SQL Injection이라고 한다. 그래서 간단하게는 입력필드에 대한 특수문자 금지와 같은 대처 방법이 있고, 프로그램을 설계할 때 Prepared Statements나 매개변수화 쿼리를 이용하는 방법이 있다. 또 Prepared Statements나 매개변수화 쿼리를 간단히 설명해보자면 SQL 쿼리문을 그냥 미리 준비해두는거고, 입력 란을 변수로 할당받게 해서 안전하게 입력 값에 영향받지 않도록 하는 방식이다.

만약에 당연히 안 하는게 좋겠지만, 이런 실습을 해보고싶다면 대충 만들어진 초등학교 학교 사이트에 들어가서 검색창에다 SQL 쿼리문을 입력해보면 가끔 먹히는 경우가 있다. 실제로 조금 나쁜 친구의 이야기이긴 하지만, SQL Injection을 통해 초등학교 식단표를 모두 맛없는 메뉴로 몰래 바꾼 친구가 있었다. 당연히 복구는 시켜놨다고 한다. 실습은 워게임 사이트나 본인 로컬환경에서 시도해보는걸 권장한다...

## 그럼 이런 Database는 뭐로 관리하나요?
Database의 관리는 모두 **'DBMS(DataBase Management System)'** 으로 이루어진다. Database의 기능을 제공하는 소프트웨어들을 일컫는다.
Data를 수월하게 검색하고 갱신할 수 있는 수단이라고 볼 수 있다.
대표적인 DBMS로는 Oracle, MySQL, PostgreSQL 등이 있다.
DBMS는 데이터 중복을 줄이기 위해, 무결성을 위해, 동시성을 더 간편하게 하기 위해 탄생하게 되었다.

## DB하니까 SQL 언어를 배우더라던데.. 이게 뭔가요?
SQL(Structured Query Language)이란 관게형 DB가 조작하기 위해 만들어진 표준형 '언어'이다. 
하나의 장점이라면 **반복이나 조건(분기)등을 이용하지 않아도 쉽게 DATA에 접근** 할 수 있다는 것이다.
반례로 자료구조때 열심히 배운 Linked-List가 떠오를 텐데, 이를 구현해서 DATA에 접근하는것과 상당히 비교되는 것 같은 개인적인 생각이 있다.

SQL의 기본 조작으로는, 우선 TABLE이라는 표 형태를 사용하고, 열(column)과 행(row)의 구조를 잘 파악해야한다. 그리고 이를 조작하기 위해서는 SELECT, INSERT, UPDATE, DELETE가 있다. 영문 그대로 해석하면 SELECT는 데이터를 조회하는 것. 검색 기능에 쓰일 듯 하다. INSERT는 새로운 데이터를 삽입할 때, UPDATE는 이미 존재하는 데이터를 수정할 때 쓰인다. DELETE는 해당 데이터를 삭제할 때 쓰인다. 이러한 기본 조작을 통해 우리는 DB CRUD가 가능해진다.

참고로 **MySQL, PostgreSQL** 등 모두 SQL 문법을 지향한다. 나는 사실 두개가 문법적으로 다른건 줄 알았는데 미묘한 차이는 있으나 그런건 아니었다.

그럼 왜 나누는거지? 싶어서 검색을 해보니 **트랜잭션 처리, 지원하는 SQL 함수들이 달랐다.** MySQL같은 경우는 이따 설명할 트랜젝션 처리가 다소 제한적이지만 빠른 성능과 읽기에 최적화 되어있고, PostgreSQL은 고급 함수들을 지원하고 복잡한 연산이나 트렌젝션들이 효율적으로 관리되며, 쓰기 작업과 읽기 작업 둘 다 많을때 사용된다고 한다. 또한 보안도 높은 수준이다. 다만 복잡한 구성과 고성능의 리소스가 요구되고, 과도한 트렌젝션들을 처리하다보니 성능 저하 이슈도 있다. 이를 보니 MySQL, PostgreSQL 모두 Trade-Off 구조임을 알 수 있었다.

### DBMS가 SQL이고 SQL이 DBMS인거 아닌가요?
앞 설명에서 특징들을 언급했듯, **둘이 조금은 다르다고 볼 수 있다.** 다소 성격은 다른 비유긴 하지만 Javascript와 Java와 같은거 아닌가요? 와 같은 소리이다. 각 약어의 끝 단어를 보면 알 수 있듯이 Software와 Language의 차이라고 볼 수 있다.
즉, DBMS는 SQL언어나, 뒤에서 설명 될 다른 방식(문서 지향형인 json, Key-Value 형식 등)으로 데이터가 관리되고 운용되는 소프트웨어 자체를 말하며, SQL은 DBMS로부터 사용되는 언어이다. SQL은 DBMS의 하위 관계라고 볼 수 있다.

### 그럼 SQL만 알면 저도 이제 Database 전문가가 되는건가요?
아니다. DBMS에는 SQL만 있는 것이 아니다. NoSQL이라는 방식이 있다. Not Only SQL이라는 뜻을 가지고 있는데, 대표적으로 JSON형태의 문서 형태로 SQL 쿼리문을 아예 사용하지 않는 MongoDB가 좋은 예시일 것 같다. SQL의 SELECT문을 MongoDB는 find()와 같은 함수를 이용하게 된다. 이런 비관계형 데이터베이스가 바로 NoSQL이다. 그래서 SQL을 정통하게 쓴다고 해서 NoSQL까지 잘 쓴다는건 아니다. 공부를 해야한다. ~~공부할게 산더미구나..~~

근데 모든 데이터는 관계성을 띄고 있으니 SQL만 잘해도 되는거 아닌가요? 라는 생각이 들 수 있지만, 사실 SQL NoSQL 모두 적법한 분야가 다르다. 데이터의 정형성에 따라 달라지는데, 데이터 구조가 일정하고 (주소록 같은) 복잡한 관계와 트랜젝션이 필요한 상황이라면 SQL 언어를 사용하고, 이와 반대로 비정형 데이터, 문어발식 대규모 확장이 필요한 데이터들은 NoSQL을 채택한다.

다시 간단히 정리하자면, SQL은 우리가 흔히 엑셀처럼 쓰는 테이블 형식을 지향하고, NoSQL은 문서나 Key-Value형태의 형식을 지향하는 차이가 있겠다.

대표적인 예시로는 전형적으로 고정적이고 정형적인 금융시스템은 거의 SQL 언어를 활용하며, SNS같이 무한히 확장되는 데이터들의 더미는 NoSQL을 사용한다. 

### 그럼 이런 Database를 어떻게 제어하나요?

다양한 명령어들이 크게 세 개로 분류된 집합으로 이용되는데, 이 세 개의 집합을 DDL, DCL, DML이라고 부른다. 이를 이용한 명령어로 쿼리문을 만들어서 데이터를 갱신하고 검색할 수 있다. 또한, 데이터는 일관적이고 무결해야하는데, 이를 지키기 위해서는 트랜젝션이라는 개념이 쓰인다. 밑에서 천천히 알아보자.

#### DDL (Data Definition Language) - 데이터 정의 언어
DDL은 데이터베이스의 구조 자체를 정의하고 관리할 때 사용하는 명령어 집합이다. 새로운 테이블을 생성하거나 삭제하고, 테이블 구조를 변경하는 작업 등이 포함된다. 더 나아가선 스키마, 도메인 등을 정의하기도 한다. 대표적인 명령어로는 CREATE(테이블 생성), ALTER(테이블 구조 변경), DROP(기존 테이블 삭제), TRUNCATE(기존 테이블 이름 변경)가 있다.

#### DML (Data Manipulation Language) - 데이터 조작 언어
DML은 테이블의 데이터를 조회하고, 추가, 수정, 삭제하는 등 데이터 자체를 다루는 명령어이다. 사실 아까 4가지 조작 방법에 대해 언급했었는데, INSERT, DELETE, UPDATE, SELECT문이 해당하는 부분이다. DML 명령어는 실행 후 결과를 즉시 저장하지 않고, 필요시 저장하도록 설정할 수 있어, 실수로 실행해도 복구가 가능하다.

#### DCL (Data Control Language) - 데이터 제어 언어
DCL은 데이터베이스에 대한 권한을 설정하고 관리하는 명령어이다. 그래서 이에 대한 권한 제어가 필요한데, GRANT(권한 부여), REVOKE(권한 해제)라는 명령어를 이용해서 특정 사용자에게 데이터베이스에 대한 접근 권한을 부여하거나 해제할 때 사용된다. DCL은 데이터의 보안과 접근 제어를 관리하는 데 중요한 역할을 합니다.

#### 트랜잭션 (Transaction)
트랜잭션은 데이터베이스에서 여러 작업을 하나의 단위로 묶어 실행하는 것을 의미한다. 쉽게 말하면 하나의 쿼리 처리 단위라고 볼 수 있다. 트랜잭션이 완료되면 작업이 데이터베이스에 모두 반영되고, 실패하면 모든 작업이 원래 상태로 되돌아간다. 이는 데이터의 일관성 때문에 엄격한 규칙을 지켜야한다. 주로 이용되는 문법으로는 ROLLBACK, COMMIT, SAVEPOINT가 있다.
ROLLBACK은 작업 시작 이전의 상태로 되돌리는 것, COMMIT은 올바르게 완료한 작업을 데이터베이스에 반영. GIT에서 배웠던 내용과 유사하기도 하다. SAVEPOINT는 말 그대로 저장 지점이다. ROLLBACK 문법과 같이 쓰기도 한다.

##### * 트랜잭션의 4가지 특징 (ACID)
- Atomicity (원자성): 트랜잭션 내의 모든 작업이 모두 완료되거나 모두 실패해야 한다.
- Consistency (일관성): 트랜잭션이 완료되면 데이터베이스의 상태는 항상 일관성을 유지해야 한다.
- Isolation (격리성): 여러 트랜잭션이 동시에 실행되더라도, 서로 간섭하지 않도록 해야 한다.
- Durability (영속성): 트랜잭션이 성공적으로 완료되면, 그 변경 사항은 영구적으로 저장되어야 한다.


### 이제 Database 사용법은 알겠어, 좀 더 구체적인 구현을 하고싶은데?

그렇다면 ERD 표현 방법을 이용해볼 수 있다. 이는 Entity Relationship Diagram의 약어로, 테이블들의 관계를 시각화해서 구성하는 수단 중 하나이다. ERD 구성에서의 주된 요소로는 개체(Entity), 속성(Attribute), 관계(Relationship)가 있다.
개체란 데이터베이스에서 저장해야하는 요소를 의미하는데, 이따 설명할 내가 간단히 설계한 학교 학생 데이터베이스를 예시로 들어보면, 학생, 강의 등이 하나의 개체가 되는 것이다. 속성은 개체가 가지게 되는 세부 정보를 의미한다. 관계는 개체간의 연결도를 보여준다.

관계의 유형은 다음과 같다.

```
-|----|-     1:1 방식 : 두 개체 간의 관계가 하나만 연결되는 것
-|----|<     1:N 방식 : 한 개체가 여러 개체와 연결되는 것
>|----|<     N:M 방식 : 두 개체 간의 관계가 서로 연결 되거나 다수의 개체랑 연결되는 것
```
    

### MySQL 짧은 실습

```sql
mysql -u root -p                -- MySQL에 로그인
quit                            -- 귀여운 인사와 함께 로그아웃이된다.
show databases;                 -- 데이터베이스 목록이 표시된다.
CREATE DATABASE minjunseong;    -- 데이터베이스를 생성한다. 
USE minjunseong;                -- minjunseong이라는 데이터베이스를 이용한다.
show tables;                    -- USE된 DATABASE에 있는 Table들을 보여준다.

-- ERD 생성 실습 

-- 0. DB 생성
CREATE DATABASE INU;

-- 1. 학생 테이블 생성
CREATE TABLE Student (
    student_id INT PRIMARY KEY,      -- 학번
    name VARCHAR(50),                -- 학생 이름
    age INT,                         -- 나이
    grade VARCHAR(10)                -- 학년
);

-- 2. 강의 테이블 생성
CREATE TABLE Course (
    course_id INT PRIMARY KEY,       -- 강의 고유 ID
    course_name VARCHAR(100),        -- 강의명
    mark INT                         -- 이수학점
);

-- 3. 교수 테이블 생성
CREATE TABLE Professor (
    professor_id INT PRIMARY KEY,    -- 교수 고유 ID
    name VARCHAR(50),                -- 교수 이름
    department VARCHAR(50)           -- 학과
);

-- 4. 학생-강의 중간 테이블 생성 (N:M 관계)
CREATE TABLE Course_Student (
    student_id INT,                  -- 학생 ID (FK)
    course_id INT,                   -- 강의 ID (FK)
    PRIMARY KEY (student_id, course_id), -- 복합 기본 키
    FOREIGN KEY (student_id) REFERENCES Student(student_id) ON DELETE CASCADE,      
    FOREIGN KEY (course_id) REFERENCES Course(course_id) ON DELETE CASCADE         
    -- Reference를 쓰는 이유 -> 중간 테이블이 다른 테이블을 참조하기 위해 사용된다 (데이터 무결성을 위함. (중간에 변조되는 일이 없도록!!))
    -- CASCADE를 쓰는 이유 -> 데이터를 수정하거나 삭제할 때 Orphan DATA를 막기 위해 + 데이터 무결성을 위함. 예를 들어 상위 학생 데이터가 갑자기 하나 날라간다면, 사라진 학생에 대한 Course_student의 데이터도 당연히 날라가야한다.
);


-- 1. 학생 데이터 삽입
INSERT INTO Student (student_id, name, age, grade) VALUES
(2101, 'minjun', 24, '3학년'),
(2102, 'yunho', 23, '2학년'),
(2103, 'sunwoo', 27, '4학년'),
(1901, 'jinkyu', 27, '4학년'),
(2001, 'minjung', 26, '4학년');

-- 2. 강의 데이터 삽입
INSERT INTO Course (course_id, course_name, mark) VALUES
(1, 'System Security', 3),
(2, 'Server Management', 2),
(3, 'Data Structures', 3);

-- 3. 교수 데이터 삽입
INSERT INTO Professor (professor_id, name, department) VALUES
(1, 'Seungsoo Lee', 'Computer Science Eng.'),
(2, 'Minkyung Seong', 'IBM Korea');

-- 4. 학생-강의 관계 데이터 삽입
INSERT INTO Course_Student (student_id, course_id) VALUES
(2101, 1), -- 민준 -> 시보
(2102, 2), -- 윤호 -> 서버관리
(2103, 1), -- 선우형 -> 서버관리
(2103, 3); -- 선우형 -> 자료구조


-- 1. 모든 학생 조회
SELECT * FROM Student;

-- 2. 모든 강의 조회
SELECT * FROM Course;

-- 3. 모든 교수 조회
SELECT * FROM Professor;

-- 4. 학생과 그들이 수강하는 강의 목록 조회
SELECT 
    s.name AS student_name,
    c.course_name AS course_name
FROM 
    Course_Student cs
JOIN 
    Student s ON cs.student_id = s.student_id
JOIN 
    Course c ON cs.course_id = c.course_id;
```



### 향후 공부 내용
- 트랜젝션 처리에 대해 더 공부해 볼 것
- 동시성 제어를 위한 LOCK에 대한 개념 알아보기
- 좀 더 다양한 실습 해보기
- 데이터베이스의 규칙과 설계에 대한 규칙에 대해 더 공부해보기 (해서는 안 되는 트랜젝션 처리)
- 다수의 테이블을 이용한 ERD 구현해보기