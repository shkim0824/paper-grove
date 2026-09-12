# SHKim의 Paper Grove — GitHub Pages 버전

**앱 접속:** https://shkim0824.github.io/paper-grove/

**처음 사용하는 분을 위한 가이드:** https://shkim0824.github.io/paper-grove/guide.html

## 시작하기

1. 두 노트북에서 앱 주소를 엽니다. 이제 index.html을 다운로드하거나 노트북끼리 보낼 필요가 없습니다.
2. 각 브라우저에서 최초 한 번 GitHub 토큰을 입력하고 **GitHub 연결**을 누릅니다. 계정과 데이터 저장소는 이미 지정되어 있습니다.
3. **이 브라우저에 토큰 기억하기**를 켜두면 다음부터 자동으로 연결합니다.
4. **GitHub 연결됨**을 확인하고 PDF를 추가합니다. 문장을 드래그하면 하이라이트와 메모를 남길 수 있습니다.

이전 HTML 파일이나 로컬 미리보기에서 인증했더라도, 새 웹사이트 주소에서는 토큰을 한 번 다시 입력해야 합니다. 브라우저는 주소별로 인증 정보를 따로 저장합니다.

## 기존 논문은 어떻게 되나요?

- 기존 앱에서 GitHub에 저장한 PDF·메타데이터·하이라이트·메모는 그대로 불러옵니다. 다시 업로드하지 않습니다.
- 로컬 모드에만 저장한 자료는 원래 HTML을 같은 경로·브라우저에서 열고, **GitHub 연결 → 저장소 설정 → 로컬 서재를 GitHub로 복사**를 실행한 뒤 새 사이트에서 확인하세요.
- 두 노트북 간 데이터는 창으로 돌아올 때와 화면에 열려 있는 동안 30초마다 확인합니다. 미저장 메모나 편집 창이 있으면 자동 반영을 잠시 미룹니다.
- 같은 논문을 두 기기에서 동시에 편집하면 마지막 저장이 우선합니다. **GitHub 저장됨**을 확인하고 다른 노트북으로 이동하세요.

## 앱 기능이 업데이트되면

앱 변경을 요청하면 코드 수정·검증 후 공개 앱 저장소에 새 버전을 배포할 수 있습니다. 배포 완료 후 **브라우저 새로고침**만 하면 두 노트북 모두 새 버전을 사용합니다. 기존 논문 데이터는 비공개 저장소에 유지됩니다. 데이터 형식 변경이 필요한 기능은 백업·호환성 확인·이전 작업도 함께 진행해야 합니다.

앱 안의 **↻ 새로고침**은 논문 목록 갱신용입니다. 새 앱 버전을 받으려면 브라우저를 새로고침하세요. 이전 화면이 계속 보이면 저장 완료 후 Windows는 **Ctrl + Shift + R**, Mac은 **Command + Shift + R**을 사용하세요.

## 저장소 구성

