---
name: sax-help
description: SAX-Meta 패키지 사용 가이드 및 도움말. Use when (1) "/SAX:help" 명령어, (2) "도움말", "SAX란", "어떻게 해" 키워드, (3) SAX 사용법 질문.
tools: [Read]
---

> **🔔 시스템 메시지**: 이 Skill이 호출되면 `[SAX] Skill: sax-help 실행` 시스템 메시지를 첫 줄에 출력하세요.

# sax-help Skill

> SAX-Meta 패키지 사용 가이드 및 워크플로우 안내

## Purpose

SAX-Meta 패키지 사용자(SAX 개발자, 패키지 관리자)에게 사용 가능한 기능과 워크플로우를 안내합니다.

## 출력 포맷

```markdown
[SAX] Skill: sax-help 실행

/

# SAX-Meta 도움말

**패키지**: SAX-Meta v{version}
**대상**: SAX 개발자, 패키지 관리자

## 📋 사용 가능한 명령어

### Agent 관리
| 명령어 | 설명 |
|--------|------|
| `새 Agent 만들어줘` | SAX Agent 생성 |
| `Agent 수정해줘` | 기존 Agent 수정 |
| `Agent 삭제해줘` | Agent 제거 |
| `Agent 검토해줘` | Agent 품질 분석 |

### Skill 관리
| 명령어 | 설명 |
|--------|------|
| `새 스킬 만들어줘` | SAX Skill 생성 |
| `스킬 수정해줘` | 기존 Skill 수정 |
| `스킬 삭제해줘` | Skill 제거 |
| `스킬 분석해줘` | Skill 품질 분석 |

### Command 관리
| 명령어 | 설명 |
|--------|------|
| `슬래시 커맨드 만들어줘` | Command 생성 |
| `Command 수정해줘` | 기존 Command 수정 |

### 패키지 관리
| 명령어 | 설명 |
|--------|------|
| `버전 올려줘` | 시맨틱 버저닝 |
| `패키지 검증해줘` | 구조 검증 |
| `패키지 동기화해줘` | .claude/ 동기화 |
| `패키지 배포해줘` | 외부 프로젝트 배포 |

### 피드백
| 명령어 | 설명 |
|--------|------|
| `/SAX:feedback` | SAX 피드백/버그 신고 |

## 📌 패키지 접두사

특정 패키지를 지정하여 작업할 수 있습니다:

| 접두사 | 대상 |
|--------|------|
| `[po]` | sax-po만 |
| `[next]` | sax-next만 |
| `[meta]` | sax-meta만 |
| `[core]` | sax-core만 |
| `[po \| next]` | 복수 패키지 |
| `[all]` | 모든 패키지 |

**예시**: `[po | next] 새 스킬 추가해줘`

## 🔗 참조 문서

- [SAX Core Principles](https://github.com/semicolon-devteam/sax-core/blob/main/PRINCIPLES.md)
- [SAX Core Message Rules](https://github.com/semicolon-devteam/sax-core/blob/main/MESSAGE_RULES.md)
```

## Execution Flow

1. VERSION 파일에서 현재 버전 읽기
2. 위 출력 포맷으로 도움말 출력
3. 사용자 추가 질문 대기

## 대화형 워크플로우

### Step 1: 상황 파악

사용자의 현재 상황을 파악합니다:

```markdown
[SAX] Skill: sax-help 실행

## 🤝 SAX 도우미 (패키지 개발자/관리자)

무엇을 도와드릴까요?

### 💭 질문 유형을 선택하세요

1. **📍 SAX 구조 이해**: "SAX 패키지 구조가 어떻게 되나요?"
2. **🔧 Agent/Skill/Command 관리**: "새 Agent를 추가하고 싶어요"
3. **📦 패키지 배포**: "패키지를 배포하고 싶어요"
4. **🔄 버저닝**: "버전 릴리스는 어떻게 하나요?"
5. **🛠️ 도구 사용법**: "각 매니저(Agent/Skill/Command)는 뭐가 달라요?"
6. **❓ 기타**: "다른 질문이 있어요"

번호를 선택하거나 자유롭게 질문해주세요.
```

### Step 2: 맞춤형 응답

사용자 선택에 따라 적절한 정보 제공:

- **1️⃣ SAX 구조**: SAX 패키지 계층 구조 설명
- **2️⃣ 컴포넌트 관리**: 해당 Manager Agent로 위임
- **3️⃣ 패키지 배포**: package-deploy skill 안내
- **4️⃣ 버저닝**: version-manager skill 안내
- **5️⃣ 도구 사용법**: 각 Manager 역할 비교 설명
- **6️⃣ 기타**: 자유 질문 응답

### Step 3: 추가 질문 유도

```markdown
---

**도움이 되셨나요?**

다른 궁금한 점이 있으시면 언제든 물어보세요:
- "Agent 만들어줘" → agent-manager 호출
- "Skill 추가해줘" → skill-manager 호출
- "/SAX:help" → 도움말 처음으로
```

## Integration with Other Tools

### agent-manager Agent

```markdown
User: "새 Agent 만들어줘"
→ [SAX] Agent 위임: agent-manager (사유: SAX Agent 생성)
```

### skill-manager Agent

```markdown
User: "새 Skill 추가해줘"
→ [SAX] Agent 위임: skill-manager (사유: SAX Skill 생성)
```

### command-manager Agent

```markdown
User: "새 Command 만들어줘"
→ [SAX] Agent 위임: command-manager (사유: SAX Command 생성)
```

## SAX Message Format

```markdown
[SAX] Skill: sax-help 실행

## 🤝 SAX 도우미 (패키지 개발자/관리자)
...
```

## Critical Rules

1. **대화형 접근**: 사용자가 질문을 선택하거나 자유롭게 물어볼 수 있도록
2. **SAX 개발자 맥락 유지**: 패키지 개발/관리 관점의 응답
3. **단계적 안내**: 한 번에 한 단계씩, 명확하게
4. **추가 질문 유도**: 항상 "더 궁금한 점?" 질문
5. **Agent/Skill 위임**: 복잡한 작업은 적절한 Agent/Skill로 위임

## Related

- [feedback Skill](../feedback/SKILL.md) - SAX 피드백 수집
- [version-manager Skill](../version-manager/SKILL.md) - 버저닝 자동화

## References

- [Help Content](references/help-content.md) - 도움말 상세 내용
