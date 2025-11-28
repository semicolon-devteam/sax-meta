# SAX-Meta Package Configuration

> SAX 패키지 자체 관리 및 개발을 위한 메타 패키지

## Package Info

- **Package**: SAX-Meta
- **Version**: 📌 [VERSION](./VERSION) 참조
- **Audience**: SAX 개발자, SAX 패키지 관리자

---

## 🔴 Orchestrator-First (최우선 규칙)

> **모든 사용자 요청은 반드시 Orchestrator를 통해 라우팅됩니다.**

### 필수 동작

1. **사용자 요청 수신**: 즉시 `agents/orchestrator.md` 읽기
2. **의도 분석 및 라우팅**: Routing Table에서 적절한 Agent/Skill 매칭
3. **SAX 메시지 출력**: 라우팅 결과를 SAX 포맷으로 출력
4. **위임 실행**: 매칭된 Agent/Skill로 작업 위임
5. **검증 실행**: 작업 완료 후 `compliance-checker` 자동 호출

### 메시지 포맷

```markdown
[SAX] Orchestrator: 의도 분석 완료 → {intent_category}

[SAX] Agent 위임: {agent_name} (사유: {reason})
```

### 예외 없음

- 단순 질문도 Orchestrator 거침
- 직접 Agent/Skill 호출 금지
- Orchestrator 메시지 생략 금지

**상세 라우팅 규칙**: [agents/orchestrator.md](agents/orchestrator.md) 참조

---

## 🔴 SAX Core 필수 참조

> **모든 작업 전 sax-core 문서를 참조합니다.**

| 파일 | 용도 |
|------|------|
| `sax-core/PRINCIPLES.md` | SAX 핵심 원칙 |
| `sax-core/MESSAGE_RULES.md` | 메시지 포맷 규칙 |

---

## 필수 원칙

### 1. 세션 컨텍스트 비의존

> **SAX는 세션 컨텍스트에 의지하지 않는다.**

모든 필수 정보는 **Reference Chain**을 통해 접근 가능해야 함:

```text
Agent/Skill → references/ → sax-core/ → docs 레포 문서
```

### 2. 패키지 접두사 명령

| 접두사 | 대상 |
|--------|------|
| `[po]` | sax-po만 |
| `[next]` | sax-next만 |
| `[core]` | sax-core만 |
| `[meta]` | sax-meta만 |
| `[po \| next]` | 복수 패키지 |
| `[all]` / (없음) | 모든 패키지 |

### 3. 서브모듈 수정 시 로컬 동기화

> **sax-meta 수정 후 반드시 `.claude/sax-meta/` 동기화**

```bash
cd sax-meta && git push origin main && cd ../.claude/sax-meta && git pull origin main
```

### 4. 작업 완료 후 버저닝

> **🔴 "작업 완료" = 버저닝까지 포함. 버저닝 없이는 작업 완료로 간주하지 않음.**

| 변경 유형 | 버전 타입 |
|----------|----------|
| Agent/Skill/Command 추가/수정/삭제 | MINOR |
| 버그/오타 수정 | PATCH |
| Breaking Change | MAJOR |

#### 버저닝 자동화 규칙

**TodoWrite 자동 추가**:

- Agent/Skill/Command 파일 수정 감지 시 TodoWrite에 "버저닝 처리" 항목 **자동 추가**
- 해당 항목 완료 전까지 작업 완료로 간주하지 않음

**커밋 전 검증**:

- Agent/Skill/Command 변경 커밋 시 다음 확인 필수:
  - VERSION 파일 업데이트 여부
  - CHANGELOG/{version}.md 생성 여부
- 버저닝 미완료 상태에서 커밋 시도 시 경고 출력

#### 세션 복원 시 규칙 재로드

> **이전 세션 이어서 작업 시 CLAUDE.md 필수 규칙 섹션 자동 참조**

세션 복원/컨텍스트 손실 후 작업 재개 시:

1. CLAUDE.md의 "작업 완료 후 버저닝" 섹션 재확인
2. 이전 작업의 버저닝 완료 여부 점검
3. 미완료 버저닝 발견 시 우선 처리

### 5. 규칙 준수 검증

> **모든 작업 완료 후 compliance-checker가 자동 실행됩니다.**

검증 항목:

- sax-core 규칙 준수
- 적절한 Agent/Skill 사용 여부
- 문서 중복 여부 (SoT 원칙)

**상세**: [compliance-checker Agent](agents/compliance-checker/compliance-checker.md) 참조

---

## References

- [SAX Core - Principles](https://github.com/semicolon-devteam/sax-core/blob/main/PRINCIPLES.md)
- [SAX Core - Message Rules](https://github.com/semicolon-devteam/sax-core/blob/main/MESSAGE_RULES.md)
- [Orchestrator](agents/orchestrator.md) - 라우팅 규칙 및 Agent/Skill 목록