| 저장소 | 공개 여부 | 용도 |
| --- | --- | --- |
| [shkim0824/paper-grove](https://github.com/shkim0824/paper-grove) | 공개 | index.html, guide.html, README.md, .nojekyll. 앱과 가이드만 배포합니다. |
| [shkim0824/paper-grove-library](https://github.com/shkim0824/paper-grove-library) | 비공개 | PDF 원본, library.json, annotations. 논문 데이터 본체이므로 삭제하지 마세요. |

토큰은 공개 저장소나 HTML에 포함하지 않습니다. 브라우저의 설정창에 입력한 토큰으로 비공개 데이터 저장소에 직접 접근합니다.

## 직접 배포 설정을 확인하려면

설정은 이미 완료되어 있습니다. 확인만 필요한 경우:

1. 공개 앱 저장소 → **Settings → Pages**로 이동합니다.
2. **Build and deployment → Source: Deploy from a branch**를 확인합니다.
3. **Branch: main**, 폴더 **/(root)**를 확인합니다.
4. **Actions**에서 Pages 배포 완료 여부를 확인합니다.

직접 앱을 수정할 때는 검증한 index.html을 공개 앱 저장소의 main 브랜치 루트에 커밋합니다. 로컬 파일만 수정하면 사이트에는 반영되지 않습니다. PDF, library.json, annotations 또는 토큰을 공개 앱 저장소에 올리지 마세요.

세부 사용법, 토큰 갱신, 오류 해결은 [웹 사용 가이드](https://shkim0824.github.io/paper-grove/guide.html)에 정리했습니다.

공식 참고: [GitHub Pages 배포 설정](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site), [GitHub Contents API](https://docs.github.com/en/rest/repos/contents), [토큰 관리](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).


## 2026.09.12 — arXiv 가져오기와 화면 개편

- 흰색·차콜 중심의 간결한 UI로 변경했습니다.
- **＋ arXiv 링크**에서 abs/pdf 링크, ID, 버전을 지원합니다. 제목·전체 저자·PDF·arXiv BibTeX가 자동 저장됩니다.
- 데이터 저장소의 `.github/workflows/import-arxiv.yml`와 `scripts/import_arxiv.py`가 처리합니다. 현재 데이터 저장소에는 설치되어 있습니다.
- 새 fine-grained PAT에는 데이터 저장소의 **Contents: Read and write + Actions: Read and write** 권한을 지정하세요.
- Actions는 계정의 사용 한도를 사용합니다. 실패/대기 상태는 앱의 실행 내역에서 확인하세요.
- `imports/<request_id>.json`은 진행 보고서이며 `imports/<request_id>-paper.json`은 버전을 고정한 복구 정보입니다. 중간에 실패하면 앱에서 같은 요청으로 다시 시도할 수 있습니다.
- 자동 인용은 arXiv 프리프린트 기준입니다. 정식 출판 정보는 논문별 Scholar 링크와 공식 출판 기록으로 대조하세요.
- [PAPER_GROVE_MEMORY.md](PAPER_GROVE_MEMORY.md): 새 GPT 세션에 첨부할 지침. 검색과 인증된 쓰기 도구가 있어야 실제 자동 등록까지 가능합니다.
- [INTEGRATION_REVIEW.md](INTEGRATION_REVIEW.md): Scholar 자동화 및 ChatGPT 연동 검토. 현재 유료 AI 연결은 설치하지 않았습니다.
- 앱 업데이트는 브라우저 새로고침으로 받습니다. 저장소의 PDF와 하이라이트 형식은 그대로 호환됩니다.

배포 파일: `index.html`, `guide.html`, `README.md`, `PAPER_GROVE_MEMORY.md`, `INTEGRATION_REVIEW.md`, `.nojekyll`.
공개 저장소에 토큰이나 데이터 저장소 파일을 올리지 마세요.


## 2026.09.12 — 폴더 분류와 인용 확인

빠른 사용법: [guide.html](guide.html).

- 기존 `tags` 배열을 폴더 경로로 사용합니다. 별도의 folders 데이터베이스나 PDF 이동이 없습니다. 예: `["Agent/Orchestration", "Reading/Favorites"]`.
- 상위 경로를 자동 생성해 표시하며, 상위 폴더 필터는 모든 하위 문헌을 포함합니다. 편집에서 기존 분류를 검색·다중 선택할 수 있습니다. 대소문자 차이는 같은 분류로 처리합니다.
- 기존 arXiv 분야 태그는 최상위 분류로 유지합니다. 비어 있는 폴더를 따로 저장하지는 않습니다.
- Scholar → 인용 → BibTeX 복사 → 편집에서 붙여넣기 → 저장. 붙여넣기는 제목·저자·출판처·연도 입력칸을 자동 갱신하지 않습니다.
- 직접 확인 체크를 저장하면 `citationStatus: "user_verified"`, `citationSource: "사용자 직접 확인"`, `citationCheckedAt`을 기록합니다. 자동 검증 상태와 구분합니다. 인용 필드를 바꾸면 UI 확인 체크가 풀립니다.
- 기존 자동/외부 검증 상태 `verified`는 분류만 수정할 때 유지됩니다. 미확인 arXiv는 `preprint`로 남습니다.

## 2026.09.12 — 연속 하이라이트와 오른쪽 메모

- 논문 상단에서 색을 한 번 선택하면 이후 드래그에도 같은 색을 적용합니다. 이 브라우저에서 선택한 색은 새로고침 뒤에도 기억합니다.
- `선택만` 또는 Esc로 색칠을 끄고 텍스트만 선택할 수 있습니다. 색을 누르면 다시 켜집니다.
- `되돌리기`는 지금 열어 둔 논문에서 새로 만든 표시를 최신순으로 취소합니다. 이전에 저장한 표시는 오른쪽에서 선택해 `하이라이트 삭제`로 지웁니다.
- 드래그 후 메모 입력창이 자동으로 뜨지 않습니다. 오른쪽 문장 목록이나 PDF의 표시를 클릭하면 오른쪽에서 메모를 작성하고 개별 색을 바꾸거나 삭제할 수 있습니다.
- 메모는 선택 사항이며 약 1.2초 뒤 자동 저장합니다. 원본 PDF와 하이라이트 데이터 형식은 그대로 유지합니다.
