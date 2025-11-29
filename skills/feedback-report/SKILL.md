---
name: feedback-report
description: SAX 패키지별 GitHub 피드백 이슈 조회 및 현황 보고. Use when (1) /SAX:feedback-report 명령어 호출, (2) "피드백 현황", "이슈 확인" 키워드, (3) sax-architect가 패키지 상태 점검 시.
tools: [Bash]
---

> **시스템 메시지**: 이 Skill이 호출되면 `[SAX] Skill: feedback-report 호출` 시스템 메시지를 첫 줄에 출력하세요.

# feedback-report Skill

> SAX 패키지별 GitHub 피드백 이슈 현황 조회 및 보고

## Purpose

sax-meta, sax-po, sax-next 3개 패키지의 GitHub 이슈 중 피드백 관련 이슈를 조회하여 집계된 현황을 보고합니다.

## When to Use

| 트리거 | 설명 |
|--------|------|
| `/SAX:feedback-report` | 명시적 피드백 현황 조회 |
| `피드백 현황`, `이슈 확인`, `피드백 몇 개` | 암시적 트리거 |
| sax-architect 패키지 점검 | 자동 호출 |

## Quick Start

```bash
# 각 패키지별 피드백 이슈 조회
gh issue list --repo semicolon-devteam/sax-meta --label "bug,enhancement" --state all --limit 20
gh issue list --repo semicolon-devteam/sax-po --label "bug,enhancement" --state all --limit 20
gh issue list --repo semicolon-devteam/sax-next --label "bug,enhancement" --state all --limit 20
```

## Workflow

### Step 1: 이슈 조회

3개 패키지에서 피드백 이슈를 병렬로 조회합니다:

```bash
# sax-meta
gh issue list --repo semicolon-devteam/sax-meta \
  --search "[Feedback] OR [Bug] in:title" \
  --state all --limit 20 --json number,title,state,createdAt,labels

# sax-po
gh issue list --repo semicolon-devteam/sax-po \
  --search "[Feedback] OR [Bug] in:title" \
  --state all --limit 20 --json number,title,state,createdAt,labels

# sax-next
gh issue list --repo semicolon-devteam/sax-next \
  --search "[Feedback] OR [Bug] in:title" \
  --state all --limit 20 --json number,title,state,createdAt,labels
```

### Step 2: 결과 집계

조회된 이슈를 패키지별로 분류하고 상태(open/closed)별로 집계합니다.

### Step 3: 보고서 출력

```markdown
[SAX] Skill: feedback-report 사용

=== SAX 피드백 현황 ===

📦 **sax-meta** (2건)
| # | 제목 | 상태 | 생성일 |
|---|------|------|--------|
| #12 | [Feedback] version-manager 푸시 누락 | open | 2024-11-29 |
| #8 | [Bug] agent-manager 규칙 오류 | closed | 2024-11-28 |

📦 **sax-po** (1건)
| # | 제목 | 상태 | 생성일 |
|---|------|------|--------|
| #5 | [Feedback] health-check 경로 오류 | open | 2024-11-28 |

📦 **sax-next** (0건)
- 피드백 이슈 없음

=== 요약 ===
- **총**: 3건
- **Open**: 2건 (처리 필요)
- **Closed**: 1건 (해결됨)
```

## Output Format

### 이슈가 있는 경우

```markdown
📦 **{패키지명}** ({총 건수}건)
| # | 제목 | 상태 | 생성일 |
|---|------|------|--------|
| #{번호} | {제목} | {open/closed} | {YYYY-MM-DD} |
```

### 이슈가 없는 경우

```markdown
📦 **{패키지명}** (0건)
- 피드백 이슈 없음
```

### 요약

```markdown
=== 요약 ===
- **총**: {총합}건
- **Open**: {open 수}건 (처리 필요)
- **Closed**: {closed 수}건 (해결됨)
```

## SAX Message Format

```markdown
[SAX] Skill: feedback-report 사용

[SAX] Feedback Report: 조회 완료 (총 {n}건)
```

## Error Handling

### GitHub CLI 미인증

```markdown
[SAX] Skill: feedback-report 오류

❌ GitHub CLI 인증이 필요합니다.

**해결 방법**:
\`\`\`bash
gh auth login
\`\`\`
```

### 레포지토리 접근 불가

```markdown
[SAX] Skill: feedback-report 경고

⚠️ {패키지명} 레포지토리에 접근할 수 없습니다.
- 권한 확인: `gh repo view semicolon-devteam/{패키지명}`
```

## Related

- [feedback Skill](../feedback/SKILL.md) - 피드백 이슈 생성
- [sax-architect Agent](../../agents/sax-architect/sax-architect.md) - 패키지 점검 시 호출
- [Orchestrator](../../agents/orchestrator.md) - 라우팅

## References

For detailed documentation, see:

- [Issue Query Options](references/issue-query.md) - gh issue list 옵션 및 필터
