# 앱센터 Basic 스터디 16.5기
> Since 2024.10.02

## 👩🏻‍💻 운영진

|**한현승**|
|:-:|
| <a href="https://github.com/82everywin"><img src="https://avatars.githubusercontent.com/u/109841880?v=4" width="120"></a> |    
---

## 👫 파트원

|나현지|박다인|성민준|정석환|
|:-:|:-:|:-:|:-:|
| <a href="https://github.com/hxxneei"><img src="https://avatars.githubusercontent.com/u/183292376?v=4" width="120"></a> |<a href="https://github.com/pdain"><img src="https://avatars.githubusercontent.com/u/180918895?v=4" width="120"></a>| <a href="https://github.com/milin3t"><img src="https://avatars.githubusercontent.com/u/103179228?v=4" width="120"></a> |<a href="https://github.com/Jungseokhwan"><img src="https://avatars.githubusercontent.com/u/155729481?v=4" width="120"></a>|
---


## 📝 규칙
 
- `커밋 컨벤션`
    - `Feat`: 새로운 기능 추가
    - `Fix`: 버그 수정
    - `Docs`: 문서 수정 
    - `Style`: 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우
    - `Refactor`: 코드 리팩토링
    - `Test`: 테스트 코드, 리팩토링 테스트 코드 추가
    - `Chore`: 빌드 업무 수정, 패키지 매니저 수정
    
  <br><br>

- `issue 규칙`
    - 참고: [https://velog.io/@junh0328/협업을-위한-깃허브-이슈-작성하기](https://velog.io/@junh0328/%ED%98%91%EC%97%85%EC%9D%84-%EC%9C%84%ED%95%9C-%EA%B9%83%ED%97%88%EB%B8%8C-%EC%9D%B4%EC%8A%88-%EC%9E%91%EC%84%B1%ED%95%98%EA%B8%B0)
    - 레이블 참고:
      [https://github.com/modolee/github-initial-settings](https://github.com/modolee/github-initial-settings)
    - 제목 참고: [https://doublesprogramming.tistory.com/256](https://doublesprogramming.tistory.com/256)
      <br><br>
    - 템플릿
        - issue 제목
            - 예시: **[Feat] 이슈 정리**
          <br><br>
          
        - issue 템플릿

            ```markdown
            ## 📋 이슈 내용
            
            ## ✅ 체크리스트
          
            ## 📚 레퍼런스
            
            ```
    <br><br>
      
- `branch 규칙`
    - 작업하려는 종류와 이슈번호를 이용하여 브랜치명을 작성합니다.
    - 예시:
    ```
  git checkout -b <브랜치명>      
  git checkout -b feat/#3
    ```
  <br><br>

- `commit message 규칙`
    - 참고: [https://doublesprogramming.tistory.com/256](https://doublesprogramming.tistory.com/256)
    - 종류: 메시지 - #이슈번호
    - 예시
        - feat: todo-list 회원 API 엔티티 구현 - #2
        - fix: todo-list 회원 단건 조회 서비스 에러 수정 - #2
    
    <br><br>
      
- `PR 규칙`
    - PR 템플릿

        ```markdown
        ## 📋 이슈 번호
            close#{이슈번호}
      
        ## 🛠 구현 사항
            구현한 사항에 대해서 적어주세요
      
        ## 📚 기타
        
        ```
