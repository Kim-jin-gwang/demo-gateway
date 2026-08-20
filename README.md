# demo-gateway

프로젝트 라이브 데모 포트폴리오 게이트웨이. 빌드 과정 없는 정적 사이트(단일 `index.html`)로, Cloudflare Pages에 배포합니다.

## 데모 카드 추가/활성화

`index.html`의 `PROJECTS` 배열에서 해당 프로젝트의 필드를 채우면 됩니다:

- `demoUrl` — 라이브 데모 주소. 채우면 "데모 준비 중" 버튼이 "라이브 데모"로 활성화됩니다.
- `healthUrl` — 헬스체크 엔드포인트. 채우면 접속 시 핑을 보내 배지가 `온라인`/`슬립 중`으로 자동 갱신됩니다.
- `sleeps` — 무료 서버 슬립 여부. `true`면 슬립 상태에서 데모 클릭 시 "서버를 깨우는 중" 안내를 띄웁니다.

## 배포

Cloudflare Pages에 GitHub 저장소를 연결하면 push마다 자동 배포됩니다.
빌드 설정: Framework preset **None**, Build command 없음, Output directory `/`.
