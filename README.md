# 📌 Learning_Github_Space

> 개인용 깃헙 공부 레포지토리입니다.

---

## 🔄 Git 푸시 과정 (Git WorkFlow)

작업 폴더의 변경 사항이 GitHub 원격 저장소에 반영되는 단계별 흐름입니다.

* **작업 폴더** : 실제 작업하는 곳
  * `↓ add` : 최신 상태로 변환
* **스테이지** : 커밋이 될 초안
  * `↓ commit` : 초안 확정, 해시 ID를 부여하여 영구 기록으로 남김
* **로컬 저장소** : `.git` 폴더에 저장
  * `↓ push` : 내 `.git` 폴더에 저장된 내용을 Github으로 복사
* **GitHub** : 내 작업물을 공유할 수 있는 원격 저장소

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

* 웹에서 직접 수정한 줄(git pull 공부 용도)
* 웹에서 직접 수정한 줄(conflict 공부 용도)
* 로컬에서 다른 브랜치에 추가한 줄(브랜치 공부 용도)

---

## ✔️ Pull Request

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
예시: closes #10, fixes #12
  * fix, fixes, fixed, close, closes, closed, resolve, resolves, resolved (전부 같은 기능)