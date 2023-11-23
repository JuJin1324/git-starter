# Git-Starter
Git 시작을 위한 정리

## 설치
> macOS : `brew install git`  
> Windows 10 : `scoop install git`  
> Ubuntu: `sudo apt install -y git`  

---

## 사용법
### 최초 설정
> 사용자 이름  
>  - 용법 : `git config --global user.name [사용자 이름]`  
>  - 예시 : `git config --global user.name jujin1324`  
> 이메일 설정  
>  - 용법 : `git config --global user.email [이메일]`  
>  - 예시 : `git config --global user.email jujin1324@daum.net`  
> 확인 : `git config --list`  

### 저장소 지정부터 커밋까지
> * `git init` : git을 사용하여 버전관리할 저장소 지정  
> * `git status` : 현재 브랜치 상태 확인  
> * `git add [파일명]` : commit 할 파일 지정  
> * `git commit` : 커밋  
>  * `git commit -a` : git의 모든 파일을 커밋함  
>  * `git commit -a -m “커밋 메시지”` : 모든 내용을 커밋하고 커밋 메시지를 남김 i를 누르고 맨 위에 커밋 메시지 작성 후, :wq로 나감  
> * `git log` : 커밋 기록 확인  
>  
> * add 하지 않을 파일 목록 생성
> ```bash
> $ touch .gitignore
> 혹은
> $ vi .gitignore   
> ```

### checkout 명령어
> checkout 명령어는 Git 에서 오래 전부터 지원하던 명령어인데, 너무 많은 기능을 포함하고 있다. 그래서 최근에는 checkout 명령어의 주요 기능이 `switch` 명령어와
> `restore` 명령어로 나누어졌다.  
> checkout 명령어처럼 커밋 아이디를 지정해서 되돌아가는 명령어는 다소 위험하므로 실무에서는 잘 사용하지 않는다.

