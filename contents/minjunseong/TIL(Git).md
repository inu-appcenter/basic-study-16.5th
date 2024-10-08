# Appcenter Basic Course Study 1 : Git (1)

### Git이란 무엇일까?
간단히 말하자면, <span style="background-color:#fff5b1">폴더 내부에 숨겨진 저장소를 만들어서, 파일의 Version(*이력)을 관리하도록 도와주는 Version Control System(VCS)</span>이다. 

그렇다면 버전관리는? 우리가 코드를 작성하다가 오류 지점이 발생하거나, 다시 원상복구해야 할 상황이 생길 수 있다. 이에 대한 Recursive Point(RP)으로 돌아가기 위한 수단 중 하나라고 볼 수 있다.

### 버젼관리 소프트웨어의 유형
#### 집중형
말 그대로 모든 소스코드가 한 가운데(중앙 서버)에 집중되어있음. 하나의 중앙 서버에 코드 이력이 남는 것이다. 딱 봐도 장단점이 보인다.
- Advantage : 운영이 간단하고 쉬움. 사용이 용이함
- Disadv. : 근데 이 모든 소스코드를 담은 중앙 서버가 해킹당하면 답이없어짐. 협업 규모가 커지면 수정 충돌도 일어남
- 그럼 이걸 누가 제공하죠? : Apache Subversion이 있긴 하다.

→ 서비스를 제공하는 대규모 프로젝트를 수행하게 되면.. 잘 안쓰게됨

#### 분산형
여러 저장소(Repository)에 각 버젼별로 소스를 보관하게 됨. 서버는 각 저장소 자료를 동기화하고 중개하는 역할을 한다.

이것의 대표적인 Case가 바로 **Git**이 되는 것


### 이걸 왜 쓰는거지?
~~그럼 이걸 안 쓸 이유가 있을까?~~
당장 대학교에서 과제 할 때에도 
- 보고서(최종1).hwp 
- 보고서(최종최종).hwp 
- 보고서(이게진짜임).hwp

와 같이 이미 우리는 굳이 개발자가 아니어도 학부과정에서부터 버전관리를 하고 있음을 알 수 있다.

하지만 효율적인 개발자가 되기 위해서는 source(수정2).c와 같은 파일을 만드는 것 보단, <span style="background-color:#fff5b1">한 파일의 여러 버전들을 보관하여 관리하는 것이 더 수월</span>할 것이다. (부끄럽지만 나도 학부 1학년 과정 때는 그렇게 했던 것 같다.)

또, 팀 단위 프로젝트를 수행하게 된다면, 서로가 여러 파일을 공유해서 각 로컬 저장소에 관리하는 것 보단, 깃을 이용하여 원격 저장소에 접근해서 <span style="background-color:#fff5b1">편리하게 유지보수와 동기화</span>가 가능해진다.

뿐만 아니라, 개인적인 측면에서도, 요즘은 한 기기로 개발하는 환경보단 노트북, 로컬PC, 심지어는 태블릿(원격 SSH 등..)으로도 코딩을 하기도 한다. 

이를 Git을 이용하면 <span style="background-color:#fff5b1">좀 더 간편하게 개발할 수 있는 환경</span>을 갖출 수 있다.

### Git의 특징들
- 대표적 DVCS (Divided Version Control System, 분산형 버젼 관리 시스템)
- 꼭 인터넷에 연결되어있지 않아도 일단 로컬 환경에서 개발을 수행하다가, 나중에 네트워크에 접속되었을 때 동기화해도 OK
- 이력을 남기기에 용이함 -> ~~프로젝트 할때 범인잡기하기 좋음~~ 어느 부분에서 수정이 일어나고 오류가 발생했는지 등을 검토하기에 좋다.
- **Push, Pull, Fetch** 기능을 통해서 개발 구성원들끼리 소스를 공유하기 편하다
- 분기 설정이 용이 (**Branch**를 나눠서 독립적으로 개발을 수행하다가 나중에 **Merge**하기도 한다.)
- 오픈소스 프로젝트를 진행한다면, 다른 외부 개발자들이 **Fork, Pull Request**를 수행하여 contribute할 수도 있음

### GitHub는 그럼 뭐죠?
유연한 실습을 위해서는 GitHub가 대체 뭐하는 곳인지 부터 알아야 할 것 같다.

