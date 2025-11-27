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

## SAX Message Format

```markdown
[SAX] Skill: sax-help 실행

/

# SAX-Meta 도움말
...
```

## Related

- [feedback Skill](../feedback/SKILL.md) - SAX 피드백 수집
- [version-manager Skill](../version-manager/SKILL.md) - 버저닝 자동화

## References

- [Help Content](references/help-content.md) - 도움말 상세 내용
