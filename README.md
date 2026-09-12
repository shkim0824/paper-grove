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
