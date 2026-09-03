# 📌 Learning_Github_Space

> 개인용 깃헙 공부 레포지토리입니다.

---

## ✔️ Git 푸시 과정 (Git WorkFlow)

작업 폴더의 변경 사항이 GitHub 원격 저장소에 반영되는 단계별 흐름입니다.

* **작업 폴더** : 실제 작업하는 곳
  * `↓ add` : 최신 상태로 변환
* **스테이지** : 커밋이 될 초안
  * `↓ commit` : 초안 확정, 해시 ID를 부여하여 영구 기록으로 남김
* **로컬 저장소** : `.git` 폴더에 저장
  * `↓ push` : 내 `.git` 폴더에 저장된 내용을 Github으로 복사
* **GitHub** : 내 작업물을 공유할 수 있는 원격 저장소

---

## ⌨️ 실무 흐름

* 이슈 생성 (feature_request)
  * ↓ git switch -c feature/이슈번호-작업명
* 작업
  * ↓ commit → push
* PR 생성 (템플릿 자동, "Closing Keyword" 작성)
  * ↓리뷰 → 수정 → Approve
* Squash and merge
  * ↓이슈 자동 종료 + 브랜치 삭제
* git switch main && git pull && git branch -D 브랜치명

---

## 브랜치

브랜치는 **코드 작업 공간을 독립적으로 분할**하여 **병렬하게 개발을 진행**할 수 있게 만드는 기능

브랜치는 작업 목적에 따라 다음과 같이 나뉜다.

|브랜치명|목적|
|---|---|
|main|배포 가능한 상태의 안정적인 코드 뭉치|
|develop|다음 배포를 위해 개발중인 코드 뭉치|
|feature|기능 추가|
|fix|버그 수정|
|hotfix|운영중인 main에서 긴급한 수정이 필요할 때|
|docs|문서|
|refactor|구조 개선|
|chore|설정, 빌드 등 잡일|

---

## 🛡️ 브랜치 보호 규칙

main이나 develop 브랜치에 검증되지 않은 코드가 함부로 섞이거나, 실수로 삭제되는 것을 막기 위한 규칙

* 모든 변경 사항은 PR을 통해서만 병합되도록 강제
* 코드 리뷰 승인 필수
  * 최소 리뷰 승인 인원 지정
  * 리뷰 승인 후 코드 추가 수정 시 기존의 승인 무효화 후 재리뷰
* CI/CD 빌드 및 테스트 통과 필수 : 자동화된 테스트나 빌드가 성공해야만 병합 가능
* 강제 push 및 브랜치 삭제 금지 : 옵션 비활성화
* 최신 브랜치 상태 유지 : 병합하려는 PR의 브랜치가 main의 최신 내역을 포함하고 있는지 확인

세팅에서 브랜치 보호하기  
Settings → Branches → Add branch ruleset  
* Ruleset Name : 해당 규칙의 이름
* Enforcement status : Disabled → Active
* Bypass list : 규칙을 무시할 수 있는 예외 대상
* Target branches : 대상으로 지정할 브랜치
  * Include default branch : 디폴트 브랜치(main)를 지정
  * Include by pattern : 브랜치명을 직접 지정
* Branch rules : 브랜치 규칙
  * Require a pull request before merging : 직접 커밋 금지. 반드시 PR을 거쳐야 됨
    * Required approvals : 승인의 개수가 정해짐
    * Required convensation resolution : 리뷰 코멘트 전부 해결해야 merge 가능
  * Block force pushes : 히스토리 강제 덮어쓰기 차단
  * Restrict deletions : 브랜치 삭제 방지
* Create : 위에서 설정한 규칙 생성

---

## 🛠️ 주요 Git 명령어

* `git clone https://github.com/~/~.git`
  * 깃헙 레포지토리에 있는 내용을 로컬 폴더로 가져옴 (현재 위치에 폴더로 생성)
* `git remote`
  * 연결된 원격 주소의 목록을 보여 줌
  * `git remote -v` : verbose(자세히), 주소까지 같이 출력하라는 뜻
* `git status`
  * 현재 작업 폴더의 상태를 보여줌
* `git log`
  * 커밋 기록을 최신순으로 보여줌
  * `git log --oneline` : 커밋 이력을 하나의 라인으로 간단하게 보여 줌
  * `git log --graph` : 커밋 이력을 그래프로 표현해서 보여 줌
* `git diff`
  * 커밋된 내용과 현재 파일 상태를 비교해 뭐가 달라졌는 지 보여 줌
* `git add 파일명`
  * 이 파일의 최신 상태를 다음 커밋에 포함 시킴
  * `git add .` : 현재 폴더의 모든 내용을 포함