Git에 대한 개념을 숙지하는 이유가 팀원 프로젝트를 수행하게 될 때 GitHub를 이용하기 때문이다.

보통 개발자들끼리 있는 자리를 가게 되면

> " 실례가 안된다면 github좀 알려주실 수 있나요? "

> " 제가 요즘 잔디 심기를 안해서.. "

> " 오 회원님 github에 있는 사이드 프로젝트가 정말 even한걸요? "

등과 같이 오고가는 대화를 들을 수 있다.

GitHub의 정의는 **Git Hosting의 대표적인 Service**라고 할 수 있다. 이와 유사한 것으로 BitBucket, GitLab등(~~홍대병~~까진 아니지만 유료 서비스이기도 하다. GitHub는 Pro버젼을 쓰지 않는다면 무료!)이 존재한다. 팀 단위 프로젝트나 개인 사이드 프로젝트를 수행할 시에 필요한 존재라고 볼 수 있다.

GitHub의 대표적인 특징으로는 Repository를 마음껏 만들 수 있고 (원격 코드 저장소), Private이나 Public으로 소스코드를 공개할 수 있으며, Issue Tracking과 같은 기능을 지원하여 이상적인 Project Management가 가능하다.

정의 보단 예시로 이해하는게 편할 것 같아 Issue 발생 건에 대한 간단한 프로젝트 활동을 대략적으로 써보자면,

1. 한 프로젝트가 완성이 되었다.
2. 하지만 그 프로젝트에서 결함이 발견되었다. 혹은 추가해야 할 사항이나 개선해야 할 부분을 찾았다. (Issue 발생)
3. 프로젝트 멤버가 그 Issue에 대해 문서 또는 제안서를 작성한다. (Issue 열기 및 Issue Number 부여)
3. Branch를 분기하여 해당 Branch에서 Issue에 대한 개발을 진행한다. (커밋 시 이슈번호 명시하기)
4. 코드 작성이 완료되면 Pull Request를 보낸다. (내 코드를 가져가달라고 요청하기)
5. 팀원들이 해당 코드를 Approve하기 위해 Code Review를 진행한다.
6. 정상적인 코드임을 검토한 뒤 Merge(합병)한다.

참고로 GitHub에 있는 Repository, 즉 원격 저장소에 연결하기 위해서는 당연히 로컬 저장소에도 git 저장소를 생성해야 연결이 가능하다. 밑에서 나의 로컬 저장소에 Git Repos.를 초기화하고 GitHub에 올려보는 실습을 해볼 예정이다.

### CLI를 통한 실습

```sh
# Tip : 맥북에서 Markdown CodeBlock을 이용하기 위해선 영어로 전환하고 ~ 키를 누르자

git config --global user.email "minjunseong@naver.com"
git config --global user.name "minjunseong"
# 내가 수정하고자 하는 코드에 이력을 남기기 위해선 누군지 명시를 해야한다.
# 한글 사용은 '지양' 하도록 하자...
```

```sh
# 언제 이 코드를 다 칠까.. 단축어를 사용하는 팁 (alias 활용)
git config --global alias.<단축어> <명령어>
# e.g. git config --global alias.st status -> git st 만 쳐도 status를 볼 수 있음.
```

### 잠깐!
여기서 알고가면 좋은 개념

깃의 저장공간은 어떻게 분류될까?

- 작업 공간 (Working Directory == Working Tree)
- Stage
- 실제 기록 공간 (Repository)

#### Tracking, Staging?
- 우선 **Tracking** 과 **Untracking**이란 ?
**Tracking**은 깃이 현재 수정 상황을 추적하고 있는 것, **Untracking**은 앞서 언급한 것에 대한 반대 상태.
파일이 한번이라도 Add인 상태가 되면, 그 파일은 Tracking중. 하지만 Add되지 않은 파일들은 working pwd에 있더라도 Untracking이다.

→ Untracking된 파일은 commit이 안될 뿐 더러, Untracking된 파일을 수정해도 이력에 남지 않는다.

→ .gitignore을 통해서 파일을 untracking 처리 할 수 있다. (뭐 예를들면.. 디버깅 하려고 확인한 output files(e.g. : a.out)을 나의 git 저장소에 안 보이게 하고 싶으면 이를 활용해 볼 수 있을 것 같다.) / 외에도 토큰과 같은 예민한 정보를 은닉하고싶을 땐 untracking해주는 것이 용이하다.

