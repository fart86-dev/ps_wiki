---
title: "연계 운행 (Chaining Operations)"
type: "concept"
tags: ["mshuttle", "dispatching", "efficiency", "optimization"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/route_and_dispatch.md"]
---

# 연계 운행 (Chaining Operations)

기사 한 명이 하루에 여러 경로를 연속으로 운행하는 방식.

## 목표

**공차(deadheading) 최소화** — 기사가 빈 차로 이동하는 거리를 줄임

## 구조

```
경로 A (09:00-10:00)
    ↓
경로 B (10:30-11:30)  ← 30분 간격으로 연결
    ↓
경로 C (12:00-13:00)  ← 30분 간격으로 연결
```

## 배차 시 고려사항

### 1. 시간 맞추기
- 경로 A 종료 시간 → 경로 B 출발 시간
- 이동 시간(버퍼) 충분히 확보
- 기사의 휴식 시간 고려

### 2. 위치 최적화
- 경로 A의 종료 지점 → 경로 B의 출발 지점
- 가까울수록 좋음 (이동 거리 ↓)

### 3. 시스템 지원
- **도구**: 시스템에서 기사별 운행 시간표 확인 가능
- **프로세스**: 배차 전 **반드시 확인** (손실 방지)

## 운영 영향

### 긍정적 영향
- 공차 감소 → 운영비 절감
- 기사 효율 증가 → 수익성 개선
- 연료비 절감

### 고려사항
- 기사의 피로도 (하루 여러 경로)
- 일정 변동 시 연쇄 영향
- 경로 간 버퍼 부족 시 지연 위험

## 관련 개념

- [스케줄링의 중요성](../concepts/scheduling-criticality.md) — 연계 운행이 스케줄링의 핵심
- [배차](../concepts/dispatching.md) — 연계 운행을 고려한 배차 의사결정
- [운행 상태](../concepts/operation-state.md) — 운행 중 경로 변경 가능성

---

**출처:**
- [경로 제작 및 배차](../sources/route-and-dispatch-detail.md)