### add 취소하기
> `git reset HEAD`  
> 참조사이트: [[Git] git add 취소하기, git commit 취소하기, git push 취소하기](https://gmlwjd9405.github.io/2018/05/25/git-add-cancle.html)

### 브랜치 사용
> * `git branch` : 브랜치 보기  
> * `git branch [브랜치명]` : 지정한 브랜치 이름으로 브랜치가 새로 만들어짐  
> * `git branch -d [브랜치명]`: 지정한 브랜치 삭제  
> * `git checkout [브랜치명]` : 현재 작업 브랜치를 해당 브랜치로 변경(단, 변경 전에 해당 브랜치에서 발생한 변경점들은 커밋이 되어야함)   
> * `git checkout -b [브랜치명]` : 브랜치를 만듬과 동시에 현재 작업 브랜치로 변경  
> * `git checkout master` : 마스터 브랜치로 변경 후에 git merge hotfix 로 hotfix와 병합 충돌이 일어난 경우 hello.c로 들어가서 파일을 수정하면 된다.   
> * `git branch -m [브랜치명]`: 현재 브랜치명을 입력한 브랜치명으로 변경한다.  
> * `git branch -m [브랜치명1] [브랜치명2]`: 브랜치명1을 브랜치명2로 변경한다.  

### 체리 픽(Cherry-Pick)
> git cherry-pick은 제목과 마찬가지로 필요한 commit만 골라서 가져오는 명령어이다.  
> 다른 브랜치와 merge 하는 것이 아닌 원하는 commit 과 merge 하는 개념이다.  
>
> git cherry-pick은 유용한 도구이지만 같은 commit이 중복되는 일이 발생하거나 그 외에도 여러가지 문제가 발생할 수 있기 때문에 꼭 필요한 상황에서만 사용하는 것을 권장한다.
> * 팀으로 협업할 때
> 팀으로 협업을 진행하고 있을때, 다른 동료가 만들고 있는 기능이 필요한 순간이 있다. 만약 동료가 해당 기능을 이미 다 만들어 놨고, 동료가 맡은 모든 작업을 merge 할 때까지 시간이 걸린다면 동료가 만들었다는 기능이 들어있는 commit만 골라서 가져올 때 사용한다.  
> * 버그를 수정할 때
> 새로운 기능을 개발하는 동안 기존에 있던 기능에서 버그가 발견되었을 때, 개발자는 이 버그를 패치하기위해 명시적 커밋을 만들고 해당 커밋만 골라서 master 브랜치에 배포할 수 있다.  
> * 반영되지 않은 손실된 커밋 복원 (pull request)
> 실수로 pull request를 merge하기 전에 닫아버렸을 때, cherry-pick을 사용해 해당 commit을 가져옴으로써 살릴 수 있다.  
> 
> **출처**
> [나만의 기록들:티스토리](https://mine-it-record.tistory.com/650)

### 리베이스(Rebase)
> 다음과 같이 feature 브랜치는 main 브랜치의 m1 커밋을 기반으로 작업했는데 f2 까지의 커밋을 main 브랜치로 병합하려는 경우.
> ```
> m1 -> m2 -> m3(main)  
>    -> f1 -> f2(feature)  
> ```
> feature 브랜치를 main 브랜치에 리베이스하면 다음과 같은 상태로 변한다.
> ```
> m1 -> m2 -> m3(main) -> f1 -> f2(feature)
> ```
> 그럼 이 상태로 PR 을 보내면 된다.

### 리셋(Reset)
> 현재 브랜치를 원하는 커밋으로 되돌리는 기능이다.   
> **Hard**  
> 현재 브랜치에서 작업하던 것을 완전히 제거 후 원하는 커밋으로 돌아간다.  
> 
> **Soft**  
> 현재 브랜치에서 작업하던 것을 제거하지 않고 원하는 커밋으로 돌아간다. 현재 브랜치에서 작업 중이던 파일은 스테이지에 올라가 있다.  
> 
> **Mixed**  
> 현재 브랜치에서 작업하던 것을 제거하지 않고 원하는 커밋으로 돌아간다. 현재 브랜치에서 작업 중이던 파일은 스테이지 아래로 내려가 있다.
> 
> 과거의 커밋으로 리셋 한 경우, 원격 저장소에 반영하기 위해서는 Force Push 가 필요하다.   

### 리버트(Revert)
> 리셋은 커밋을 마치 없었던 일처럼 되돌리는 방법이다. 하지만 모두가 쓰는 브랜치라 이력 관리가 중요하다면 리셋을 하는 것보다 변경 사항을 되돌리는 새로운
> 커밋을 만드는 것이 더 좋다. 이럴 때 사용하는 것이 리버트이다.  
> 
> 리셋과의 차이라면 리셋은 리셋한 커밋의 이후 커밋은 모두 제거하는 것이다.  
> 리버트는 잘못된 커밋이 있을 때 해당 커밋을 제거하지 않고 해당 커밋의 내용을 제거했다는 커밋을 새로 남기는 것이다.  

### 스태시(Stash)
> 파일 변경이 발생했을 때 다른 브랜치로 이동하고 싶은 경우에 변경한 파일을 커밋하고 브랜치를 이동하거나 아직 변경 중이라서 커밋하기 싫은 경우 
> 스태시로 변경 파일을 임시 저장 후 브랜치를 이동할 수 있다.

---

## 원격저장소
### GitHub
> `fork` : 다른 사람의 저장소를 내 저장소로 복사    
> `Pull request` : 포크한 저장소에서 내가 수정 후에 원본 사용자에게 병합해달라고 요청    

### 원격저장소와 로컬 저장소 동기화
> `git clone` : 원격저장소(ex: GitHub)에서 로컬 저장소로 복사  
> 예시)
> ```bash
> $ git clone https://github.com/JuJin1324/command_hello.git
> ```
>  
> `git remote` : 로컬 저장소를 원격 저장소와 연결     
> ※ github에 repository 생성 후 "clone or download" 버튼 클릭 -> 해당 주소 복사    
> 예시) 
> ```bash
> git remote add origin https://github.com/JuJin1324/Git-Command.git  
> ```
> `git remote -v` : 원격 저장소와 연결되었는지 확인   
> `git push` : 로컬 git에 commit을 원격저장소로 업로드  
> `git push origin --all` : 전체 푸쉬  
> `git push origin master` : origin의 master 브랜치만 푸쉬  
> ※README.md 파일을 만들어서 꼭 푸쉬하시길..  
> `git push -f`: 로컬의 깃 내용을 리모트에 강제로 덮어쓰기   
> `git pull` : 원격저장소의 최신버전을 로컬로 다운로드  

