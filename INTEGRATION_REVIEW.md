# 인용 자동화와 ChatGPT 연동 검토

검토일: 2026-09-12

**arXiv 링크 → PDF·제목·저자·arXiv BibTeX 자동 등록은 구현했습니다.** 정식 학회·저널 인용 정보의 완전 자동 확정은 별도의 검증이 필요합니다. 이번에는 유료 AI 서비스나 새로운 인증 서버를 연결하지 않고, Scholar 검색 링크와 재사용 가능한 GPT 작업 지침을 제공합니다.

## 현재 구현

앱의 `＋ arXiv 링크`에 abs/pdf URL 또는 ID를 입력하면 비공개 데이터 저장소의 GitHub Actions가 실행됩니다. 공식 arXiv API의 메타데이터와 PDF를 받아 library.json에 병합합니다. 브라우저에서 arXiv PDF를 직접 가져오는 CORS 문제를 피하기 위한 구조입니다. 별도의 서버나 외부 프록시 계정은 필요 없습니다.

- 제목·전체 저자·연도·분야 태그·PDF·arXiv BibTeX를 저장합니다.
- 제목 없는 요약을 AI로 지어내지 않습니다. 초록은 `abstract`에 보관하며 한줄 요약은 사용자 입력용으로 비워 둡니다.
- 자동 인용은 프리프린트인 `@misc`로 표시합니다. API에 DOI/journal reference가 있어도 정식 출판 검증을 마쳤다고 표시하지 않습니다.
- 버전 없는 동일 ID의 재입력은 중복으로 처리합니다. 기존 원본과 메모를 바꾸지 않습니다.
- SHA 충돌 시 최신 목록을 읽어 병합합니다. 실패 상태와 재시도 버튼이 있습니다. 업로드 후 목록 저장이 실패한 경우 같은 요청으로 재시도해 복구합니다.
- 요청을 보낸 뒤 창을 닫아도 GitHub에서 처리가 계속됩니다. 앱을 다시 열면 이 브라우저의 대기 요청을 복구하며, 다른 기기도 완료된 문헌을 동기화합니다.
- 95 MiB 이하 PDF, 한 번에 링크 하나를 지원합니다. arXiv 장애·접근 제한이나 GitHub Actions 사용 한도에 따라 실패할 수 있습니다.

