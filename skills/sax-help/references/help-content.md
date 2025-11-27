# Help Content

> SAX-Meta 도움말 상세 내용

## 패키지 개요

SAX-Meta는 SAX 패키지 자체를 관리하고 개발하기 위한 **메타 패키지**입니다.

### 대상 사용자

- **SAX 개발자**: SAX 프레임워크를 개선하고 확장하는 개발자
- **패키지 관리자**: SAX 패키지 구조, 버저닝, 배포를 담당하는 관리자

### 비대상 사용자

- PO/기획자 → SAX-PO 사용
- Next.js 개발자 → SAX-Next 사용

## 주요 워크플로우

### 1. Agent 생성 워크플로우

```
"새 Agent 만들어줘"
→ Orchestrator: Agent 생성 요청
→ agent-manager: Agent 정보 수집
→ Agent 파일 생성
→ package-validator: 구조 검증
→ version-manager: 버저닝
```

### 2. Skill 생성 워크플로우

```
"새 스킬 만들어줘"
→ Orchestrator: Skill 생성 요청
→ skill-manager: Skill 정보 수집
→ SKILL.md + references/ 생성
→ package-validator: 구조 검증
→ version-manager: 버저닝
```

### 3. 버저닝 워크플로우

```
"버전 올려줘"
→ Orchestrator: 버전 관리 요청
→ version-manager: 변경사항 분석
→ VERSION 업데이트
→ CHANGELOG 생성
→ 커밋
```

## 패키지 구조

```
sax-meta/
├── CLAUDE.md           # 패키지 설정
├── VERSION             # 현재 버전
├── agents/             # Agent 정의
│   ├── orchestrator.md
│   ├── agent-manager/
│   ├── skill-manager/
│   ├── command-manager/
│   └── sax-architect.md
├── skills/             # Skill 정의
│   ├── sax-help/
│   ├── feedback/
│   ├── package-validator/
│   ├── package-sync/
│   ├── package-deploy/
│   └── version-manager/
└── commands/           # Slash Command
    └── help.md
```

## 자주 묻는 질문

### Q: 새 Agent는 어떻게 만드나요?

"새 Agent 만들어줘"라고 요청하면 agent-manager가 필요한 정보를 수집하고 Agent 파일을 생성합니다.

### Q: 버전은 언제 올려야 하나요?

- Agent/Skill/Command 추가/수정/삭제 → MINOR
- 버그/오타 수정 → PATCH
- Breaking Change → MAJOR

### Q: 다른 패키지도 수정하고 싶어요

`[po | next]` 같은 접두사를 사용하세요. 예: `[po | next] 새 스킬 추가해줘`