### 원격저장소 커밋 되돌리기
> 로컬 커밋 간소화 확인 - `$ git log --pretty=oneline --abbrev-commit`  
> 
> [참조 링크](https://jupiny.com/2019/03/19/revert-commits-in-remote-repository/)  

### 추천 Extension
> Octotree: github chrome extension, 다운로드 링크: [chrome 웹 스토어](https://chrome.google.com/webstore/detail/octotree/bkhaagjahfmjljalopjnoealnfndnagc/related?hl=ko)

### Conventional Commits
> Conventional Commits 스펙은 커밋 메시지에 곁들여진 가벼운 컨벤션으로 명확한 커밋 히스토리를 생성하기 위한 간단한 규칙을 제공한다. 
> 이렇게 만들어진 커밋 히스토리를 이용하여 더 쉽게 자동화된 도구를 만들 수 있다.
> 
> Conventional Commit 의 메시지 구조
> ```
> <타입>[적용 범위(선택 사항)]: <설명>
> 
> [본문(선택 사항)]
> 
> [꼬리말(선택 사항)]
> ```
> 
> 타입의 종류
> * feat: features (기능 개발 관련, `MINOR` 버전 변경)
> * docs: documentations (문서화 작업)
> * conf: configurations (환경설정 관련)
> * test: test (test 관련)
> * fix: bug-fix (오류 개선 혹은 버그 패치, `PATCH` 버전 변경)
> * refactor: refactoring
> * ci: Continuous Integration
> * build: Build (빌드 관련)
> * perf: Performance
> * improvement: 새로운 기능이나 버그 수정 없이 현재 구현체를 개선하는 커밋
> * chore: 그 외 실제 코드에는 영향이 없는 단순 수정
> 
> 본문 내용
> * BREAKING-CHANGE: `BREAKING-CHANGE` 이라는 꼬리말을 가지거나 타입/스코프 뒤에 !문자열을 붙인 커밋은 단절적 API 변경(breaking API change)
> 있다는 것을 의미합니다 (이는 유의적 버전에서의 `MAJOR` 와 관련이 있습니다). 어떤 커밋 타입이라도 BREAKING CHANGE 는 해당 커밋의 일부가 될 수 있습니다.
> * Closes: 지라와 같은 프로젝트 관리 툴에서 일감 적용을 완료했을 때 사용.
> 
> commit 할 때 기억해야할 것
> * commit 은 동작 가능한 최소단위로 자주 할 것.
> * 해당 작업단위에 수행된 모든 파일 변화가 해당 commit에 포함되어야 함.
> * 모두가 이해할 수 있는 log를 작성할 것.
> * Open Source Contribution시 영어가 강제되지만, 그렇지 않을 경우 팀 내 사용 언어를 따라 쓸 것.
> * 제목은 축약하여 쓰되(50자 이내), 내용은 문장형으로 작성하여 추가설명 할 것.
> * 제목과 내용은 한 줄 띄워 분리할 것.
> * 내용은 이 commit의 구성과 의도를 충실히 작성할 것.
> 
> 예제
> 본문에 설명과 BREAKING CHANGE 를 가지는 커밋 메시지
> ```
> chore!: drop Node 6 from testing matrix
> 
> BREAKING CHANGE: dropping Node 6 which hits end of life in April
> ```
> 본문이 없는 커밋 메시지
> ```
> docs: correct spelling of CHANGELOG
> ```
> 적용 범위를 가지는 커밋 메시지
> ```
> feat(lang): add polish language
> ```
> 옵션이 이슈 번호를 가진 fix 타입의 커밋 메시지
> ```
> fix: correct minor typos in code
> 
> see the issue for details on the typos fixed
> 
> closes issue #12
> ```
> 커밋 컨벤션 예제
> ```
> feat: Create server.py to start flask project
> docs: Create README.md
> conf: poetry init
> test: User model CRUD test complete
> ```
> 
> **참조사이트**  
> [Conventional Commits에 관하여](https://velog.io/@hustle-dev/Conventional-Commits에-관하여)
> [Conventional Commits](https://www.conventionalcommits.org/ko/v1.0.0/)

### 풀 리퀘스트를 병합하는 세 가지 방법
> 1.병합 커밋 생성(Create a merge commit): 가장 기본 방법이다. 두 브랜치 상태를 비교해서 새로운 커밋을 만들면서 코드를 병합한다.
> 
> 2.스쿼시해서 병합(Squash and merge): PR 의 커밋들을 하나로 퉁쳐버린 후 브랜치의 최신 커밋과 합친다.  
> PR 에 커밋을 아무리 많이 올렸어도 main 브랜치의 커밋 히스토리에는 PR 마다 커밋 1개만 남는다는 장점이 있다. 병합 커밋 생성과는 달리
> 새로 생긴 커밋이 main 브랜치의 최신 커밋만 부모로 가리킨다. 이로 인해 main 브랜치의 히스토리가 한 줄로 깔끔하게 남는다.  
> 
> 3.리베이스해서 병합(Rebase and merge): 위에서 했던 리베이스 설명과 같다.  

### 브랜치 보호하기
> GitHub 의 Repository 에 Settings 탭을 클릭하고 왼쪽 메뉴에서 Branches 를 클릭하여 브랜치 설정 페이지로 이동한다.  
> Branch protection rules 항목의 Add branch protection rule 버튼을 클릭한다.  
> 
> Branch name pattern 항목에 지정할 브랜치 이름을 입력한다. 브랜치 이름을 입력할 때는 와일드카드(*)를 활용할 수도 있다.  
> ex) feature/ 로 시작하는 모든 브랜치: `feature/*`  
> 다음으로 Protect matching branches 항목에 Require a pull request before merging 과 Require approvals 옵션에 체크한다.  
> 보통 이 두 옵션을 함께 사용해서 리뷰를 강제하고 브랜치를 보호한다. 이렇게 하면 지정된 브랜치에는 반드시 다른 브랜치 커밋들의 PR 을 통해서만
> 커밋이 생성된다.  
> 
> Require approvals 옵션은 지정된 숫자만큼의 리뷰어 승인이 있어야만 PR 을 병합할 수 있게 하는 옵션이다.  
> 관리자에게도 규칙이 강제로 적용되게하려면 Do not allow bypass the above settings 옵션도 체크한다.

---
