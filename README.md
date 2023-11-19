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
