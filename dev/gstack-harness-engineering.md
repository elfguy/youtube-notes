# 🔧 gstack? 하네스 엔지니어링? | 직접 써봤더니 진짜 중요한 건 따로 있었다 — 요약

> **영상:** https://youtu.be/OvZiSEZpzxs
> **요약일:** 2026-04-02

---

## 핵심 메시지

**"프롬프트를 잘 쓰는 시대는 끝났다. AI가 실수할 수 없는 환경을 설계하는 시대다."**

gstack과 하네스 엔지니어링 — 둘 다 요즘 AI 코딩계에서 동시에 터진 개념이다. 이 영상은 두 기술이 정확히 어떤 문제를 해결하려고 나온 건지, 실제로 써보면 진짜 중요한 게 뭔지를 다룬다.

---

## 📋 주요 개념

### 1. gstack — YC CEO가 공개한 Claude Code 실전 셋업

**배경:** Y Combinator CEO **Garry Tan**이 자신의 Claude Code 셋업을 오픈소스로 공개
- 공개 2주 만에 GitHub **56,000+ ⭐** 획득
- 한 줄 요약: *"That is not a copilot. That is a team."*

**철학:**
```
"Planning is not review.
Review is not shipping.
Founder taste is not engineering rigor."
```

기획, 리뷰, 배포는 전부 다른 인지 모드가 필요하다. 같은 프롬프트 창에서 다 하면 "어중간하게 다 하는" 결과가 나온다.

**구성:** 29개 슬래시 커맨드 스킬 (역할별 AI 에이전트)

| 카테고리 | 주요 스킬 | 역할 |
|---------|---------|------|
| 기획·리뷰 | `/office-hours` | YC Office Hours — 6가지 강제 질문으로 방향 확정 |
| 기획·리뷰 | `/plan-ceo-review` | 창업자 관점 — 10배 더 나은 제품 상상 |
| 기획·리뷰 | `/plan-eng-review` | 엔지니어링 매니저 — 아키텍처·엣지케이스 확정 |
| 기획·리뷰 | `/autoplan` | CEO→Design→Eng 자동 순차 실행 |
| 디자인 | `/design-review` | 라이브 사이트 80항목 시각 감사 + 자동 수정 |
| 구현·테스트 | `/review` | Staff Engineer — 프로덕션 버그 탐색 |
| 구현·테스트 | `/qa` | QA Lead — 버그 발견→수정→재검증 루프 |
| 구현·테스트 | `/cso` | OWASP + STRIDE 보안 감사 |
| 배포 | `/ship` | Release Engineer — 배포 관리 |
| 안전 | `/freeze` / `/guard` | 파괴적 명령 차단, 작업 범위 잠금 |

**설치:**
```bash
# 요구사항: Claude Code + Git + Bun v1.0+
gh repo clone garrytan/gstack
```

---

### 2. 하네스 엔지니어링 (Harness Engineering)

**정의:** 프롬프트보다 넓은 개념 — AI 에이전트가 작동하는 **환경 전체**를 설계하는 것
- 운영 규칙, 역할 분리 구조, 검증 루프, 안전 가드레일 포함

**배경:** 2026년 두 달 간격으로 양대 AI 회사가 동시 발표
- OpenAI: *"Harness Engineering"* (2026-02-11)
- Anthropic: *"Harness Design for Long-Running Apps"* (2026-03-24)

**핵심 원칙:**

| 원칙 | gstack 구현 |
|------|------------|
| 환경 설계 | `CLAUDE.md` — 세션 시작 시 항상 로드되는 운영 규칙 |
| 역할 분리 | `SKILL.md` 기반 29개 역할 명시적 분리 |
| 피드백 루프 | `/autoplan` → 구현 → `/review` · `/qa` |
| 행동 가드레일 | `/careful` · `/freeze` · `/guard` |

**프롬프트 엔지니어링 vs 하네스 엔지니어링:**
- 프롬프트: 더 긴 프롬프트로 더 좋은 결과
- 하네스: 같은 모델이 더 일관되게 일하도록 **행동 공간 자체를 재설계**

**실증 데이터:**
> LangChain이 모델을 고정하고 하네스만 변경 → 에이전트 벤치마크 52.8 → **66.5** (↑26%)

---

### 3. 진짜 중요한 건 따로 있었다

gstack을 써보면서 깨닫는 핵심:

1. **역할 분리가 핵심** — "만능 AI"에게 다 맡기면 만능으로 실패한다
2. **검증 루프를 구조화** — 자기 코드를 자기가 리뷰하면 맹점이 생긴다
3. **CLAUDE.md = 항상 로드되는 운영 규칙** — 매번 프롬프트에 쓰는 것보다 훨씬 강력
4. **`/office-hours`가 핵심** — 코딩 시작 전 6가지 강제 질문으로 방향을 확정하는 구조

---

## 💡 핵심 인사이트

1. **같은 모델, 다른 하네스 → 다른 결과** — 더 좋은 모델이 아니라 더 좋은 환경이 답
2. **역할 스위칭이 게임 체인저** — CEO 모드 / Staff Engineer 모드 / QA 모드는 전혀 다른 사고방식
3. **"Humans steer. Agents execute."** — 방향은 사람이, 실행은 AI가
4. **프롬프트는 복사할 수 있지만 구조적 설계는 재발명되지 않는다**

---

## 📌 Leo한테 의미있는 포인트

### 우리가 바로 쓸 수 있는 것들

**1. lineage-rpg에 gstack 구조 적용**
- 이미 Prometheus(기획), Hephaestus(구현), QA Tester 역할 분리해서 비슷하게 가고 있음
- `/office-hours` 개념: 개발 시작 전 6가지 질문 체크리스트화 가능

**2. OWL 봇 개발에서 역할 분리**
- 전략 설계(CEO 모드) / 코드 구현(Engineer 모드) / 백테스트 검증(QA 모드) 분리
- 지금 Brain/autopilot 구조가 사실 하네스 엔지니어링과 같은 방향

**3. CLAUDE.md를 운영 규칙 레벨로 강화**
- 각 프로젝트의 CLAUDE.md에 역할별 행동 가이드라인 추가
- 청약비서, 피다, OWL 각각 맞춤화

**4. OpenClaw에서 이미 하네스 엔지니어링 하고 있음**
- `sessions_spawn` = Sub-Agent 병렬 실행
- 크론 = 자동화 검증 루프
- SKILL.md = gstack의 역할별 스킬과 동일 구조
- AGENTS.md / SOUL.md = CLAUDE.md의 역할

---

## 🔗 참고 링크

- gstack GitHub: https://github.com/garrytan/gstack
- OpenAI Harness Engineering: https://openai.com/index/harness-engineering/
- Anthropic Harness Design: https://www.anthropic.com/engineering/harness-design-long-running-apps

---

*관련 영상: 하네스 엔지니어링 완전 가이드 — https://goddaehee.tistory.com/565*
