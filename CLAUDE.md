# 시간조각 (time_piece)

하루를 시간 단위로 칠해서 기록하는 개인용 웹앱. 목표 / 실제 / 비교 / 달력 4개 탭.
사용자(혜림)는 개발·배포가 완전 초보이므로 설명은 한국어로, 하나씩 단계별로 쉽게 안내한다.

## 구조
- `index.html`: 앱 전체(HTML + CSS + 순수 JS 한 파일, 빌드 과정 없음). 이 파일이 원본이다.
- `supabase.js`: supabase-js UMD 번들(로컬 사본, CDN 사용 안 함).
- `privacy.html`: 개인정보처리방침. 받는 정보나 저장 방식이 바뀌면 같이 고친다.
- `manifest.webmanifest`, `*.png`: 홈 화면 앱 설정과 아이콘.

## 데이터
- 기본 저장은 브라우저 localStorage(`timelog:` 접두사). 로그인하면 Supabase에도 저장.
- Supabase 프로젝트: `https://vkniwingfvwdfidavzyy.supabase.co` (공개 키는 index.html에 있음).
- 표: `days(user_id, day, goal, actual, ra, updated_at)`, `settings(user_id, data, updated_at)`. 행 단위 보안(RLS)으로 본인 행만 접근.
- 코드의 `makeDb()`가 Supabase를 `db.collection().doc().set/get/onSnapshot` 형태로 감싼다. 오프라인에서 못 올린 변경은 `timelog:dirty:*`로 표시했다가 재전송한다.
- 비밀 키(service_role 등)는 절대 코드나 저장소에 넣지 않는다.

## 배포
- GitHub Pages: `main` 브랜치에 push하면 1~2분 뒤 https://rnldusgpfla-gif.github.io/time_piece/ 에 반영된다.
- 로그인(구글 OAuth)은 Supabase에 이 주소가 Redirect URL로 등록되어 있어야 동작한다.

## 작업 규칙
- 수정 후 JS 문법 검사(`node --check`)와 Playwright 화면 확인을 하고 push한다.
- 한 번에 하나씩, 무엇이 바뀌었는지 한국어로 짧게 알려 준다.
- push 전에 사용자가 원하면 변경 내용을 먼저 보여 준다.
