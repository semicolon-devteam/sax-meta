---
name: version-manager
description: SAX 패키지 시맨틱 버저닝 자동화. Use when (1) Agent/Skill/Command 변경 후 릴리스, (2) VERSION 및 CHANGELOG 업데이트, (3) Keep a Changelog 형식 버전 관리.
tools: [Bash, Read, Write, Edit]
---

> **🔔 시스템 메시지**: 이 Skill이 호출되면 `[SAX] Skill: version-manager 호출 - {버전 타입}` 시스템 메시지를 첫 줄에 출력하세요.

# version-manager Skill

> SAX 패키지 버저닝 자동화 Skill

## Purpose

SAX 패키지의 Semantic Versioning 관리를 자동화합니다.

- VERSION 파일 업데이트
- CHANGELOG/{version}.md 파일 생성
- CHANGELOG/INDEX.md 업데이트
- Keep a Changelog 형식 준수

## Quick Start

```bash
# 1. 현재 버전 확인
cat sax/VERSION

# 2. 변경사항 분석 후 버전 타입 결정 (MAJOR/MINOR/PATCH)

# 3. VERSION 업데이트
echo "3.15.0" > sax/VERSION

# 4. CHANGELOG 생성
# sax/CHANGELOG/{version}.md 파일 작성

# 5. 커밋 & 푸시
git add -A && git commit -m "🔖 [SAX] 3.15.0: {변경 요약}"
git push origin main

# 6. 🔴 Slack 알림 (필수) - 아래 섹션 참조
```

## Semantic Versioning 요약

| 버전 | 트리거 | 예시 |
|------|--------|------|
| **MAJOR** | 호환성 깨지는 변경 | 워크플로우 근본 변경 |
| **MINOR** | 기능 추가/삭제 | Agent/Skill 추가, CLAUDE.md 변경 |
| **PATCH** | 버그/오타 수정 | 문서 보완, 성능 개선 |

## 🔴 필수: Slack 릴리스 알림

> **버저닝은 Slack 알림까지 완료해야 완료로 간주됩니다.**

커밋 & 푸시 완료 후 **반드시** `notify-slack` Skill 호출:

```markdown
[SAX] Skill: notify-slack 호출 - 릴리스 알림
```

### 알림 내용

| 항목 | 값 |
|------|-----|
| **채널** | #_협업 |
| **타입** | release |
| **패키지** | sax-{package} |
| **버전** | v{new_version} |
| **변경 내역** | CHANGELOG 요약 |

### 완료 확인

```markdown
[SAX] Versioning: Slack 알림 전송 완료 (#_협업)
```

> **⚠️ 이 단계를 누락하면 버저닝 미완료 상태입니다.**

## SAX Message

```markdown
[SAX] Skill: version-manager 사용

[SAX] Versioning: {old_version} → {new_version} ({version_type})

[SAX] Versioning: 커밋 완료 → 푸시 진행

[SAX] Versioning: 완료 (푸시 성공)

[SAX] Skill: notify-slack 호출 - 릴리스 알림

[SAX] Versioning: Slack 알림 전송 완료 (#_협업)
```

## Related

- [sax-architect Agent](../../agents/sax-architect/sax-architect.md)
- [package-validator Skill](../package-validator/SKILL.md)
- [SAX Core - Principles](https://github.com/semicolon-devteam/sax-core/blob/main/PRINCIPLES.md)

## References

For detailed documentation, see:

- [Semantic Versioning Rules](references/semantic-versioning.md) - MAJOR/MINOR/PATCH 상세 규칙
- [Workflow](references/workflow.md) - 9단계 버저닝 프로세스 (커밋 & 푸시 & Slack 알림)
- [Changelog Format](references/changelog-format.md) - Keep a Changelog 템플릿
- [Output Format](references/output-format.md) - 성공/실패 출력, Edge Cases
