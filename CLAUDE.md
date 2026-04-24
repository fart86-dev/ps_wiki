# LLM Wiki Schema

당신의 세컨드 브레인. 이 문서는 위키의 구조, 컨벤션, 그리고 워크플로우를 정의합니다.

## 개요

이 위키는 세 개의 계층으로 구성됩니다:

1. **raw/** — 원본 소스 (수정 금지, LLM이 읽기만 함)
2. **wiki/** — 생성된 마크다운 파일 (LLM이 전적으로 관리)
3. **CLAUDE.md** (이 파일) — 스키마와 워크플로우 정의

## 폴더 구조

```
ps_wiki/
├── CLAUDE.md                 # 이 파일 (스키마)
├── index.md                  # 위키 카탈로그
├── log.md                    # 작업 기록
├── raw/                      # 원본 소스
│   ├── articles/            # 웹 기사, 블로그
│   ├── papers/              # 논문, 보고서
│   ├── books/               # 도서 노트
│   ├── screenshots/         # 스크린샷, 다이어그램
│   └── assets/              # 이미지 파일
└── wiki/                     # 생성된 페이지
    ├── entities/            # 인물, 회사, 도구
    ├── concepts/            # 개념, 주제
    ├── syntheses/           # 통합 분석, 비교
    ├── sources/             # 소스 요약
    └── log/                 # 쿼리 결과 아카이브
```

## 페이지 포맷

모든 위키 페이지는 이 frontmatter를 가집니다:

```yaml
---
title: "페이지 제목"
type: "entity|concept|synthesis|source"
tags: ["태그1", "태그2"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/articles/example.md"]
---
```

## 워크플로우

### 1. Ingest (소스 추가)

새 소스가 `raw/`에 들어오면:

1. **Read** — 소스를 읽고 주요 내용 추출
2. **Summarize** — `wiki/sources/` 에 요약 페이지 작성
3. **Extract** — 개체, 개념을 식별하고 `wiki/entities/`, `wiki/concepts/`에 페이지 생성 또는 업데이트
4. **Link** — 기존 페이지와의 교차 참조 추가
5. **Index** — `index.md` 업데이트
6. **Log** — `log.md`에 ingest 기록

### 2. Query (질문)

질문을 받으면:

1. `index.md`를 읽어 관련 페이지 찾기
2. 해당 페이지들 읽기
3. 종합하여 답변 작성
4. 필요시 새 합성 페이지를 `wiki/syntheses/`에 생성
5. `log.md`에 쿼리 기록

### 3. Lint (위키 건강도 체크)

정기적으로:

- 모순 탐지
- 고아 페이지 찾기
- 누락된 교차 참조
- 업데이트 필요한 정보
- 탐색할 새로운 질문 제안

## Index.md 포맷

```markdown
# Wiki Index

**Last updated:** [날짜]

## Entities (개체)
- [Entity Name](wiki/entities/entity-name.md) — 한 줄 설명 | 소스 3개

## Concepts (개념)
- [Concept Name](wiki/concepts/concept-name.md) — 한 줄 설명 | 관련 5개

## Syntheses (통합)
- [Title](wiki/syntheses/title.md) — 한 줄 설명 | 소스 2개

## Sources (소스 요약)
- [Title](wiki/sources/title.md) — 날짜 | 카테고리
```

## Log.md 포맷

```markdown
# Log

## [2026-04-22] ingest | Article Title
- Source: raw/articles/...
- Pages created: 3
- Pages updated: 5
- Key topics: topic1, topic2

## [2026-04-22] query | "How to..."
- Query time
- Result: syntheses/...
- Related pages: 7
```

## 워크플로우 명령어

Ingest할 때는 이렇게:
```
/ingest raw/articles/example.md
```

질문할 때는:
```
/query "What is...?"
```

위키 건강도 체크:
```
/lint
```

## 컨벤션

- **파일명**: kebab-case (한글은 로마자 또는 영어)
- **링크**: `[Text](wiki/category/file.md)` (상대경로)
- **태그**: lowercase, 하이픈 구분
- **날짜**: YYYY-MM-DD

