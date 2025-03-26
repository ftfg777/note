#git

**📌 1. Git 기본 설정**

| **명령어**                              | **설명**            |
| ------------------------------------ | ----------------- |
| git config --global user.name "이름"   | 전역 사용자 이름 설정      |
| git config --global user.email "이메일" | 전역 사용자 이메일 설정     |
| git config --local user.name "이름"    | 현재 저장소 사용자 이름 설정  |
| git config --local user.email "이메일"  | 현재 저장소 사용자 이메일 설정 |
| git config --list                    | Git 설정 정보 전체 출력   |

---
**📌 2. Git 저장소 초기화 및 클론**

|**명령어**|**설명**|
|---|---|
|git init|현재 디렉토리를 Git 저장소로 초기화|
|git clone <URL>|원격 저장소를 로컬로 복제|

---
**📌 3. Git 파일 상태 확인**

|**명령어**|**설명**|
|---|---|
|git status|현재 파일 상태 확인 (추적 여부, 변경 사항 등)|
|git diff|변경된 파일의 차이점 비교|

---
**📌 4. Git 파일 추가 및 제거**

| **명령어**               | **설명**                     |
| --------------------- | -------------------------- |
| git add <파일명>         | 특정 파일을 스테이징 영역에 추가         |
| git add .             | 변경된 모든 파일을 스테이징 영역에 추가     |
| git rm --cached <파일명> | Git의 추적 대상에서만 제거 (파일은 유지)  |
| git rm -r --cached .  | 모든 파일을 Git 추적에서 제거 (캐시 삭제) |
| git reset <파일명>       | 스테이징에서 파일 제거 (commit 전)    |
| git reset --hard      | 작업 디렉토리까지 변경사항을 되돌림        |

---
**📌 5. Git 커밋 (Commit)**

|**명령어**|**설명**|
|---|---|
|git commit -m "커밋 메시지"|스테이징된 파일을 커밋|
|git commit --amend -m "새 메시지"|마지막 커밋 메시지를 수정|

---
**📌 6. Git 브랜치 (Branch)**

|**명령어**|**설명**|
|---|---|
|git branch|브랜치 목록 확인|
|git branch <브랜치명>|새로운 브랜치 생성|
|git checkout <브랜치명>|해당 브랜치로 이동|
|git switch <브랜치명>|브랜치 변경 (checkout 대체)|
|git checkout -b <브랜치명>|브랜치 생성 후 이동|
|git switch -c <브랜치명>|브랜치 생성 후 이동 (checkout -b 대체)|
|git merge <브랜치명>|현재 브랜치에 다른 브랜치를 병합|
|git branch -d <브랜치명>|브랜치 삭제|
|git branch -D <브랜치명>|강제 브랜치 삭제|

---
**📌 7. Git 원격 저장소 (Remote) 관련**

|**명령어**|**설명**|
|---|---|
|git remote -v|연결된 원격 저장소 확인|
|git remote add origin <URL>|원격 저장소 추가|
|git remote remove origin|원격 저장소 제거|
|git remote set-url origin <새 URL>|원격 저장소 URL 변경|

---
**📌 8. Git 푸시 & 풀 (Push & Pull)**

|**명령어**|**설명**|
|---|---|
|git push origin <브랜치명>|원격 저장소에 현재 브랜치를 푸시|
|git push -u origin <브랜치명>|기본 푸시 브랜치를 설정 후 푸시|
|git push origin --delete <브랜치명>|원격 저장소의 브랜치 삭제|
|git pull origin <브랜치명>|원격 저장소에서 변경 사항 가져오기|
|git fetch|원격 저장소의 변경 사항을 가져오지만 병합하지 않음|

---
**📌 9. Git 로그 및 변경 사항 확인**

|**명령어**|**설명**|
|---|---|
|git log|커밋 로그 확인|
|git log --oneline|한 줄로 간결한 커밋 로그 확인|
|git log --graph --oneline --all|브랜치 그래프 형태로 로그 확인|
|git show <커밋ID>|특정 커밋의 변경 사항 확인|

---
**📌 10. Git 되돌리기 (Reset, Revert, Checkout)**

|**명령어**|**설명**|
|---|---|
|git reset --soft <커밋ID>|해당 커밋으로 이동하고, 변경 사항은 유지|
|git reset --mixed <커밋ID>|해당 커밋으로 이동하고, 변경 사항은 스테이징에서만 제거|
|git reset --hard <커밋ID>|해당 커밋으로 이동하고, 모든 변경 사항 삭제|
|git revert <커밋ID>|특정 커밋을 취소하는 새로운 커밋 생성|
|git checkout <파일명>|특정 파일을 마지막 커밋 상태로 복원|

---
**📌 11. Git 태그 (Tag)**

| **명령어**                        | **설명**            |
| ------------------------------ | ----------------- |
| git tag                        | 태그 목록 확인          |
| git tag <태그명>                  | 태그 생성             |
| git tag -a <태그명> -m "태그 메시지"   | 주석이 포함된 태그 생성     |
| git push origin <태그명>          | 태그를 원격 저장소에 푸시    |
| git push origin --tags         | 모든 태그를 원격 저장소에 푸시 |
| git tag -d <태그명>               | 로컬 태그 삭제          |
| git push origin --delete <태그명> | 원격 저장소의 태그 삭제     |

---
**📌 12. Git 서브모듈 (Submodule)**

|**명령어**|**설명**|
|---|---|
|git submodule add <URL>|현재 저장소에 서브모듈 추가|
|git submodule update --init --recursive|서브모듈 업데이트 및 초기화|
|git submodule foreach git pull origin main|모든 서브모듈 업데이트|