- **Unmodified, Modified, Staged?**
  - Unmodified는 git add 명령어를 수행한 뒤에 파일을 아무것도 건들지 않으면 Unmodified 상태이다.
  - Modified는 add 명령어를 수행한 뒤 뭔가 수정이 되면 Modified 상태. (add한 뒤 파일을 삭제하게 되어도 마찬가지로 Modified이다)
  - Staged는 Git 저장소에 정상적으로 등록된 상태.

#### Bash 환경이 익숙하지 않은 사람들을 위한 Git 실습을 하며 쓰일 아주 간단한 터미널 용어 정리
```sh
ls          # 현재 있는 폴더에서의 파일들을 본다
ls -a       # 현재 있는 폴더에서의 '모든(숨겨진 파일 포함)' 파일들을 본다.
pwd         # 현재 내가 어느 폴더에 위치해있는지 확인해본다
mkdir       # 폴더 생성 (make directory의 약어)
cd ..       # 경로 이동 할 때 쓰인다. (choose directory의 약어) / cd .. 하면 상위 폴더, cd 경로 하면 해당 경로로 이동한다.
echo        # echo 명령어는 사실 다양하게 쓰인다. 화면에 출력하기도, 리다이렉션을 통한 생성을 하기도.. 밑에 예시를 적어야겠다
cat         # 파일의 내용을 출력할때 잘 쓰인다

echo 안녕하세요                     # 이러면 터미널 창에 안녕하세요 를 출력해준다.
echo "# 안녕하세요" >> tmp.md       # 이와 같이 파일 내용을 적고 만드는것도 가능하다.
cat tmp.md                          # tmp.md 내의 내용물을 확인할 수 있다.
```

#### 기본적인 Git 명령어 CLI 실습
```sh
git clone [해당 주소]
# 해당 주소의 repository를 나의 로컬 폴더에 가져올 때 쓴다.

git fetch
# pull과 유사. merge는 따로 하지 않는다. (누군가 커밋한거에 대한 사항을 갱신할 때 쓴다.)

git init
# 내가 이 명령어를 치는 터미널에 위치한 Directory (pwd) 에서 은닉폴더인 Git Repository를 생성
# 해당 터미널에서 git 은닉폴더가 어떻게 만들어졌는지 확인하기 위해선 ls -a command를 입력해서 확인해보자. (.git 형태로 있을 것! 여기서 파일 명 앞에 Dot(.)이 붙으면 숨김폴더이다.)

git remote add origin "Repository 주소(GitHub 예시 : https://github.com/username/repositoryname)"
# 어떤 Repository에 업로드 할 것인가?
# 참고로 git remote add [별칭] [주소] 로 하는 이유는, 주소의 이름을 short doamin으로 쓰더라도 매번 치기 번거로우니까 별칭을 이용해서 지정해준다. 별칭은 주로 "origin"을 많이 쓴다.

git remote remove origin
# 이미 repository에 연결되어있다면 기존에 연결되어있는 repository와 연결을 끊어주고 진행하기 위한 코드

git remote -v
# remote 상태가 정상적인지 확인 (내가 어떤 도메인의 레포지토리에 접근했는가?)

git add 파일명
# 파일의 변동 사항을 추적하기 위해 add 한다. 만약 add . 와 같이 사용한다면 해당 디렉토리의 모든 파일을 tracking한다.

git commit -m "커밋(수정/변동) 내용"
# 수정이 완료된 소스를 서버로 전송하기 위해 "메시지"와 함께 커밋한다. (커밋 메시지를 작성하지 않을 경우 커밋되지 않는다.)

git pull origin master # master 대신 branch 명 아무거나
# 나는 master branch에서 작업을 했기에, 그리고 해당 Repos에는 master branch만 잔존하기에 이와 같이 사용했다. 
# 하나하나 뜯어서 말하자면, origin(https://github.com/username/repositoryname)의 해당 레포지토리를 pull 하는 것이다.
# pull을 하는 이유는 프로젝트에 갱신된 내용이 있을 수 있기 때문이다.

git push origin master
# pull & push를 통한 동기화 작업
# 서버에 push하여 나의 소스코드를 전송한다.

git branch
# 해당 Git에 어떤 분기들이 있는지 확인 

git branch [브랜치 이름]
# 브랜치 이름에 해당하는 브랜치를 생성한다. -r을 이용하면 원격 브랜치들을 확인 가능.
# git checkout -b [브랜치 이름] 을 적어도 된다.

git branch -D [브랜치 이름]
# 브랜치 이름에 해당하는 브랜치를 삭제한다. (-D는 강제 삭제 옵션. -d를 주로 사용해보자.)

git checkout [존재하는 브랜치 이름]
# 해당 브랜치로 이동한다.

git diff
# Working Directory와 Staging Area사이에서의 차이점을 확인한다. (수정 변동 내역 확인할 때. / q를 이용해서 escape 가능.)
```

