#git 

**1. 📌 .gitignore를 추가해도 기존 파일이 삭제 되지 않는 이유**

처음 .gitignore를 설정하기 전에 이미 GitHub에 올린 파일이 있다면,
.gitignore에 추가해도 자동으로 삭제 되지 않는다.

✅ **이유** → **Git은 한 번이라도 git add 된 파일을 계속 추적(Tracked)하기 때문!**

따라서 .gitignore를 적용하려면 **Git의 캐시에서 해당 파일을 제거하는 과정**이 필요하다.

`물론! 일반 소스 코드도 동일한 방식으로 적용 가능하다.` 


---
**2. ✏️ .gitignore 파일 수정하기**

예를 들어, 프로젝트에 
node_modules/ 패키지 폴더와 .env 파일이 .gitignore에 누락됐다고 가정하자. 
이를 .gitignore에 추가하는 방법은 다음과 같다.

**🧑‍💻 명령어로 추가**
```sh
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
```


**🧑‍💻 직접 수정**
```sh
nano .gitignore  # nano 에디터로 열기
vim .gitignore   # vim 에디터로 열기
```


**💾 저장 방법**
• **nano**: Ctrl + X → Y → Enter

• **vim**: i (편집 시작) → 내용 입력 → Esc → :wq → Enter


📌 **수정 후 확인**
```sh
cat .gitignore  # 파일 내용 확인
```

✳️ 물론  프로젝트 내부에서 .gitignore 파일을 수정해도 된다!
만약 .gitignore 파일이 없다면 터미널에서 직접 생성할 수도 있다.
```sh
touch .gitignore  # 현재 디렉토리에 생성
```


---
**3. 🔥 Git의 캐시에서 기존 파일 제거**

.gitignore에 추가했지만, 기존에 GitHub에 올라간 파일들은 여전히 추적되고 있다.
따라서 **Git의 캐시에서 해당 파일을 제거하는 과정**이 필요하다.

```sh
git rm -r --cached .
```

✅ **이 명령어의 역할**

• Git이 추적 중인 모든 파일을 **캐시에서 제거(언트랙)**

• **로컬 파일은 삭제되지 않고 그대로 유지됨**

• .gitignore에 추가된 파일은 이제 Git이 추적하지 않음

> [!tip] 
> git rm -r --cached . 명령어를 쓰면 **모든 파일을 한 번에 언트랙**할 수 있고, 
> 특정 파일만 제거하려면 개별적으로 git rm --cached <파일명>을 사용하면 된다.

예를 들어, config.json 파일을 Git에서 제거하고 싶다면?
```sh
git rm --cached config.json
```


---
**4. ✅ 변경 사항 커밋하고 GitHub에 반영**

파일을 제거한 후, 변경 사항을 저장하고 푸시하면 GitHub에서도 삭제된다.

```sh
git commit -m "Remove ignored files from tracking"
git push origin main  # (또는 현재 브랜치명)`
```

이제 .gitignore에 추가한 파일들이 **GitHub에서도 삭제된 것을 확인할 수 있다!** 🎉


---
**5. 🧐 Git의 원리: 왜 .gitignore만 추가하면 안 될까?**

Git의 파일 상태는 크게 3가지다.

1️⃣ **Untracked(미추적)** → Git이 관리하지 않는 파일

2️⃣ **Tracked(추적됨)** → Git이 관리하고 있는 파일

3️⃣ **Ignored(무시됨)** → .gitignore에 의해 추가되지 않는 파일


📌 **한 번이라도 git add를 한 파일은 “Tracked 상태”가 되어 Git이 계속 관리**한다.
즉, .gitignore만 추가한다고 해서 기존에 올라간 파일이 자동으로 삭제되지 않는 이유다.


🚀 **해결 방법** → git rm -r --cached . 명령어 사용!


이 명령어를 실행하면 파일 자체는 삭제되지 않고 **Git의 추적 대상에서만 제거**된다.
그 결과, 수정된 .gitignore를 새롭게 적용할 수 있게 된다!