* `git push`
  * 원격에 최신 커밋 내용을 반영
  * `git push -u origin 브랜치명` : 로컬에서 생성한 브랜치를 원격에 병합
  * `git push origin --delete 브랜치명` : 원격에서 브랜치 삭제(웹으로 더 많이 하긴 함)
* `git fetch`
  * 원격의 최신 커밋 내용을 로컬로 가져와 조회
  * `git fetch -p` : 원격에서 사라진 브랜치 정보 정리
* `git merge`
  * 원격의 최신 커밋 내용을 로컬로 가져와 기존 내용과 병합
  * `git merge --abort` : pull 시작 전으로 롤백
  * Fast-Forward 방식: 브랜치 한 개만 바뀌어 병합이 간단한 형태
  * 3-way 방식: 브랜치 두 개 이상이 바뀌어 세 지점(공통 조상, 브랜치A, 브랜치B)을 비교하여 병합하는 형태
* `git pull`
  * git fetch + git merge
* `git switch 브랜치명`
  * 해당 브랜치로 이동
  * `git switch -c 브랜치명` : 해당 브랜치명으로 브랜치를 만들고, 그 브랜치로 이동
* `git branch`
  * 브랜치 조회 및 현재 브랜치 확인(로컬)
  * `git branch -d 브랜치명` : 해당 브랜치명의 브랜치를 삭제 (merge 안했으면 거부)
  * `git branch -D 브랜치명` : 강제 삭제
  * `git branch -a` : 원격 브랜치 및 로컬 브랜치 전부 확인

---

## 🔄️ 되돌리기

git에서는 작업의 시점을 구분하여 되돌리는 것을 구분한다.  
위치는 크게 작업 폴더(로컬), 스테이지, 로컬 저장소(.git), GitHub 으로 구분한다.

* `git restore` : 작업 폴더
  * 파일을 고쳤는데 없던 일로 하고 싶을 때, 마지막 커밋 상태로 덮어쓴다.
  * `git add`와 명령어가 비슷하다. (EX : git add . 나 git add README.md)
* `git restore --staged` : 스테이지
  * add를 취소하는 명령어로, 스테이지에서만 취소하고 파일 내용은 그대로 둔다.
* `git commit --amend` : 직전 커밋 수정
  * 커밋 후 오타나 파일을 빠뜨렸을 때
  * `git commit --amend -m "수정 메시지"
  * `git commit --amend --no-edit` : 메시지는 그대로 두고, 파일만 추가해서 다시 커밋한다.(전에 git add로 빠뜨린 파일을 추가한다.)
* `git reset` : 로컬 저장소
  * 커밋 되돌리기 (push 전), 옵션 3개로 강도가 갈린다.
  * `git reset --soft HEAD~1` : 커밋만 풀린다. HEAD~1은 직전 커밋을 의미한다.
  * `git reset --mixed HEAD~2` : add도 풀린다. 빨간색으로 남는다. HEAD~2는 2개 전 커밋을 의미한다.
  * `git reset --hard HEAD~3' : 작업 자체가 사라진다. 정말 필요할 때만 사용한다.
  * HEAD~ 뒤에 붙는 숫자는 고정이 아니라 유동적으로 바뀔 수 있다.
* `git revert` : GitHub
  * 기존 커밋을 지우지 않고, 그걸 취소하는 새 커밋을 추가한다.
  * before	: A ㅡ B ㅡ C
  * after	: A ㅡ B ㅡ C ㅡ C' (C를 취소)
* `git reflog`
  * 날린 줄 알았던 커밋을 찾는 곳 HEAD가 거쳐간 모든 위치가 기록되어 있다.
  * 기본 90일간 보관되어 복구 가능하다.

---

## ⛔.gitignore

깃헙에 올라가면 안되는 파일이 올라가는 것을 막는다

**문법**

|파일명|설명|
|---|---|
|# 주석|'이 파일이 왜 올라가면 안되는 지'에 대한 설명|
|secret.txt|특정 파일|
|*.log|확장자 전체|
|build/|폴더 전체 (슬래시로 폴더임을 명시)|
|/config.json|루트의 것만 (하위 폴더는 제외 안 함)|
|!important.log|예외 (앞의 규칙에서 제외)|
|temp?.txt|? 는 한 글자|

---

## 📃 Issues

해야할 일을 기록하는 곳(버그, 기능 요청, 작업 항목 전부)

- 이슈 템플릿에 따라 기록하면 된다.
- PR과 연결된다.

---

## 🙏 Pull Request

브랜치를 합치는 것을 요청하는 것  
단순히 합치는 게 목적이 아니라, **다른 사람이 코드를 보게하는 것이 목적**  
PR 하나 = 브랜치 하나 = 작업 하나