### Pull과 Push의 순서 ?
다른사람들과 작업을 할 때, Merge Conflict가 발생할 수 있다. 따라서, Pull을 먼저 해준 뒤에 Push를 해주는 것이 좋다.

충돌 방지용으로 권장하는 순서는 다음과 같다:
> pull → 코드 작성 → commit → pull → push

새로운 커밋 내용들이 있을 수 있으니, pull을 자주 하는 습관을 들이는 것도 좋다고 한다.

하지만 무분별한 push와 pull의 사용은 commit 이력을 꼬이게 하므로 주의해서 사용해야한다.

### 그럼 깃의 작동 과정은 어떻게 되나요?
위에서도 간접적으로 많이 언급되긴 했지만, 이를 좀 더 명료하게 적어보도록 하겠다.
사실 그림으로 이해하는게 좀 더 직관적일 수 있지만, 텍스트로 적어보자면

1. init을 통해 현재 디렉토리에 git 폴더를 생성하여 초기화 해준다.
2. 해당 폴더에서 열심히 코딩해준다.
3. git add를 통해 해당 폴더에 있는 파일들을 추적 상태로 둔다 (Tracking)
4. Staging Area에서 변경 이력들을 감시한다. (이때의 변경 이력들은 Working Dir가 아닌 Staging Area에서 감시된다.)
5. commit을 하게 되면 Local Repository에 로컬 Git의 데이터(Staging Area에서 수정된 데이터)들이 반영된다
6. pull을 통해 원격 저장소(Remote Repository)의 변동 정보들을 가져온다.
7. push를 통해 원격 저장소에 반영한다.

### Clone, Fetch, Pull, Merge
- Pull : 가장 최신 상태의 Repository를 내 로컬로 불러와, Merge한 상태로 두는 것 (fetch와 merge를 동시에 수행)
- Clone : 내 로컬 저장소에 git Repository를 복사해 오는 것
- Merge : 작업 내용을 합칠 때 쓰인다 (e.g. : 내가 다른 branch에서 작업을 하고, master branch로 병합할 때)
- Fetch : 다른 사람이 수정한 코드를 확인하고 가져올 수 있다.

### Branch는 왜 이용하는걸까?
우선 Branch는, 기존 폴더를 복제하는 것이 아닌 하나의 가상 폴더를 하나 생성하여 복제한다.

원본(master 혹은 main branch)과 분리된 상태로 개발을 진행할 수 있기에, 유지보수 측면에서 애용한다고 볼 수 있다.

Branch를 분기하여 개발하면, 분리된 브랜치에서 소스 코드를 각자 수정한 후 원본 코드에 병합하는 명령만 실행하면 된다. 

이러한 특성 덕에 깃의 Branch는 규모가 큰 코드 수정이나 병합을 처리할 때 필수적이라고 볼 수 있다.


### Pull Request (PR) 이란?
내가 수정한 코드를 프로젝트장 혹은 PM에게 요청해서 검토해달라고 하는 과정. 

PR 대상의 Repos를 나의 Github 저장소에 Fork해와서 commit하거나, 해당 프로젝트의 Repos를 나의 로컬 영역으로 가져와서 분기를 생성해서 하는 방법도 있다.

사실 위에 GitHub 설명 예시에 과정이 자세하게 적혀있다.


## 추가로 ..
### Readme 문서의 특징
Readme 문서는 쉽게 말해 프로젝트의 명세서와 같은 존재이다. 어떤 프로젝트를 GitHub에서 마주하게 된다면, 가장 맨 처음에 보게 될 화면이기도 하다.

Readme문서는 특별히 정해진 틀 같은건 존재하지 않는다. 사실 확장자도 꼭 .md 문서로 안해도 되는 부분이다. (그래도 가급적이면 .md형 파일을 지향한다. ~~남들 다 하는걸 안하는 역행자가 되진 말자~~)