arXiv는 서지 메타데이터 API를 제공하며 사용량을 절제하도록 안내합니다. 구현은 요청을 순차 처리하고 메타데이터 조회와 PDF 다운로드 사이 간격을 둡니다. [arXiv API 안내](https://info.arxiv.org/help/api/user-manual.html), [이용 조건](https://info.arxiv.org/help/api/tou.html).

## Google Scholar 자동화

| 방법 | 가능 범위 | 판단 |
|---|---|---|
| 논문별 Scholar 검색 링크 | 정확한 제목을 검색창에 전달 | 구현 완료 |
| Scholar 결과/BibTeX를 정기 크롤링 | 차단, CAPTCHA, 결과 혼동 가능 | 안정적인 자동 등록 경로로 사용하지 않음 |
| arXiv 공식 메타데이터 | 프리프린트의 제목·저자·ID·기본 인용 | 구현 완료 |
| DOI/출판사/학회/Crossref 대조 | 정식 출판 기록 확인 | AI나 사람이 출처를 대조하는 후속 단계 |

Scholar는 Cite를 통한 BibTeX 내보내기를 제공하지만 자동화 도구에는 robots.txt 준수를 요구하며 일괄 접근을 제공하지 않는다고 안내합니다. 따라서 **Scholar 검색 결과를 언제나 자동 확보하고 정확한 인용으로 확정하는 기능을 보장하기 어렵습니다.** [Google Scholar 공식 도움말](https://scholar.google.com/intl/en/scholar/help.html).

Scholar는 발견 도구로 사용하고, 최종 인용은 공식 출판 기록으로 검증하는 편이 적합합니다. DOI가 알려져 있으면 해당 기록을 조회하고 제목·저자를 대조할 수 있습니다. DOI를 추측해서 붙이거나 제목이 비슷한 첫 검색 결과를 저장해서는 안 됩니다. [Crossref REST API](https://www.crossref.org/documentation/retrieve-metadata/rest-api/).

## 내 사이트 안에 ChatGPT를 연결할 수 있나?

**가능하지만, 정적 HTML에 ChatGPT 로그인만 붙여 자동화되는 구조는 아닙니다.** 두 가지 별도 구성을 선택할 수 있습니다.

### A. Custom GPT에서 내 서재에 추가하기

Custom GPT에 검색 지침과 GitHub API를 호출하는 Action을 구성하면, 대화에서 링크를 주고 가져오기 실행·상태 확인·검증된 메타데이터 저장을 할 수 있습니다. API Key 또는 OAuth 인증과 허용 엔드포인트 스키마가 필요합니다. 이 MD 파일만 업로드해서는 Action이 만들어지지 않습니다. 실제 사용 가능한 검색 도구와 Action의 조합도 해당 GPT에서 확인해야 합니다. [GPT Actions](https://developers.openai.com/api/docs/actions/introduction), [Action 인증](https://developers.openai.com/api/docs/actions/authentication).

개인용 구성에는 데이터 저장소 하나로 제한한 자격 증명을 사용하고 GPT의 인증 설정에 보관합니다. 공개 GPT나 공개 HTML에 토큰을 넣어서는 안 됩니다. 정식 연동 시에는 검색 후 확인된 필드만 수정하는 작은 API를 두면 GitHub 전체 파일 쓰기보다 권한과 검증 범위를 좁히기 쉽습니다. 현재는 이 Action을 설치하거나 연결하지 않았습니다.

### B. Paper Grove 자체에 AI 검색 버튼 추가하기

로그인으로 보호된 백엔드(또는 비공개 GitHub Actions의 별도 AI 작업)가 OpenAI Responses API의 웹 검색 도구를 호출하고, 확인한 인용 필드와 출처를 앱에 반환하는 구성이 가능합니다. API 키는 서버/비공개 실행 환경의 secret에 보관해야 합니다. 브라우저 JavaScript에 OpenAI 키를 넣으면 안 됩니다. [웹 검색 API](https://developers.openai.com/api/docs/guides/tools-web-search), [API 인증과 키 관리](https://developers.openai.com/api/reference/overview).

별도의 OpenAI API 인증 및 사용량 관리가 필요합니다. 이 검토 단계에서는 API 키 발급, 과금 설정, AI 호출을 수행하지 않았습니다. 웹 검색 도구가 있다는 사실도 Scholar의 차단을 해제하거나 검색 결과의 정확성을 보장하지는 않습니다.

### 지금 사용할 방법

`PAPER_GROVE_MEMORY.md`를 새 GPT 세션에 첨부하고 arXiv 링크와 함께 요청하세요. 검색 도구만 있으면 출처 대조와 BibTeX 작성까지, **인증된 GitHub 쓰기 도구까지 있으면 실제 서재 등록까지** 가능합니다. 도구가 없는 일반 대화에서는 결과를 앱의 편집 창에 붙여 넣으면 됩니다.

## 토큰과 운영

기존 PDF·메모 기능의 `Contents: Read and write` 외에, 새 arXiv 실행에는 데이터 저장소의 **`Actions: Read and write`** 권한이 필요합니다. 현재 연결로 실제 가져오기 실행을 검증했습니다. 새 fine-grained PAT를 만들 때 이 두 repository permission을 선택하세요. 앱에서 워크플로 파일을 수정하지 않으므로 일상 사용용 토큰에 Workflows 쓰기 권한은 필요 없습니다. [워크플로 실행 API와 권한](https://docs.github.com/en/rest/actions/workflows#create-a-workflow-dispatch-event).

GitHub Actions는 계정의 사용 한도와 결제 정책을 따릅니다. 자동 가져오기 때문에 사용 시간이 발생합니다. 별도 유료 요금제나 지출 한도 변경은 하지 않았습니다. 개인 저장소의 Actions 탭에서 실패·대기 상태를 볼 수 있습니다. 데이터 저장소는 비공개로 유지하세요.
