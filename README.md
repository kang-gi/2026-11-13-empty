# 2026-11-13-empty

Git Bash에서 HTML 파일을 만들고 Git으로 버전을 관리한 뒤 GitHub 원격 저장소에 연결해 데이터 분석가 소개 페이지를 게시하기 위한 실습 저장소입니다.

## 1. Git Bash 설치 (Windows)

이 저장소의 커밋 기록에는 설치 과정이 남아 있지 않습니다. 아래는 Windows에서 Git Bash를 준비할 때 사용하는 일반적인 설치 절차입니다.

1. [Git for Windows 공식 다운로드](https://git-scm.com/downloads/win) 페이지에서 설치 파일을 받습니다.
2. 내려받은 설치 파일을 실행하고 안내에 따라 설치합니다. 별도 설정이 없다면 기본 옵션을 유지해도 됩니다.
3. 시작 메뉴에서 **Git Bash**를 검색해 실행합니다.
4. 설치 여부를 확인합니다.

```bash
git --version
bash --version
```

## 2. 작업 폴더와 기본 명령어

Git Bash에서 프로젝트 폴더로 이동합니다. 아래 경로는 예시이며, 실제 폴더 위치에 맞게 바꿉니다.

```bash
cd /c/ex
pwd
ls -la
```

- `cd`: 폴더 이동
- `pwd`: 현재 작업 경로 확인
- `ls -la`: 일반 파일과 숨김 파일을 자세히 표시
- `cd ..`: 상위 폴더로 이동
- `.git`: Git의 커밋·브랜치·설정 등 버전 관리 정보가 저장되는 폴더입니다. 보통 직접 수정하지 않습니다.
- `cd .git`: 해당 메타데이터 폴더 안으로 이동하는 명령이며, 일반적인 작업을 위해 들어갈 필요는 없습니다.

## 3. HTML 파일 만들고 확인하기

최초 작업에서 사용한 파일 생성·작성 방식입니다.

```bash
touch index.html
echo "<h1>안녕하세요</h1>" > index.html
```

- `touch index.html`: 빈 HTML 파일을 만듭니다.
- `>`: 명령 결과를 파일에 씁니다. 기존 파일 내용이 있으면 덮어씁니다.
- 편집기로 직접 작성하려면 `nano index.html`을 사용할 수 있습니다.
- 브라우저에서 확인하려면 Windows Git Bash에서 `start index.html`을 실행합니다.

HTML은 웹페이지의 구조를 작성하는 언어입니다. 이번 페이지에는 문서 언어, 문자 인코딩, 모바일 화면 설정(viewport), 제목, 본문, CSS 스타일을 사용했습니다.

## 4. Git 저장소 초기화 및 사용자 설정

프로젝트 폴더에서 Git을 초기화합니다.

```bash
git init
git config --global user.name "GitHub 사용자명"
git config --global user.email "GitHub 계정 이메일"
```

이미 설정한 사용자 정보가 있다면 다시 설정할 필요는 없습니다. 설정값은 다음 명령으로 확인할 수 있습니다.

```bash
git config --global --list
```

## 5. 변경 사항 기록하기 (commit)

Git은 파일의 변경 이력을 기록합니다. 아래 순서로 현재 파일을 커밋에 포함합니다.

```bash
git status
git add index.html
git commit -m "feat: 첫 웹페이지 추가"
```

- `git status`: 변경·추가·삭제된 파일 확인
- `git add index.html`: 해당 파일을 다음 커밋에 포함하도록 스테이징
- `git add .`: 현재 폴더 아래의 변경 사항을 스테이징
- `git commit -m "메시지"`: 스테이징한 변경 사항을 로컬 저장소의 이력으로 저장

파일을 수정한 뒤에도 `git status` → `git add` → `git commit` 순서로 반복합니다.

## 6. GitHub 원격 저장소 연결 및 업로드

GitHub 저장소 주소를 로컬 저장소의 원격 이름 `origin`으로 등록합니다.

```bash
git remote add origin https://github.com/kang-gi/2026-11-13-empty.git
git remote -v
git branch -M main
git push -u origin main
```

- `origin`: 원격 저장소 주소에 붙인 별칭입니다.
- `git remote -v`: fetch(가져오기)와 push(올리기)에 사용하는 원격 주소를 확인합니다.
- `git branch -M main`: 현재 브랜치 이름을 `main`으로 변경합니다.
- `git push -u origin main`: 로컬 `main` 브랜치를 GitHub에 올리고 추적 관계를 설정합니다.

이미 `origin`이 등록되어 있다면 `git remote add`를 반복하지 말고 다음 명령으로 주소를 확인하거나 변경합니다.

```bash
git remote get-url origin
git remote set-url origin https://github.com/kang-gi/2026-11-13-empty.git
```

이후 변경 사항을 올릴 때는 다음 흐름을 사용합니다.

```bash
git status
git add .
git commit -m "페이지 내용 수정"
git push
```

## 7. 이번 저장소의 실제 변경 이력

GitHub의 현재 `main` 브랜치 커밋 기록을 확인해 정리했습니다.

| 순서 | 커밋 메시지 | 변경 내용 |
|---|---|---|
| 1 | `웹페이지 만들기` | `index.html`을 처음 추가했습니다. HTML 기본 문서 구조, viewport 설정, `Document` 제목과 임시 본문 문구가 들어갔습니다. |
| 2 | `Create responsive data analyst introduction page` | 기존 내용을 데이터 분석가 소개 페이지로 교체했습니다. 한국어 문서 설정과 반응형 스타일을 적용했습니다. |

두 번째 커밋에서 추가된 페이지 내용:

- **소개 문구:** “데이터로 문제를 명확하게 바라봅니다.”
- **배경:** 경제학 전공, 데이터를 활용해 실행 가능한 인사이트를 찾는다는 소개
- **관심 분야:** 공공데이터, 지표 설계, 시각화
- **기술 및 자격:** Python·Pandas(학습 중), SQL, Tableau, Excel, ADsP, 컴퓨터활용능력 1급
- **경험:** KOSIS 데이터 정리·시각화, 학생회 재무 거래 약 405건 및 증빙 점검, 복지 현장 이용자 상태·대응 기록

### 화면 구성과 코드 요소

- `<!doctype html>`: HTML5 문서임을 선언합니다.
- `<html lang="ko">`: 문서의 기본 언어를 한국어로 지정합니다.
- `<meta charset="utf-8">`: 한글을 포함한 문자 인코딩을 지정합니다.
- `<meta name="viewport"...>`: 모바일 화면 너비에 맞춰 표시되도록 합니다.
- CSS `max-width`와 자동 좌우 여백: 큰 화면에서 본문이 지나치게 넓어지지 않게 합니다.
- CSS `clamp()`: 화면 크기에 따라 제목 글자 크기가 유연하게 바뀌게 합니다.
- 녹색·민트 계열 색상과 태그 스타일: 소개 영역과 기술 목록을 구분합니다.

## 8. .env 파일이란?

`.env`는 프로그램 실행에 필요한 환경변수(예: API 키, 비밀번호가 아닌 설정값, 실행 환경)를 저장할 때 사용하는 파일 이름입니다. **이번 정적 HTML 소개 페이지에 .env가 사용되었다는 기록은 없으며, 현재 페이지를 표시하는 데 필요하지 않습니다.**

실제 비밀값을 `.env`에 넣었다면 GitHub에 올리지 않도록 `.gitignore`에 등록합니다.

```gitignore
.env
.env.*
!.env.example
```

실제 API 키나 비밀번호를 HTML, README, Git 커밋에 직접 기록하지 않습니다.

## 9. 참고 링크

- [Git for Windows 다운로드](https://git-scm.com/downloads/win)
- [Git 공식 문서](https://git-scm.com/doc)
- [이 저장소](https://github.com/kang-gi/2026-11-13-empty)
- [index.html 소스 보기](https://github.com/kang-gi/2026-11-13-empty/blob/main/index.html)
- [실제 페이지 변경 커밋](https://github.com/kang-gi/2026-11-13-empty/commit/b54d0960704cfb0c8fbf0c05963708f7fd5b62dc)

## 기록 범위 안내

커밋으로 확인되는 실제 저장소 이력은 위의 2개 커밋입니다. Bash 설치 절차와 일부 명령어 설명은 커밋에 남아 있지 않아 실습을 재현할 수 있도록 일반적인 Git for Windows 사용 절차로 정리했습니다. 따라서 설치 옵션 하나하나를 과거에 실제 선택한 기록으로 간주하지 않습니다.
