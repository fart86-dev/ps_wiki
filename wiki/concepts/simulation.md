---
title: "시뮬레이션 (Simulation)"
type: "concept"
tags: ["mshuttle", "simulation", "driver", "pre-operation"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md"]
---

# 시뮬레이션 (Simulation)

배차 완료 후 기사가 해당 경로에 대해 진행하는 사전 확인 프로세스.

## 진행 시점

- **[배차](../concepts/dispatching.md) 완료 직후**
- **정기 경로만** 진행 (비정기 경로는 미진행)

## 진행 주체

- **기사** — 기사 앱 정보 기반으로 경로 점검

## 내용

- 배정된 경로 정보 확인
- 출발점, 경유지, 도착점 확인
- 예상 시간, 거리 확인
- 주의사항 확인

## 완료 후

시뮬레이션 완료 시:
- 운영팀이 경로 상태를 "운행"으로 전환
- 실제 운행 시작 준비 완료

## 특징

- 정기 경로의 안정성 보장 수단
- 기사의 경로 숙지 확인
- 비정기(1회성)는 불필요하므로 미진행

---

**출처:**
- [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)