**PR 생성 순서**  
1. 상단에 노란 배너로 Compare & pull request라고 적혀있다.  
2. 들어가면 상단에 [base:브랜치A ← compare:브랜치B] 배너가 적혀있다.  
* base는 합쳐지는 목적지 브랜치, compare는 합칠 브랜치이다.  
* Able to merge. 라고 초록색으로 적혀있으면 충돌이 없고, Can’t automatically merge. 라고 빨간색으로 적혀있으면 충돌이 있는 것  
3. 내용 작성
* 작업 내용, 변경 이유, 확인 사항 등, **다른 인원이 코드를 봤을 때** 아는 부분 대신 **모르는 부분**을 집중적으로 써야한다.  
4. PR 생성

**PR 생성 이후 이루어지는 것들**  
* Files Changed 탭
  * 특정 줄을 리뷰할 수 있다.
* Merge 방식
  * `Create a merge commit` : 그동안 브랜치에 합쳐진 모든 커밋을 합친다.  
실제로 일어난 일이 그대로 보존되고, 언제 합쳤는 지 알 수 있지만, 그래프가 복잡해지고 짜잘한 수정도 남는다.
  * **`Squash and merge`** : 브랜치에 합쳐진 모든 커밋을 1개로 압축해 합친다. 실무에서 가장 많이 사용하는 형태  
main 히스토리가 깔끔해지고, PR과 커밋이 대응되어 나중에 롤백이 쉬워지지만, 중간 과정이 사라지고, 커밋 메시지를 다시 써야한다.
  * `Rebase and merge` : merge 커밋 없이 커밋들을 단순히 main 끝에 이어 붙인다.  
히스토리가 일직선이며 커밋도 보존되지만, 실제 시간 순서와 다르게 구성되고 사실과 다르게 기록되어 초보자에게는 권하지 않는 방식이다.
* 브랜치 삭제
  * 사용된 브랜치는 merge 이후 과감하게 삭제한다.
* 로컬 정리
  * 원격은 이미 브랜치가 지워졌으므로, 로컬에서도 브랜치를 삭제한다.

* 사이드바
  * Reviewers : 작업을 봐줄 상대를 지목한다.(자신은 불가) 지목 시 상대방에게 연락이 간다. 지정된 사람은 리뷰 제출 시 아래 세 가지 중 하나를 고른다.
    * Comment : 의견
    * Approve : 승인
    * Request changes : 수정 요구
  * Assigness : 작업을 만든 사람(본인), 관리용 표시
  * Labels :  작업의 분류 태그
    * bug : 버그 관련(버그 해결 전에는 Open 상태 + bug 라벨, 버그 해결 후에는 Closed 상태 + bug 라벨)
    * enhancement : 기능 개선
    * documentation : 문서
    * good first issue : 초보자용
    * help wanted : 팀원이나 외부의 도움이나 의견 요청
    * invalid : 필요 없는 작업 혹은 잘못 올렸을 때를 표시
    * question : 질문, 검토 요청, 논의
    * wontfix : 해결하지 않기로 의도적으로 결정한 작업
    * 커스텀 라벨 : 프로젝트 성격에 따라 팀에서 결정하여 만든 라벨
  * Projects : 작업 현황을 보여주는 보드
  * Milestone : 마감 기한이 있는 묶음, 관련된 PR/이슈를 한 덩어리로 묶고 진행률을 보여준다.
  * development : 이 PR이 어떤 이슈나 작업 항목을 해결하는지 연동하는 영역
* Closing Keyword : 이슈 번호를 함께 적으면 PR이 병합될 때 이슈를 자동으로 닫아주는 예약어  
EX : closes #10, fixes #12
  * fix, fixes, fixed, close, closes, closed, resolve, resolves, resolved (전부 같은 기능)

---

## Actions

저장소에 이벤트가 생기면 자동으로 발생되는 기능
push → 테스트 → PR Open → 빌드 확인 → main에 merge → 배포(CI/CD)
.github/workflows/ 폴더에 .yml 파일을 두면 깃헙이 자동으로 지정한 시점(.yml 파일에 사용자가 지정)에 깃헙 서버로 실행

구성 예시
|파일명|기능|
|---|---|
|ci.yml|PR마다 테스트, 린트|
|deploy.yml|main에 merge 시 배포|
|codeql.yml|보안 스캔(매주 1회)|
|stale.yml|오래된 이슈 자동 정리|

같은 파일인데 작업이 여러 개라면 job으로 쪼갠다.
---

## 📚 공부용 문구

* 웹에서 직접 수정한 줄(git pull 공부 용도)
* 웹에서 직접 수정한 줄(conflict 공부 용도)
* 로컬에서 다른 브랜치에 추가한 줄(브랜치 공부 용도)
