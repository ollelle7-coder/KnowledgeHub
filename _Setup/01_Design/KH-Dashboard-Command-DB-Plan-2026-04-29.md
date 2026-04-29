# KH Dashboard Command & DB Plan - 2026-04-29

## 1. 결론

KH Dashboard는 React 기반 웹 콘솔로 설계한다.

초기 핵심은 단순 모니터링이 아니라 아래 흐름을 다루는 Command Hub다.

```text
명령 생성
↓
명령 전달
↓
수행 상태 추적
↓
결과 회수
↓
대시보드 표현
↓
사용자 판단/승인
```

KH는 여러 AI 앱의 화면을 그대로 띄우는 도구가 아니다. Claude Code, Codex, GPT, GitHub, Local Worker 등에 보낸 명령과 결과를 프로젝트 단위로 추적하는 운영 허브다.

## 2. 기술 방향

### Frontend

```text
React / Next.js
```

이유:

- KH는 모바일 앱보다 운영 콘솔 성격이 강하다.
- 프로젝트별 카드, 명령 입력, 로그 확인, 결과 확인에 웹 UI가 적합하다.
- GitHub, 파일 링크, 로컬 서버, NAS, API 연동을 표현하기 쉽다.

### Backend

초기 후보:

```text
FastAPI
```

또는 Next.js API route로 더 단순하게 시작할 수 있다.

### DB

초기:

```text
SQLite
```

확장 시:

```text
PostgreSQL
```

초기에는 혼자 쓰는 로컬/개인 허브이므로 SQLite로 충분하다. 여러 워커, 장기 운영, 외부 접속, 동시 작업이 늘어나면 PostgreSQL 전환을 검토한다.

## 3. KH DB의 역할

KH DB는 지식 원본 저장소가 아니다.

KH DB는 운영 상태를 저장한다.

```text
KH DB = 명령, 전달, 상태, 결과, 판단 필요 항목을 저장
KS = 확정 지식의 원본 저장소
```

## 4. KH DB에 들어갈 주요 데이터

### Projects

KH가 관제하는 프로젝트 목록과 최소 상태.

```text
- id
- name
- type
- status
- repo_url
- profile_path
- dashboard_order
- last_activity_at
```

현재 대상:

```text
- EOB
- Cafe_ops
- KS / KnowledgeStorage
- Warship
```

### Commands

사용자가 KH를 통해 내린 명령.

```text
- id
- project_id
- title
- instruction
- target_tool
- expected_result
- priority
- status
- created_at
- updated_at
```

상태 예시:

```text
draft / dispatched / running / blocked / done / failed / cancelled
```

### Dispatches

명령이 어떤 도구나 에이전트에 어떻게 전달되었는지 기록한다.

```text
- id
- command_id
- target_tool
- delivery_method
- sent_at
- external_link
- log_path
- current_status
```

대상 도구 예시:

```text
- Claude Code
- Codex
- GPT
- GitHub
- Local Worker
```

### Results

명령 수행 결과.

```text
- id
- command_id
- summary
- output_path
- changed_files
- blocker
- next_action
- needs_decision
- received_at
```

### Operator Inbox

운영자의 순간 메모와 아이디어 수집.

```text
- id
- raw_input
- source
- status
- routed_project_id
- routed_command_id
- created_at
```

목적은 정리 자체가 아니라 휘발 방지다.

### Decisions

사용자가 내린 결정과 연결 정보.

```text
- id
- project_id
- command_id
- result_id
- decision
- reason
- created_at
```

### Agents / Tools

KH가 명령을 전달할 수 있는 대상.

```text
- id
- name
- type
- status
- permission_level
- notes
```

## 5. 프로젝트별 대시보드 표현

대시보드는 프로젝트 단위로 명령과 결과를 보여준다.

예시:

```text
Cafe_ops
- Active Command: KH-CMD-0007
- Tool: Claude Code
- Status: Running
- Last Update: 2026-04-29 20:55
- Result: Pending
- Needs Decision: No

KS
- Active Command: KH-CMD-0008
- Tool: Codex
- Status: Blocked
- Blocker: 파일 경로 확인 필요
- Needs Decision: Yes

EOB
- Active Command: None
- Last Result: EP2 플롯 검토 완료
- Needs Decision: Save the Cat 구조 반영 여부
```

## 6. 명령 흐름

### 1단계: 명령 생성

사용자가 KH에 명령을 입력한다.

```text
Project: Cafe_ops
Target Tool: Claude Code
Instruction: 재고관리 UX 개선안 기준으로 화면 구조 점검
Expected Result: 개선안 요약 + 수정 필요 파일 목록
```

### 2단계: 명령 전달

KH는 명령 ID를 만들고 전달 상태를 기록한다.

```text
KH-CMD-0007
Status: dispatched
Target: Claude Code
```

### 3단계: 수행 상태 추적

도구나 에이전트는 상태 파일, 로그, 커밋, PR, 결과 문서 중 하나로 진행 정보를 남긴다.

### 4단계: 결과 회수

결과는 표준 위치나 결과 파일로 회수한다.

예시:

```text
_AI-State/results/KH-CMD-0007.md
```

### 5단계: 대시보드 표현

KH는 결과 요약, 변경 파일, 막힌 지점, 승인 필요 여부를 대시보드에 표시한다.

## 7. AI 화면 직접 모니터링에 대한 판단

Claude Code, Codex, GPT의 실제 UI를 KH Dashboard 안에 그대로 임베드하는 방식은 우선순위가 낮다.

이유:

- 각 서비스의 세션 화면을 외부에서 직접 읽거나 임베드하기 어렵다.
- 내부 상태 접근이 제한된다.
- 실시간 미러링보다 명령/결과 추적이 운영 가치가 크다.

따라서 초기 방향은 다음과 같다.

```text
틀린 방향:
각 AI 앱 화면을 그대로 한 화면에 띄우기

맞는 방향:
각 AI에게 보낸 명령과 결과를 프로젝트 단위로 추적하기
```

## 8. KS DB화 판단

KS는 당장 DB 구조로 바꾸지 않는다.

현재는 Markdown/Git 기반을 유지한다.

이유:

- 사람이 읽기 쉽다.
- Git으로 변경 이력을 추적하기 좋다.
- AI가 문맥으로 읽기 좋다.
- 아직 스키마를 고정하기 이르다.

나중에는 KS 원본을 DB로 바꾸는 것이 아니라, 색인 DB를 붙이는 방향이 적합하다.

```text
KS Markdown 원본
↓
Indexer
↓
Search DB / Vector DB / Metadata DB
↓
KH에서 검색/참조
```

색인 대상 예시:

```text
- 문서 제목
- 프로젝트
- 태그
- 상태
- 마지막 수정일
- 요약
- 관련 결정
- 임베딩
```

## 9. 단계별 구현 방향

### 1단계

```text
React / Next.js Dashboard
SQLite
Projects / Commands / Dispatches / Results 최소 모델
수동 명령 입력과 결과 등록
```

### 2단계

```text
Operator Inbox
Project Registry
Project Profiles 연결
상태 파일 기반 결과 회수
```

### 3단계

```text
GitHub commit / PR / issue 연결
Claude Code / Codex / GPT 결과 로그 표준화
```

### 4단계

```text
Local Worker
NAS / 파일 시스템 연동
스케줄 작업
```

### 5단계

```text
PostgreSQL 전환 검토
KS 색인 DB / 검색 인덱스 / Vector DB 연결
```

## 10. 현재 결정

- KH Dashboard는 React / Next.js 기반으로 생각한다.
- KH DB는 운영 상태 저장용으로 둔다.
- 초기 DB는 SQLite가 적합하다.
- KS는 Markdown/Git 원본을 유지한다.
- KS DB화는 나중에 색인 DB 방식으로 검토한다.
- KH의 1차 핵심은 Command Hub다.
