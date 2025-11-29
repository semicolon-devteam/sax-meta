# Issue Query Options

> gh issue list 명령어 옵션 및 필터 가이드

## 기본 명령어

```bash
gh issue list --repo {owner}/{repo} [options]
```

## 주요 옵션

| 옵션 | 설명 | 예시 |
|------|------|------|
| `--repo` | 대상 레포지토리 | `semicolon-devteam/sax-meta` |
| `--state` | 이슈 상태 | `open`, `closed`, `all` |
| `--label` | 라벨 필터 (쉼표 구분) | `bug,enhancement` |
| `--search` | 검색 쿼리 | `"[Feedback] in:title"` |
| `--limit` | 조회 개수 제한 | `20` |
| `--json` | JSON 출력 필드 | `number,title,state,createdAt` |

## 피드백 이슈 조회 쿼리

### 제목 기반 검색

```bash
# [Feedback] 또는 [Bug] 접두사가 있는 이슈
gh issue list --repo semicolon-devteam/sax-meta \
  --search "[Feedback] OR [Bug] in:title" \
  --state all \
  --limit 20
```

### 라벨 기반 검색

```bash
# bug 또는 enhancement 라벨이 있는 이슈
gh issue list --repo semicolon-devteam/sax-meta \
  --label "bug" \
  --state all \
  --limit 20

gh issue list --repo semicolon-devteam/sax-meta \
  --label "enhancement" \
  --state all \
  --limit 20
```

### JSON 출력

```bash
gh issue list --repo semicolon-devteam/sax-meta \
  --search "[Feedback] in:title" \
  --state all \
  --json number,title,state,createdAt,labels,author
```

**출력 예시**:

```json
[
  {
    "number": 12,
    "title": "[Feedback] version-manager 푸시 누락",
    "state": "OPEN",
    "createdAt": "2024-11-29T10:00:00Z",
    "labels": [{"name": "bug"}, {"name": "sax-meta"}],
    "author": {"login": "username"}
  }
]
```

## 패키지별 레포지토리

| 패키지 | 레포지토리 |
|--------|-----------|
| sax-meta | `semicolon-devteam/sax-meta` |
| sax-po | `semicolon-devteam/sax-po` |
| sax-next | `semicolon-devteam/sax-next` |

## 필터 조합 예시

### Open 피드백만 조회

```bash
gh issue list --repo semicolon-devteam/sax-meta \
  --search "[Feedback] in:title" \
  --state open \
  --limit 10
```

### 최근 7일 이내 생성된 이슈

```bash
gh issue list --repo semicolon-devteam/sax-meta \
  --search "[Feedback] in:title created:>$(date -v-7d +%Y-%m-%d)" \
  --state all
```

### 특정 작성자의 이슈

```bash
gh issue list --repo semicolon-devteam/sax-meta \
  --search "[Feedback] in:title author:username" \
  --state all
```

## 출력 포맷팅

### 테이블 형식 (기본)

```bash
gh issue list --repo semicolon-devteam/sax-meta
```

### JSON → 마크다운 테이블 변환

```bash
gh issue list --repo semicolon-devteam/sax-meta \
  --json number,title,state,createdAt \
  | jq -r '.[] | "| #\(.number) | \(.title) | \(.state) | \(.createdAt[:10]) |"'
```

## 에러 처리

### 레포지토리 없음

```text
GraphQL: Could not resolve to a Repository with the name 'semicolon-devteam/sax-meta'.
```

**해결**: 레포지토리 이름 확인, 접근 권한 확인

### 인증 필요

```text
gh: To use GitHub CLI, you must authenticate by running `gh auth login`
```

**해결**: `gh auth login` 실행

### 권한 부족

```text
GraphQL: Resource not accessible by integration
```

**해결**: Organization 멤버십 확인, 레포 접근 권한 확인
