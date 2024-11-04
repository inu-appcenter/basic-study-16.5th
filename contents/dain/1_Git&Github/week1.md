# <1주차> Git & GitHub


## Git이란


- 버전 관리 도구
    - version: 어떤 프로그램을 수정, 개선하여 완성한 것. 이전과 약간씩 다른 변화들을 구분하는 표시
- 언제 누가 무엇을 변경했는지 비교할 수 있다
- 코드 합치기, 이전 버전으로 돌아가기
- 분산형 버전 관리 시스템(DVCS): 각 개발자에게 공유 가능한 저장소 사본을 제공


## Git에서 사용하는 명령어


`git init`
- 현재 디렉토리(버전 관리할 디렉토리) 아래에 .git 디렉토리를 만들고 Git 저장소 초기화(생성)
- 추적X

`git add 파일명`
- 변경된 파일을 스테이징 영역에 추가(추적해줘)
- staging area: commit이 가능한 영역으로, commit하기 전 파일을 담아두는 상자와 같은 개념
  -"파일명" 자리에 . 입력 시 모든 파일 스테이징

`git commit`
- 스테이징 영역에 있는 파일들(git add된 것)의 상태를 저장소(repository)에 기록(버전 생성)
- 장바구니(스테이징 영역)에 담은 것을 주문(commit)한다고 생각하면 편함

` git commit -m 커밋 메시지`
- 메시지 작성

`git log --all -oneline`
- commit 이력 조회

`git status`
- 파일 변경, 스테이징 확인 가능

`git branch 브랜치명`
- 브랜치 생성(최근 commit의 사본 생성)

`git switch 브랜치명`
- 브랜치 이동

`git checkout`
- 브랜치 간 전환 또는 현재 작업 중인 파일들 복원

`git merge`
- 각 브랜치에 commit이 있는 경우 두 브랜치의 코드를 합쳐 새로운 커밋 생성

`git push origin 브랜치이름`
- 작성한 코드를 원격 저장소에 업로드

`git clone`
- 원격 저장소의 로컬 복사본이 컴퓨터에
- 복제된 저장소의 모든 브랜치를 생성하고 원격의 기본 활성 브랜치로 체크아웃(전환?)
-
`git config`
- Git의 환경 설정 관리
- 사용자 정보 설정이나 저장소별 설정을 구성



## GitHub란


- 코드 저장소
- 개발자들의 소셜 네트워크
- 깃으로 관리한 코드를 push 통해 GitHub에 올린다(저장한다)
- 드라이브와 같은 개념


## Pull request란

![image.png](image.png)

- '내가 작업한 코드가 있으니 내 브랜치를 당겨 검토 후 병합해주세요'
    - Push: 내가 작업한 것을 깃 서버에 올리는 것
    - Pull: 깃 서버에 업데이트되어 있는 내용을 받아오는 것

## fork란

- 다른 사람의 Github repository에서 내가 어떤 부분을 수정하거나 추가 기능을 넣고 싶을 때 해당 respository를 내 Github repository로 그대로 복제하는 기능(원본과 연결)
- original repository에 변경 사항을 적용하고 싶으면 해당 저장소에 pull request를 해야한다. (병합)

1. Repository에 권한이 없는 사용자가 저장소를 fork한다
2. fork한 자신의 저장소에 변경 사항을 적용한 후 Push한다
3. 이후 원래 저장소(original repository)에 내 저장소에 있는 브랜치를 Pull Request 한다
4. 관리자가 승인하면 해당 저장소에 Merge 된다.

## fork와 clone 비교

| 구분    | fork                                            | clone                               |
|-------|-------------------------------------------------|-------------------------------------|
| 목적    | 원격 저장소를 내 계정으로 복사                               | 원격 저장소를 내 컴퓨터(로컬)로 복사               |
| 복사 위치 | GitHub 상에서 내 계정에 저장소 생성                         | 내 로컬 컴퓨터에 복사                        |
| 용도    | 주로 오픈 소스 프로젝트에 기여하거나 다른 프로젝트를 수정할 때 사용          | 원격 저장소를 로컬에서 작업하기 위한 환경 세팅          |
| 연결 상태 | 원본 저장소와 독립적이며, 변경 사항을 원본에 반영하려면 Pull Request 필요 | 원격 저장소와 연결 유지, 로컬에서 작업 후 직접 Push 가능 |


## GitHub 저장소에 Pull Request를 보내기 위한 과정에서 이용하는 git 명령과 명령별 옵션(- 붙으면 옵션)

1.원본 저장소를 Fork한 후, 자신의 GitHub 계정에 있는 Fork 저장소를 로컬로 클론
- git clone <URL>
2. 새 브랜치 생성
- git checkout -b <브랜치명>
- -b는 branch의 약자. 새 브랜치 만들고 바로 이동
3. 파일 수정 및 추가
   -git add <파일명>
4. 커밋
- git commit -m "설명"
5. 원격 fork 저장소에 push
- git push origin <브랜치명>
- git push -u origin <브랜치명>
6. github fork 저장소의 해당 브랜치에서 New Pull Request 클릭하여 생성

## git 주소를 가져와서 commit하고 push할 때까지의 흐름에 대해

1. git clone <원격_저장소_URL> - 원격 저장소를 로컬로 클론
2. 파일 수정 또는 추가
3. git add <파일명> - 변경 사항 스테이징
4. git commit -m "커밋 메시지" - 스테이징된 변경 사항 커밋
5. git push origin <브랜치명> - 원격 저장소에 커밋된 변경 사항 푸시


## git add와 commit을 할 때 git 내부 동작은

`git add`: 현재 commit된 버전과 다르게 변경된 파일이 있음을 알리는 동작
- 실행시 'objects', 'index'파일 변화
- `objects`: 파일의 내용
- `index`: objects 파일 링크의 list(파일 이름 포함)

`git commit`: 그 전까지 add한 파일이 해당 commit에 기록됨
- commit의 전체 정보가 담긴 파일 objects 생성됨
- 위의 objects와 다른 파일
    - 좀 더 큰 단위의 objects가 작은 단위, 이전 단위의 objects를 가르키고 있다
    - objects 파일의 링크, commit 저자의 정보, commit에서 남긴 메시지, 이전 commit의 링크 등

마지막 commit을 가르키는 HEAD 등 변경됨

## Readme.md에 대해

- Github에 프로젝트를 올릴 때 프로젝트에 대한 설명, 사용 방법, LICENSE 등의 내용을 기술하는 파일
- 어떤 프로그램을 사용하거나 오픈소스를 참고하기 위해 GitHub repository에 들어가 가장 먼저 확인하는 파일

1. 나를 위해
- 나의 프로그램을 다시 읽고 해석할 때 수고를 덜어준다
2. 협업자를 위해
- 지침서 역할로 유용하게 쓰인다
3. 유저를 위해
- 오픈소스로 배포하는 경우 유저들이 프로그램을 쉽게 이해하도록 한다

- 주된 구성: 프로젝트 구성, 프로그램 설치방법, 프로그램 사용법, 저작권 및 사용권 정보 등...

## 확장자 .md에 대해

- .md라는 확장자는 Git에서만 사용한다
- md는 마크다운의 약자로 마크다운 문법을 사용한다는 의미
    - 마크업 언어: 데이터 가공 및 연산이 아니라, 그저 데이터를 화면에 표시하기 위해 사용하는 언어
    - 마크다운 언어: 마크업 언어에서 파생되었지만, 태그(< >)를 사용하지 않는다. 읽고 쓰기 쉬운 문서 양식을 지향