다만, 해당 프로젝트가 어떤 프로젝트인지는 명시하는 것이 좋기에 보통은 다음과 같이 작성을 한다 : 

> - 프로젝트 구성
> - 프로젝트 프로그램 설치방법
> - 프로젝트 프로그램 사용법 (Requirements, Prerequisites 등을 자세히 적어두자)
> - 저작권 및 사용권 정보
> - 프로그래머 정보
> - 버그 및 디버그
> - 참고 및 출처
> - 버전 및 업데이트 정보
> - FAQ
> Ref : https://velog.io/@gmlstjq123/Readme.md-%ED%8C%8C%EC%9D%BC-%EC%9E%91%EC%84%B1%EB%B2%95

사실상 장난감을 사도 설명서가 없는 장난감이 없듯, 프로젝트를 하게 된다면 README 파일은 거의 필수적이다. 직관적이고 명확한 작성법에 대해 꼭 숙지해야할 부분이라고 본다.

### Bonus : Readme Profile
GitHub에서 내가 어떤 사람인지(혹은 포폴용.., 내가 어떤 Tech Stack을 가지고 있고 어느 프로젝트를 수행할 수 있는가에 대한 척도)를 나타내고 싶을 때, 본인 username으로 README 파일을 생성한다면, GitHub User 메인 화면에 표시할 수 있다.

포트폴리오처럼 학력, 이용하는 기술, 협업했던 프로젝트들, 수상 이력, 연락처 등을 적곤 한다. 밋밋한 본인의 깃허브를 꾸밀 수 있는 방법 중 하나이다. (단, Public Repos.로 등록해야 보인다.)

### Markdown 문서(확장자 .md)란?
Readme 파일을 작성해야 하는 이유는 잘 알겠지만, 해당 파일을 작성하는 문법에 대해서도 알아야 할 필요가 있다.

흔히들 개발을 접하면 HTML에 대해서는 다들 잘 알 것이다. HTML의 약어를 보면 M의 약어가 Markup임을 알 수 있다.

당연히 HTML이 사용하는 양식과 Markdown의 양식은 다르나 둘이 설명하기 위한 '문서'라는 유사성을 갖고 있다.

다만, HTML과의 차이로는 <>와 같이 태그 표현을 쓰지 않고, 오직 문서 작성에만 초점이 맞춰진 걸 볼 수 있는데,
사용법이 간단해서 .md 파일을 주로 사용하곤 한다. (그래도 html 문법이 일부 적용이 되기도 한다.)

자주 사용하는 마크다운 문법들을 좀 간략하게 보자면,
```
#의 갯수 1~6 : 1이 가장 큰 글씨, 6이 가장 작은 글씨로 Heading하는 역할! (Bold체)
~~글자~~ : 취소선
**글자** : 굵은글씨
- : 세부 문단 분리할때 쓰임
> : 인용구를 만들어준다. 
`3개 코드 `3개 : 코드 블럭 생성 (첫 `3개 옆에 어떤 언어를 사용했는지 적으면 해당 언어에 대한 Highlighting도 지원한다.)
!()[] : ()는 표시되는 내용, []는 하이퍼링크 블록이다.
- - - : 구분선

* 기타 html문법을 이용해도 마크다운에 적용되기도 한다.
```


## 마치며 ..

사실 나는 GitLens와 같은 VSCode Extension에 의존하여 GitHub에 커밋하곤 했는데, CLI환경에서의 반복적인 실습을 해보니 Git의 작동 구조에 좀 더 친숙하게 다가갈 수 있었던 것 같다. 

다른 개발자들도 Extension에만 의존하지 말고 CLI환경에서 직접 실습해보는 Experience가 있으면 좋겠다는 마음이 있다.

또한, 협업 과정에서 GitHub에 커밋을 할 때 주의해야 할 점이나, PR시에 해야할 행동 등을 숙지할 수 있어서 한번 쯤은 Git에 대한 개념을 자세히 짚고 갈 필요가 있다고 생각한다. 

생각보다 알아야 할 내용도 많고, 숙지해야 할 내용도 많다. 한 문서에 Git에 대한 내용을 다 담기 어려울 것 같아서 중구난방해질 듯 하니 (1)과 (2)로 나누어서 개념 정리를 할 예정이다.