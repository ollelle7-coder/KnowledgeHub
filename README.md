# KnowledgeHub

KnowledgeHub(KH)는 여러 프로젝트를 세밀하게 대신 관리하는 일반 PM 도구가 아니라, 운영자의 판단과 실행을 보조하는 프로젝트 관제 허브다.

## 목적

KH의 목적은 다음 네 가지다.

1. 머릿속에 스팟으로 떠오른 생각과 메모를 놓치지 않게 수집한다.
2. 수집된 입력을 적절한 프로젝트, 작업, 문서, 판단 항목으로 라우팅한다.
3. 지금 운영자가 봐야 할 판단거리와 막힌 지점을 위로 올린다.
4. 프로젝트별 AI, 에이전트, 도구, 저장소를 한 곳에서 관제한다.

## 핵심 원칙

- KH는 프로젝트 관리 시스템이 아니라 의사결정 보조 관제 시스템이다.
- 모든 프로젝트에 필요하지 않은 항목은 공통 항목으로 만들지 않는다.
- 진행 세부사항은 각 프로젝트 안에 둔다.
- KH는 최소 상태, 판단 필요 항목, 막힌 지점, 연결 정보만 추적한다.
- 프로젝트 생성 시 반복되는 셋업은 파이프라인화한다.

## 현재 관리 대상 프로젝트

- EOB
- Cafe_ops
- KS / KnowledgeStorage
- Warship

## 기본 계층

```text
KH
├─ Hub Setup
├─ Operator Inbox
├─ Project Creation Pipeline
├─ Project Registry
└─ Project Profiles
```

## 역할 구분

```text
Hub Setup
- KH 자체 목적, 구조, 대시보드, 권한, 도구 연결 설계

Operator Inbox
- 빠른 메모, 아이디어, 음성/텍스트 입력, 미분류 생각 수집

Project Creation Pipeline
- 새 프로젝트를 관리 가능한 단위로 승격시키는 초기 셋업 절차

Project Registry
- KH가 관제하는 프로젝트 목록과 최소 상태

Project Profiles
- 프로젝트별 특화 관리 항목
```

## KS와의 관계

KS는 KH의 상위 개념이 아니라 KH가 관리하는 프로젝트 중 하나다. 다만 지식 저장소라는 특수성을 가지며, 다른 프로젝트의 확정된 결과물이 KS로 승격될 수 있다.

```text
KH = 판단과 운영을 돕는 관제 허브
KS = 확정 지식을 보존하는 프로젝트/저장소
```

## Agent 문서

- Agent operating guide: `AGENTS.md`
- Claude Code entry file: `CLAUDE.md`
