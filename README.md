# claude-insights

Claude Code의 `/insights` 사용 분석 리포트를 한국어로 번역해 보관하는 아카이브입니다.

`/insights`는 로컬 세션 트랜스크립트(`~/.claude/projects/*/*.jsonl`)를 분석해 작업 패턴,
마찰 지점, 개선 제안을 담은 HTML 리포트를 생성합니다. 이 저장소의 파일들은 커스텀 스킬
`/insights-korean`으로 만든 결과물로, 원본 리포트의 차트 데이터와 수치는 그대로 유지하고
본문·차트 라벨·복사용 프롬프트를 한국어로 번역한 것입니다.

## 리포트 목록

날짜를 클릭하면 GitHub Pages에서 렌더링된 리포트가 열립니다.

| 데이터 기간 | 소스 |
|---|---|
| [2026-08-05 ~ 2026-09-08](https://choiseungmyung.github.io/claude-insights/html/20260805-20260908.html) | [html](html/20260805-20260908.html) |
| [2026-07-06 ~ 2026-08-03](https://choiseungmyung.github.io/claude-insights/html/20260706-20260803.html) | [html](html/20260706-20260803.html) |
| [2026-06-02 ~ 2026-07-03](https://choiseungmyung.github.io/claude-insights/html/20260602-20260703.html) | [html](html/20260602-20260703.html) |
| [2026-05-18 ~ 2026-06-18](https://choiseungmyung.github.io/claude-insights/html/20260518-20260618.html) | [html](html/20260518-20260618.html) |
| [2026-04-23 ~ 2026-05-26](https://choiseungmyung.github.io/claude-insights/html/20260423-20260526.html) | [html](html/20260423-20260526.html) |
| [2026-03-16 ~ 2026-04-09](https://choiseungmyung.github.io/claude-insights/html/20260316-20260409.html) | [html](html/20260316-20260409.html) |

리포트 파일은 `html/` 폴더에 `YYYYMMDD-YYYYMMDD.html` 형식(데이터 기간의 시작일-종료일)으로
보관합니다. 렌더링된 페이지에서 타임존 선택, 프롬프트 복사 버튼, 목차 앵커가 동작합니다.

## 생성 방법

`/insights`는 기간 지정 옵션이 없어 전체 트랜스크립트를 분석합니다. `/insights-korean`
스킬은 직전 리포트와 기간이 겹치지 않도록 다음 절차로 동작합니다.

1. 가장 최근 리포트 파일명에서 직전 데이터 종료일을 읽어 경계일을 정한다
2. 경계일 이전 세션 트랜스크립트를 임시 격리한다 (manifest에 기록, 종료 후 반드시 복원)
3. `claude -p "/insights"`를 헤드리스로 실행한다
4. 생성된 리포트를 번역한다 — HTML 구조·CSS·JS·차트 수치는 원본 유지, 텍스트만 한국어화
5. 요소 개수(`bar-fill`, `chart-title`, 카드류)를 원본과 대조해 검증한다
