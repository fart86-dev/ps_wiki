---
title: "스케줄링의 중요성"
type: "concept"
tags: ["mshuttle", "scheduling", "core-value", "efficiency"]
created: "2026-04-22"
updated: "2026-04-22"
sources: ["raw/papers/mshuttle 서비스 전체 흐름 33340c143d6e81a6aaf3f197879795c5.md"]
---

# 스케줄링의 중요성

## 핵심 원칙

> **스케줄링이 mshuttle 서비스의 핵심**

## 왜 중요한가?

mshuttle의 특성:
- **여러 유저가 같은 경로 공유** → 공차거리(deadheading) 최소화 필요
- **한 기사가 여러 경로 담당** → 효율적인 배치 필요

이 조건에서 **누가 언제 어디서 타는지**를 얼마나 효율적으로 배치하느냐가:
- **공차거리 최소화** (운영 효율성)
- **비용 합리성** (고객 만족도)
에 직결됨

## 현재 상황

**스케줄링은 운영팀이 수동으로 판단**

- DB 쿼리를 통해 근거 데이터 제공받음
- 이 데이터에 기반해 의사결정
- 수동 프로세스 → 자동화 기회 있음

## 최적화 방향

스케줄링 자동화/최적화를 통해:
- 공차거리 감소 → 운영비 절감
- 배차 속도 향상 → 고객 대응력 개선
- 운영팀 업무 부담 감소

## 관련 개념

- [경로](../concepts/route.md) — 스케줄링의 기본 단위
- [배차](../concepts/dispatching.md) — 스케줄링의 실행 프로세스
- [운행 상태](../concepts/operation-state.md) — 스케줄링 결과의 운영
- [연계 운행](../concepts/chaining-operations.md) — 스케줄링 최적화의 핵심 (공차 최소화)

---

**출처:**
- [mshuttle 서비스 전체 흐름](../sources/mshuttle-overview.md)
