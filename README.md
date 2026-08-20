# demo-gateway

프로젝트 라이브 데모 포트폴리오 사이트. 빌드 과정 없는 정적 사이트로 Cloudflare에 배포되며, push할 때마다 자동 재배포됩니다.

🌐 **Live**: https://demo-gateway.trealight112.workers.dev/

## 구조

```text
demo-gateway/
├── index.html            # 게이트웨이 메인 (프로젝트 카드 목록)
└── cafe-focusing/        # Cafe-Focusing 전용 데모 프론트엔드
    ├── index.html        #   드래그앤드롭·Ctrl+V 입력, 원본↔결과 비교 슬라이더
    └── sample.png        #   원클릭 체험용 샘플 이미지
```

데모 프론트엔드는 **화면은 Cloudflare, 연산은 Hugging Face Spaces API**로 분리된 2-티어 구조입니다. 각 데모 페이지는 게이트웨이와 동일한 디자인 토큰(색·폰트·다크모드)을 사용하고, 브라우저에서 `@gradio/client`로 해당 HF Space의 API를 직접 호출합니다.

## 데모 카드 추가/활성화

`index.html`의 `PROJECTS` 배열에서 해당 프로젝트의 필드를 채우면 됩니다:

- `demoUrl` — 데모 주소. 이 저장소 안의 커스텀 FE라면 상대경로(예: `"cafe-focusing/"`), 외부 서비스라면 절대 URL. 채우면 카드의 버튼이 활성화됩니다.
- `healthUrl` — 백엔드 헬스체크 주소(예: HF Space URL). 접속 시 핑을 보내 배지가 `온라인`/`슬립 중`으로 자동 갱신됩니다.
- `sleeps` — `true`면 슬립 상태에서 데모 클릭 시 "서버를 깨우는 중" 안내를 띄웁니다. 커스텀 FE는 페이지가 자체적으로 웨이크업을 처리하므로 `false`.

## 새 데모 프론트엔드 추가 절차

1. `<프로젝트명>/index.html` 생성 — 게이트웨이의 CSS 변수/레이아웃 관례를 따름
2. `@gradio/client`(jsdelivr ESM)로 해당 HF Space API 연동
3. `PROJECTS` 배열에 `demoUrl: "<프로젝트명>/"` 설정 후 push
