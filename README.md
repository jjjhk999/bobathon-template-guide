# Bobathon 템플릿 가이드

Bobathon 참가자가 BoB과 MCP를 빠르게 익힐 수 있도록 하는 사이트입니다.

## 프로젝트 구조

```text
tools-template/
├── index.html                  # 홈 화면과 템플릿 카드
├── guides/                     # 각 템플릿의 상세 페이지
├── images/                     # 안내 화면과 예시 이미지
├── assets/
│   ├── style.css               # 사이트 공통 스타일
│   └── site.js                 # 복사 버튼 등 공통 동작
└── script/preview              # 로컬 미리보기 실행 파일
```

## 로컬에서 확인하기

프로젝트 최상위 폴더에서 다음 명령을 실행합니다.

```bash
./script/preview
```

브라우저에서 <http://127.0.0.1:4173/>을 엽니다. 4173 포트를 이미 사용 중이라면 아래 예시와 같이 다른 포트로 실행할 수 있습니다.

```bash
PORT=4181 ./script/preview
```

HTML이나 CSS를 수정한 뒤에는 브라우저를 새로고침하면 결과를 확인할 수 있습니다.

## 기존 템플릿 수정하기

1. 수정할 상세 페이지를 `guides/` 폴더에서 찾습니다.
   - 기본 MCP: `guides/basic-mcp.html`
   - Notion MCP: `guides/notion-mcp.html`
   - Context7 MCP: `guides/context7-mcp.html`
   - Exa MCP: `guides/exa-mcp.html`
2. 해당 HTML 파일의 제목, 설명, 설정 코드, 요청 예시와 이미지를 수정합니다.
3. 홈 화면의 카드 문구도 바꿔야 한다면 `index.html`에서 해당 카드를 찾아 함께 수정합니다.
4. 공통 디자인을 바꿔야 할 때만 `assets/style.css`를 수정합니다. 이 파일의 변경은 여러 상세 페이지에 함께 영향을 줄 수 있습니다.
5. 로컬 미리보기에서 홈과 상세 페이지를 모두 확인합니다.

이미지 파일을 교체할 때는 새 이미지를 `images/`에 넣고 상세 페이지의 경로를 다음처럼 작성합니다.

```html
<img src="../images/05_a.png" alt="화면에 표시되는 내용을 설명하는 문구">
```

이미지에 API 키, 비밀번호, 회사 내부 정보나 개인 정보가 보이지 않는지 반드시 확인합니다.

## 새 템플릿 추가하기

### 1. 상세 페이지 만들기

구성이 비슷한 기존 파일을 복사해 새 파일을 만듭니다.

```bash
cp guides/notion-mcp.html guides/new-tool-mcp.html
```

파일명은 영문 소문자와 하이픈을 사용합니다. 예: `slack-mcp.html`, `github-mcp.html`

복사한 파일에서 다음 내용을 새 템플릿에 맞게 수정합니다.

- 브라우저 탭에 표시되는 `<title>`
- 템플릿 번호와 페이지 제목
- 어떤 상황에 도움이 되는지 설명하는 문장
- MCP 설정 코드와 연결 절차
- BoB에 입력할 요청 예시
- 성공 여부를 확인하는 방법과 주의사항
- 안내 이미지와 대체 텍스트(`alt`)

상세 페이지의 공통 파일 경로는 아래 형식을 유지합니다.

```html
<link rel="stylesheet" href="../assets/style.css?v=5">
<a href="../index.html">홈</a>
<script src="../assets/site.js"></script>
```

### 2. 홈 화면에 카드 추가하기

`index.html`에서 알맞은 섹션의 `.card-grid` 안에 새 카드를 추가합니다.

```html
<a class="card" href="guides/new-tool-mcp.html">
  <span class="card-number">05</span>
  <div class="card-copy">
    <h3>새 도구 MCP</h3>
    <p>이 템플릿이 필요한 상황을 한 문장으로 설명합니다.</p>
  </div>
  <span class="card-action">열기 →</span>
</a>
```

기존 공란 카드가 있다면 새 카드를 추가하기보다 해당 카드의 번호, 제목, 설명과 링크를 교체합니다. 카드 번호가 중복되지 않도록 확인합니다.

### 3. 이미지 추가하기

안내 이미지가 필요하면 `images/` 폴더에 추가합니다. 템플릿 번호에 맞춰 `05_a.png`, `05_b.png`처럼 정리하면 찾기 쉽습니다.

상세 페이지에서는 다음과 같이 연결합니다.

```html
<img src="../images/05_a.png" alt="MCP 설정 화면">
```

### 4. 로컬에서 최종 확인하기

다음 항목을 확인합니다.

- 홈 카드가 올바른 상세 페이지로 이동하는가
- 상세 페이지의 `홈` 링크가 정상 동작하는가
- CSS, JavaScript와 이미지가 빠짐없이 표시되는가
- 설정 코드와 복사 버튼이 정상 동작하는가
- 참가자가 성공 여부를 확인할 방법이 적혀 있는가
- 비밀번호, API 키와 개인 정보가 포함되지 않았는가
- 화면 폭을 줄였을 때 내용이 잘리거나 겹치지 않는가

## Git에 반영하기

`main`에서 직접 작업하지 않고, 수정이나 추가 작업마다 별도의 브랜치를 만듭니다. 별도의 장기 `dev` 브랜치는 사용하지 않습니다.

```bash
git switch main
git pull
git switch -c feat/add-new-tool-guide
```

작업과 로컬 확인이 끝나면 변경한 파일만 선택해서 커밋하고 브랜치를 올립니다.

```bash
git status
git add index.html guides/new-tool-mcp.html images/05_a.png
git commit -m "feat: add new tool MCP guide"
git push -u origin feat/add-new-tool-guide
```

GitHub에서 해당 브랜치의 Pull Request를 만들고, 내용을 확인한 뒤 `main`에 병합합니다.

- 새 기능이나 템플릿 추가: `feat/작업명`
- 오류 수정: `fix/작업명`
- 문서 수정: `docs/작업명`

`main` 브랜치에 병합되면 GitHub Pages 배포가 자동으로 실행됩니다. `guides/`와 `images/` 안에 파일을 추가하는 일반적인 작업에서는 Pages 워크플로를 수정할 필요가 없습니다.
