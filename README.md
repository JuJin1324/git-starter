# Git-Starter
Git 시작을 위한 정리

## 개요
### 설치
> macOS : `brew install git`  
> Windows 10 : `scoop install git`  
> Ubuntu: `sudo apt install -y git`
>

### 용어정리
> **워킹트리(Working tree)**   
> 워킹트리, 워킹 디렉터리, 작업 디렉터리, 작업 폴더 모두 같은 뜻으로 사용된다. 일반적으로 사용자가 파일과
> 하위 폴더를 만들고 작업 결과물을 저장하는 곳을 Git 에서는 워킹트리라고 부른다.
> 
> **로컬 저장소**  
> git init 명령으로 생성되는 .git 폴더가 로컬 저장소이다.  
> 
> **원격 저장소**  
> 로컬 저장소를 업로드하는 곳을 원격 저장소라고 부른다.  
> 
> **Git 저장소**  
> 엄밀하게는 로컬 저장소를 의미하지만 넓은 의미로 작업 폴더(워킹트리 + 로컬 저장소)를 의미하기도 한다.  

---

## 브랜치(Branch)
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
> <타입>[적용 범위(선택 사항)]: <제목>
> 
> [본문(선택 사항)]
> 
> [꼬리말(선택 사항)]
> ```
> 
> **타입의 종류**  
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
> **제목 규칙**  
> * 제목은 50자 이내로 쓴다.
> * 제목에는 마침표를 넣지 않는다.
> * 제목을 영어로 쓸 경우 첫 글자는 대문자로 쓴다.  
> * 제목을 영어로 쓸 경우 현재형으로 시작한다.
> 
> **본문 내용**  
> * BREAKING-CHANGE: `BREAKING-CHANGE` 이라는 꼬리말을 가지거나 타입/스코프 뒤에 !문자열을 붙인 커밋은 단절적 API 변경(breaking API change)
> 있다는 것을 의미합니다 (이는 유의적 버전에서의 `MAJOR` 와 관련이 있습니다). 어떤 커밋 타입이라도 BREAKING CHANGE 는 해당 커밋의 일부가 될 수 있습니다.
> * Closes: 지라와 같은 프로젝트 관리 툴에서 일감 적용을 완료했을 때 사용.
> 
> **본문 규칙**  
> * 본문은 72자 단위로 줄바꿈한다.  
> * 어떻게 보다 무엇과 왜를 설명한다.
> 
> **commit 할 때 기억해야할 것**  
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

## CLI
### init
> 기본 명령어: `git init`
> 설명: 현재 디렉터리에 git 저장소로 초기화한다.   
> 옵션: `git init -b main`   
> 설명: 자동으로 초기화되는 Git 브랜치의 이름을 main 으로 지정할 수 있다.
> 2.42.1 버전까지도 브랜치 이름을 지정하지 않으면 자동으로 초기화되는 브랜치 이름은 master 이다.

### status
> 기본 명령어: `git status`  
> 설명: Git 워킹트리의 상태를 보는 명령으로 사용한다.   
> 옵션: `git status -s`  
> 설명: 사용하여 상태를 짧게 요약해서 보여줄 수도 있다.  

### config
> **현재 프로젝트의 모든 옵션 목록 확인**  
> 명령어: `git config --list`  
> 
> **사용자 이름 설정**  
> 명령어: `git config --global user.name [사용자 이름]`  
> 
> **사용자 이메일 설정**  
> 명령어: `git config --global user.email [이메일]`   
>
> **기본 에디터 설정**  
> 확인 명령어: `git config --global core.editor`    
> VS Code 설정 명령어: `git config --global core.editor "code --wait"`  
> 
> **기본 컬러 설정**  
> 자동 설정: `git config --global color ui auto`  
> 
> **기본 브랜치 명 설정**  
> main 으로 설정: `git config --global init.defaultbranch main`  
> 
> **참조사이트**  
> [Git과 텍스트 편집기 연결](https://docs.github.com/ko/enterprise-cloud@latest/get-started/getting-started-with-git/associating-text-editors-with-git?platform=mac)  

### checkout
> 명령어: `git checkout [브랜치명]`   
> 설명: 현재 작업 브랜치를 해당 브랜치로 변경(단, 변경 전에 해당 브랜치에서 발생한 변경점들은 커밋이 되어야함)  
> 
> 명령어: `git checkout -b [브랜치명]`  
> 설명: 브랜치를 만듬과 동시에 현재 작업 브랜치로 변경.  
> 
> checkout 명령어는 Git 에서 오래 전부터 지원하던 명령어인데, 너무 많은 기능을 포함하고 있다. 그래서 최근에는 checkout 명령어의 주요 기능이
> `switch` 명령어와 `restore` 명령어로 나누어졌다.  
> checkout 명령어처럼 커밋 아이디를 지정해서 되돌아가는 명령어는 다소 위험하므로 실무에서는 잘 사용하지 않는다.

### branch
> **브랜치 목록 조회**  
> 명령어: `git branch`  
> 설명: Commit 이 있는 브랜치들의 목록 조회  
> 
> **브랜치 생성**  
> 명령어: `git branch [브랜치명]`  
> 설명: 지정한 브랜치 이름으로 브랜치가 새로 만들어짐  
> 
> **브랜치 변경**  
> 명령어: `git switch [브랜치명]`  
> 설명: 지정한 브랜치로 변경한다.  
> 
> **브랜치 생성하면서 변경**  
> 명령어: `git switch -c [브랜치명]`  
> 설명: `git checkout -b [브랜치명]` 과 같다.  
> 
> **브랜치 삭제**  
> 명령어: `git branch -d [브랜치명]`  
> 설명: 지정한 브랜치 삭제  
> 
> **브랜치명 변경**  
> 명령어: `git branch -m [브랜치명]`  
> 설명: 현재 브랜치명을 입력한 브랜치명으로 변경한다.
> 
> 명령어: `git branch -m [브랜치명1] [브랜치명2]`  
> 설명: 브랜치명1을 브랜치명2로 변경한다.    
> 
> **병합**  
> 명령어: `git merge <대상 브랜치>`
> 
> **병합 취소**  
> 명령어: `git merge --abort`  
> 설명: 병합 충돌 시 병합을 취소하기 위한 명령어이다.  
> 
> **재배치**  
> 명령어: `git rebase [원본 브랜치]`  
> 설명: main 브랜치가 있고 내가 작업 중인 feature 브랜치가 있다고 예시를 해보자.   
> feature: 1 <- 3  
> main: 1 <- 2  
> feature 브랜치는 main 의 1번 커밋 뒤에 3번 커밋을 생성하여 3번 커밋을 가리키고 있었는데 main 에서 2번 커밋을 새로 만들었다.  
> feature 브랜치가 1 <- 2 <- 3 으로 커밋을 재배치하고 싶은 경우 feature 브랜치로 스위치 후 다음 명령어를 실행한다.  
> ```shell
> git switch feature
> git rebase main
> ```
> 주의: rebase 명령어는 주로 로컬 브랜치를 깔끔하게 정리하고 싶을 때 사용한다. 원격에 푸쉬한 브랜치를 리베이스할 때는 조심해야 한다.  
> 여러 Git 가이드에서도 원격 저장소에 존재하는 브랜치에 대해서는 리베이스를 하지 말 것을 권한다.  

### commit
> **파일을 스테이지에 추가**  
> 명령어: `git add <파일명> <파일명> ...`  
> 
> **커밋**  
> 명령어: `git commit`
> 설명: 스테이지에 있는 파일들 커밋. git config 에 core.editor 를 저장하고나서 git commit 을 하게되면 지정한 에디터가 열린다.
> 사용자는 열린 에디터에서 커밋 메시지를 편집하고 저장 후 닫으면 커밋이 완료된다.  
> 
> add 명령어 생략하고 바로 커밋: `git commit -a`  
> 
> 커밋 메시지 수정: `git commit --amend`  
> 
> **원격 저장소 업로드**  
> 명령어: `git push`  
> 
> 지정해서 업로드: `git push [원격 저장소명] [브랜치 이름]`  
> 
> **원격 저장소의 변경점을 로컬에 적용**  
> 명령어: `git pull`  
> 설명: git fetch + git merge 와 같다.   
>
> **언스테이징(unstaging)**  
> 명령어: `git reset HEAD`  
> 설명: 스테이지에 add 한 파일들을 모두 내린다.
> 
> **reset**  
> 명령어: `git reset --hard HEAD~[숫자]`  
> 설명: git reset --hard 명령을 사용하려면 커밋 체크섬을 알아야한다. CLI 에서 복잡한 커밋 체크섬을 타이핑하는 건 꽤 번거로운 작업이다. 이럴 때는
> 보통 `HEAD~[n]` 을 사용해서 현재 HEAD 의 n 번째 조상 커밋으로 리셋을 의미한다.  
> 
> **태그**  
> 명령어: `git tag -a -m [간단한 메시지] [태그 이름]`  
> 예시: `git tag -a -m "Release version 0.1" v0.1`  
> 
> 태그 푸쉬: `git push origin v0.1`  

### log 
> 명령어: `git log`  
> 설명: 커밋 히스토리를 확인한다.  
> 
> 그래프로 이쁘게 보이기: `git log --oneline --graph --all --decorate`    
> 최신 커밋 5개만 보기: `git log --oneline -n5`  

### remote
> 원격 저장소를 로컬 저장소와 연결한다. 다만 원격 저장소는 미리 만들어서 준비해둬야한다.  
> 명령어: `git remote add <원격 저장소 이름> <원격 저장소 주소>`  
> 설명: 통상 첫번째 원격 저장소를 origin 으로 저장한다.  
> 
> 원격 저장소 목록 확인: `git remote -v`

---

## Git 브랜치 전략
> Git 브랜치 전략은 프로젝트의 Git 브랜치를 효과적으로 관리하기 위한 워크플로우이다.
> 직접 브랜치 전략을 만들어 사용해도 되겠지만, 세상에는 브랜치를 효과적으로 관리하기 위한 모범 사례들이 존재한다.
> 그 모범사례 중 유명한 Git Flow, Github Flow 를 정리한다.

### Git Flow
> Git Flow 는 크게 `Main` 브랜치, `Develop` 브랜치, `Supporting` 브랜치로 구분하여 브랜치를 관리한다.   
> 이때, Supporting 브랜치는 또 다시 `Feature` 브랜치, `Release` 브랜치, `Hotfix` 브랜치로 나뉜다.
>
> **Main 브랜치**  
> Main 브랜치는 출시 가능한 프로덕션 코드를 모아두는 브랜치이다. Main 브랜치는 프로젝트 시작 시 생성되며, 개발 프로세스 전반에 걸쳐 유지된다.
> 배포된 각 버전을 Tag 를 이용해 표시해둔다.
>
> **Develop 브랜치**  
> 다음 버전 개발을 위한 코드를 모아두는 브랜치이다. 개발이 완료되면, Main 브랜치로 머지된다.
>
> **Feature 브랜치**  
> 하나의 기능을 개발하기 위한 브랜치이다. Develop 브랜치에서 생성하며, 기능이 개발 완료되면 다시 Develop 브랜치로 머지된다.
> 머지할때 주의점은 Fast-Forward 로 머지하지 않고, Merge Commit 을 생성하며 머지를 해주어야 한다. 이렇게해야 히스토리가 특정 기능 단위로 묶이게 된다.  
> 네이밍은 feature/branch-name 과 같은 형태로 생성한다.
>
> **Release 브랜치**  
> 소프트웨어 배포를 준비하기 위한 브랜치이다. Develop 브랜치에서 생성하며, 버전 이름 등의 소소한 데이터를 수정하거나 배포전 사소한 버그를 수정하기 위해 사용된다.
> 배포 준비가 완료되었다면 Main 과 Develop 브랜치에 둘다 머지한다. 이때, Main 브랜치에는 태그를 이용하여 버전을 표시한다.  
> Release 브랜치를 따로 운용함으로써, 배포 업무와 관련없는 팀원들은 병렬적으로 Feature 브랜치에서 이어서 기능을 개발할 수 있게된다.  
> 네이밍은 release/v1.1 과 같은 형태로 생성한다.
>
> **Hotfix 브랜치**  
> 이미 배포된 버전에 문제가 발생했다면, Hotfix 브랜치를 사용하여 문제를 해결한다. Main 브랜치에서 생성하며,
> 문제 해결이 완료되면 Main 과 Develop 브랜치에 둘다 머지한다.  
> Release 브랜치와 마찬가지로 Hotfix 브랜치를 따로 운용함으로써, 핫픽스 업무와 관련없는 팀은 병렬적으로 기능 개발을 할 수 있다.  
> 네이밍은 hotfix/v1.0.1 과 같은 형태로 생성한다.
>
> **Git Flow 의 한계: 웹 어플리케이션에는 적합하지 않다.**  
> 즉, Git Flow 는 명시적으로 버전관리가 필요한 이를 테면, 스마트폰 어플리케이션, 오픈소스 라이브러리/프레임워크 등의 프로젝트에 적합하다.  
> 웹 어플리케이션은 특성상 사용자는 항상 최신의 단일 버전만을 사용하게된다. 여러 버전을 병렬적으로 지원할 필요가 없는 것이다.
> 또한 웹 어플리케이션은 하루에 몇번이고 릴리즈될 수 있다. 이런 특성상 웹 어플리케이션 개발에 Git Flow 는 다소 적합하지 않다.

### GitHub Flow
> Git Flow 는 대부분의 케이스에서 매우 복잡하다. 기계적으로 규칙을 따르기만 하면 큰 문제 없다고 하지만, 결국 복잡하기 때문에 많은 사람들이 실수하고 헤매게된다.
> Github Flow 는 Git Flow 와 다르게 굉장히 간단한 구조이다.
>
> **Main 브랜치**  
> 항상 Stable 한 상태여야 한다. 이때, Stable 하다는 것은 Main 의 모든 커밋은 언제 배포하든 문제 없어야하고,
> 언제든 브랜치를 새로 만들어도 문제가 없어야 한다. Main 브랜치의 모든 커밋은 빌드가 되고, 테스트를 통과해야한다.
> 이것이 Github Flow 가 강제하는 유일한 사항이다.
>
> **Topic 브랜치**  
> 새로운 기능을 개발할 때에는 Topic 브랜치를 Main 브랜치로부터 생성한다. Git Flow 의 Feature 브랜치와 동일한 역할을 한다.
> 또한 별도로 Hotfix 브랜치를 관리하지 않으며, 버그 수정도 Topic 브랜치에서 진행한다.
> 이때, Topic 브랜치의 이름은 기능을 설명하는 명확한 이름으로 네이밍 해야한다.
> 예를 들면, user-content-cache-key, submodules-init-task, redis2-transition 등이 있다.  
> Topic 브랜치의 커밋은 기능이 완성되지 않았더라도 꾸준히 Push 한다. 노트북 분실, 작업 컴퓨터의 고장등의 위험으로 코드가 유실되는 것을 막아준다.
> 이것보다 더 중요한 이유는 꾸준히 Push 함으로써 구성원 모두가 끊임없이 커뮤니케이션 할 수 있게 해준다.
> Github 에서는 PR(Pull Request)라는 유용한 기능이 존재한다. 개발자는 기능을 개발하는 중 언제든 상관없이 PR을 개설할 수 있다.
> 심지어 코드의 변경이 없더라도 스크린샷, 아이디어를 공유하고 싶을 때에도 PR을 개설한다.
> 개발자들은 개설된 PR에서 토론을 하고, 코드의 특정 라인을 선택해 코멘트를 남겨 코드리뷰를 주고 받는다.
> 토론과 리뷰가 끝났으면, 다른 사람들의 동의(Approve)를 얻고 Main 브랜치에 자신의 Topic 브랜치를 머지한다.
> 단, 이때 Topic 브랜치는 자동화된 CI 빌드를 통과해야 머지가 가능하다.
>
> **참조할만한 규칙**
> * 원격 저장소(origin)의 main를 로컬 저장소에서 pull 해서 가져온다.
> * 로컬 저장소의 main에서 기능 개발을 위한 브랜치(feature branch)를 만들고 작업한다.
    > 기능 개발 전, 이슈트랙커에 이슈를 추가한다: docs 를 제외한 모든 작업(기능, 디자인, 버그, 리팩토링, 세팅)은 모두 추가한다.
    > docs 는 main branch 에 바로 업로드한다.  
    > 브랜치 이름은 기능이 두드러지도록 한다: ex. feature/home-ui
> * 작업한 내역을 원격 저장소에 push 한다.
> * 원격 저장소에서 feature branch에서 main branch로 PR을 날리고, 코드 리뷰를 진행한다.
    > PR을 날릴 때 체크 리스트를 작성, 스스로 코드 리뷰를 진행한다. 코드 리뷰에는 나중에 리팩토링할 코드, 관련 공부 자료 등을 표기한다.
> * 코드 리뷰를 하고 난 후, Github Action 수행 결과를 확인, main branch로 merge 한다. 이 때 rebase 방식 x

### GitLab Flow
> 정기 배포, 장기 프로젝트가 존재하는 애플리케이션, 버저닝 관리가 필요하지 않은 웹 애플리케이션에 적합하다.
>
> 브랜치 구성: feature, release, hofix, master
>
> **feature**
> * 보조 브랜치
> * 기능 단위 개발 브랜치
> * feature 에서 개발 완료 후 release 로 merge
> * issue list 로 브랜치 생성 및 관리
>
> **release**
> * 보조 브랜치
> * 배포 대상인 feature 가 모이는 통합 테스트 브랜치
> * 테스트 완료 후 master 로 merge
> * 소스 프리징을 해결하기 위한 브랜치
>
> **hotfix**
> * 보조 브랜치
> * 운영 중 긴급한 오류를 해결하기 위한 브랜치
>
> **master**
> * 유지 브랜치
> * 기본 브랜치
> * 언제든지 배포 가능한 형태를 유지

### 참조사이트
> [Git 브랜치 전략 (feat. Git Flow, Github Flow)](https://hudi.blog/git-branch-strategy/)  
> [[설계] Git Branch 전략이란? & Git Branch 전략 알아보기 (Git Flow, GitHub Flow)](https://ksh-coding.tistory.com/109)  
> [[적용기] Branch 전략 적용 후기(Git Flow, Github Flow)](https://sjevie.tistory.com/entry/%EC%A0%81%EC%9A%A9%EA%B8%B0-%EC%84%9C%EB%A1%9C-%EB%8B%A4%EB%A5%B8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-%EB%8B%A4%EB%A5%B8-Branch-%EC%A0%84%EB%9E%B5-%EC%A0%81%EC%9A%A9-%ED%9B%84%EA%B8%B0Git-Flow-Github-Flow)

---

## 인증
### GitHub 인증 제거
> **macOS**  
> 터미널을 오픈한 후 다음 명령어를 차례로 입력한다.
> ```shell
> git credential-osxkeychain erase return (엔터)
> host=github.com return (엔터)
> protocol=https (엔터)
> ```
> `키체인 접근` 앱 실행 > 키체인 접근 열기 버튼 클릭 > iCloud 탭에서 `github.com` 문구로 찾기 > github.com 목록들 제거     
> 
> **Windows**  
> 1.제어판 > 사용자 계정 > 자격 증명 관리자 로 이동  
> 2.일반 자격 증명 목록에서 github.com 을 찾아서 제거  
> 
> **제거 확인: 공통**  
> Github 을 사용하는 프로젝트로 들어가서 `git push` 명령어 입력해서 Github 로그인 창이 나타나면 성공.  
> 
> **Jetbrains IDE**  
> 1.Settings > Version Control -> GitHub 메뉴로 이동  
> 2.계정 제거

### 인증 Cache / Store 설정
> Cache 의 경우 외부 저장소의 인증 설정을 일정 시간 동안만 저장해두는 설정이다.  
> 명령어 예시: 30초간 아이디 및 패스워드 저장
> ```shell
> git config credential.helper "cache --timeout=30"  
> ```
> 
> Store 의 경우 외부 저장소의 인증 설정을 영구적으로 저장해두는 설정이다.  
> 명령어 예시
> ```shell
> git config credential.helper store
> ```
> 다만 store 옵션에는 한 가지 문제점이 있는데 사용자의 아이디와 패스워드가 홈 디렉터리의 `.git-credentials` 파일에 저장된다는 것이다.  
> 따라서 패스워드의 노출이 꺼려진다면 store 옵션은 사용하지 않는 것이 좋다.  
> 
> store 옵션을 더 이상 사용하지 않을 때에는 잊지말고 인증 정보가 담긴 .git-credentials 파일을 삭제한다.  
> ```shell
> rm ~/.git-credentials
> ```
