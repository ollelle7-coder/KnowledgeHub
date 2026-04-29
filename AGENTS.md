# KnowledgeHub Agent Operating Guide

AGENTS.md is the canonical operating guide for agents working in this repository.

## Core Definition

KnowledgeHub(KH)는 일반 PM 도구가 아니라 의사결정 보조 관제 허브다. KH는 여러 프로젝트의 세부 진행을 대신 관리하는 시스템이 아니라, 운영자의 판단과 실행 흐름을 보조하는 관제 시스템이다.

KH의 핵심 역할은 다음 네 가지다.

```text
Capture - 운영자의 생각, 메모, 외부 입력을 놓치지 않게 받는다.
Route   - 수집된 입력을 프로젝트, 작업, 문서, 판단 항목으로 보낸다.
Surface - 지금 운영자가 봐야 할 판단거리와 막힌 지점을 위로 올린다.
Track   - 열려 있는 작업과 최소 상태만 추적한다.
```

## Current Projects

현재 KH가 관리하는 대상 프로젝트는 다음 네 개다.

- EOB
- Cafe_ops
- KS / KnowledgeStorage
- Warship

KS는 KH의 상위 개념이 아니라 KH가 관리하는 프로젝트 중 하나다. 다만 지식 저장소라는 특수성을 가지며, 다른 프로젝트의 확정된 결과물이 KS로 승격될 수 있다.

## Operating Principles

- 모든 프로젝트에 필요하지 않은 항목은 공통 항목으로 만들지 않는다.
- 프로젝트 세부 관리는 각 Project Profile에 둔다.
- KH 공통 추적 항목은 최소화한다.
- KH는 프로젝트별 문서와 판단 내용을 내부에 중복 저장하지 않는다.
- 허브 자체가 또 하나의 과도한 관리 대상이 되지 않게 한다.
- 불확실한 판단 지점은 정책을 새로 꾸며내지 말고 판단 필요 항목으로 보존한다.

## Shared Structures

Operator Inbox는 운영자의 순간 메모와 아이디어를 휘발되지 않게 수집하는 장치다. 정리 자체보다 빠른 수집과 이후 라우팅을 우선한다.

Project Creation Pipeline은 새 프로젝트 생성 시 반복 셋업을 파이프라인화하는 장치다. 프로젝트의 일상 관리를 대신하는 곳이 아니라, 아이디어를 관리 가능한 프로젝트로 승격시키는 초기 셋업 절차다.

Project Profiles는 프로젝트별 특화 관리 항목을 두는 곳이다. 공통 항목에 넣기 애매하거나 프로젝트마다 형태가 다른 내용은 각 Project Profile에 둔다.

## Documentation Priority

KH 문서 기준과 설계 판단은 다음 문서를 우선 참조한다.

1. `README.md`
2. `_Setup/01_Design/KH-Overview-2026-04-29.md`

비중 있는 구조 변경이나 운영 정책 변경 전에는 위 문서를 확인하고, AGENTS.md와 충돌하는 내용이 있으면 먼저 사용자에게 확인한다.

## Write Policy

- 구조 변경은 관련 README나 설계 노트도 함께 갱신한다.
- 프로젝트별 규칙과 세부사항은 Project Profile에 둔다.
- 임시 생각과 빠른 메모는 Operator Inbox 성격의 문서나 도구에 둔다.
- `CLAUDE.md` 같은 도구 전용 파일에 운영 정책을 길게 중복하지 않는다.
