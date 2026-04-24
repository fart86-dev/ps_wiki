---
title: "기사 운행 (Driver Operation)"
type: "concept"
tags: ["mshuttle", "driver-operation", "operations"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md"]
---

# 기사 운행 (Driver Operation)

기사가 기사 전용 앱을 사용해 셔틀을 운행하는 활동.

## 특징

- **운행 상태 중** 매 운행일마다 진행
- **기사 전용 앱 필수** 사용
- **탑승 체크는 기사가 직접** 앱을 통해 진행

## 핵심 프로세스

1. 기사가 기사 앱 실행
2. 경로 정보 확인
3. 운행 진행
4. 탑승자 체크 (앱을 통해)
5. 운행 데이터 자동 수집

## 중요 주의점

> **앱 미사용 시 관제 데이터가 수집되지 않음**

따라서:
- 기사 앱 사용 여부 반드시 확인 필요
- 미사용 시 [관제](../concepts/control.md) 불가
- 데이터 미수집 → 정산 문제로 이어질 수 있음

## 데이터 흐름

```
기사 앱 사용
  ↓
운행 데이터 수집
  ↓
탑승 체크 기록
  ↓
정산 근거 데이터
```

## 관제 상호작용

기사 운행은 동시에 진행:
- [관제](../concepts/control.md) — 운영팀의 실시간 모니터링
- 탑승 — 유저 탑승

---

**출처:**
- [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)
