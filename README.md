# Claude Agents Collection 🤖

Claude AI를 위한 전문 에이전트 정의 모음집입니다. 각 에이전트는 특정 작업을 전문적으로 수행하도록 설계되었습니다.

## 🚀 빠른 시작

**완전 초보자**라면? → **[5분 만에 첫 Agent 만들기](QUICKSTART_GUIDE.md)** 📖

복사-붙여넣기만으로 바로 사용할 수 있는 단계별 가이드입니다!

## 📚 목차

- [🚀 빠른 시작](#빠른-시작) ← **초보자는 여기서 시작!**
- [🎬 워크플로우 실제 예시](WORKFLOW_EXAMPLE.md) ← **Agent 연쇄 호출 과정**
- [🔍 Agents vs Skills 차이점](#agents-vs-skills-차이점)
- [🏗️ Agent 구성 방법](#agent-구성-방법)
- [📦 현재 보유 Agent](#현재-보유-agent)
- [🚀 Agent 사용법](#agent-사용법)
- [🛠️ 새로운 Agent 만들기](#새로운-agent-만들기)
- [🔧 Agent 관리](#agent-관리)

> 💡 **처음 사용하시나요?** 위의 "빠른 시작" 링크를 클릭해서 5분 만에 첫 Agent를 만들어보세요!  
> 🎭 **Agent들의 협업이 궁금하다면?** "워크플로우 실제 예시"에서 오케스트레이터가 다른 Agent들을 어떻게 조율하는지 봐보세요!

## 🔍 Agents vs Skills 차이점

### Skills
- **정의**: Claude가 **자동으로 상황을 파악해서 실행**하는 도구
- **위치**: `.claude/skills/skill-name/SKILL.md`
- **실행**: Claude가 필요하다고 판단할 때 자동 실행
- **용도**: 반복적인 도구 사용 패턴 정의 (예: GitHub 조작, 파일 분석)
- **예시**: 코드 리뷰를 요청하면 자동으로 GitHub API 사용해서 분석

### Agents
- **정의**: **특정 역할과 전문성을 가진 독립적인 AI 페르소나**
- **위치**: 별도 `.md` 파일로 정의
- **실행**: 사용자가 명시적으로 호출하거나 다른 Agent가 호출
- **용도**: 전문 작업 수행 (예: 컨텐츠 기획, 카피라이팅, 디자인)
- **예시**: "Instagram 캐러셀 전략가" 역할을 하는 Agent 호출

### 비교표

| 구분 | Skills | Agents |
|------|--------|---------|
| **호출 방식** | Claude가 자동 판단 | 사용자/Agent가 명시적 호출 |
| **역할** | 도구 사용법 가이드 | 전문가 페르소나 |
| **지속성** | 일회성 실행 | 대화 전체에서 역할 유지 |
| **메모리** | 없음 | 프로젝트/세션별 메모리 가능 |
| **구조** | SKILL.md + 스크립트들 | 단일 정의 파일 |

## 🏗️ Agent 구성 방법

### 1. 기본 구조

Agent는 하나의 `.md` 파일로 정의되며, 다음 구조를 따릅니다:

```markdown
---
name: agent-name
description: "Agent 역할과 사용 시점 설명"
model: sonnet
color: blue
memory: project
---

[Agent의 역할, 책임, 작업 방식 정의]
```

### 2. Frontmatter 옵션

```yaml
name: agent-name              # Agent 식별자
description: "상세 설명"      # 언제 사용할지 설명
model: sonnet                 # 사용할 모델 (haiku/sonnet/opus)
color: blue                   # UI에서 표시할 색상
memory: project              # 메모리 범위 (session/project/global)
```

### 3. Agent 본문 작성 가이드

#### 역할 정의
```markdown
You are an elite [전문 역할] specializing in [전문 분야]. 
You have deep expertise in [구체적 전문성] and [핵심 스킬].
```

#### 핵심 책임
```markdown
## YOUR CORE RESPONSIBILITIES

1. **첫 번째 주요 업무**
   - 구체적인 세부 작업들
   - 품질 기준과 제약사항

2. **두 번째 주요 업무**
   - 세부 작업들
   - 결과물 요구사항
```

#### 작업 프로세스
```markdown
## WORKFLOW

1. **입력 분석**: 받은 정보를 어떻게 분석할지
2. **전문성 적용**: 어떤 전문 지식을 활용할지  
3. **결과물 생성**: 최종 산출물 형태와 품질 기준
4. **검증**: 품질 확인 방법
```

#### 제약사항과 품질 기준
```markdown
## CONSTRAINTS

- 반드시 지켜야 할 제약사항들
- 품질 기준과 체크리스트
- 피해야 할 실수들
```

## 📦 현재 보유 Agent

### Instagram 캐러셀 제작 팀

1. **carousel-content-strategist** 🎯
   - **역할**: 컨텐츠 전략 수립 및 리서치
   - **입력**: 주제, 타겟 오디언스, 요구사항
   - **출력**: 전략적 브리프, 슬라이드별 구성안

2. **instagram-carousel-copywriter** ✍️
   - **역할**: 캐러셀 카피라이팅
   - **입력**: 전략 브리프
   - **출력**: 슬라이드별 최종 텍스트

3. **instagram-carousel-generator** 🎨
   - **역할**: HTML 슬라이드 제작
   - **입력**: 최종 카피
   - **출력**: 1080x1440px HTML 파일들

4. **instagram-carousel-orchestrator** 🎭
   - **역할**: 전체 제작 프로세스 관리
   - **입력**: 초기 요구사항
   - **출력**: 완성된 캐러셀 (다른 Agent들 조율)

5. **slide-production-exporter** 📤
   - **역할**: 최종 PNG 익스포트 및 배포
   - **입력**: HTML 슬라이드들
   - **출력**: 소셜미디어 업로드용 이미지

### 작업 플로우
```
사용자 요청 → Orchestrator → Strategist → Copywriter → Generator → Exporter → 완성
```

> 🎬 **실제 동작 과정이 궁금하다면?** → **[워크플로우 실제 예시 보기](WORKFLOW_EXAMPLE.md)**  
> Instagram 캐러셀을 만드는 전체 과정을 Agent들의 실제 대화로 보여줍니다!

## 🚀 Agent 사용법

### 1. 기본 사용법 (가장 쉬움!)
Claude와 대화할 때 이렇게 말해보세요:

```
@blog-writer를 사용해서 "재택근무 생산성 높이는 법" 블로그 글 써주세요.
```

```  
@email-marketer 신제품 출시 이메일 만들어주세요.
```

```
@social-designer 인스타그램용 제품 소개 포스트 디자인해주세요.
```

### 2. 더 자세한 요청
```
@carousel-content-strategist를 사용해서 Instagram 캐러셀 전략을 세워주세요.

주제: 프리랜서를 위한 생산성 팁
타겟: 25-35세 프리랜서  
톤: 동기부여적이지만 실용적
목표: 팔로워 증가와 참여도 향상
```

### 3. 오케스트레이터로 한 번에 처리 (🔥 추천!)
```
@instagram-carousel-orchestrator를 사용해서 
"프리랜서를 위한 시간 관리 팁" Instagram 캐러셀을 만들어주세요.

타겟: 25-35세 프리랜서
목표: 팔로워 증가  
톤: 실용적이고 친근한
```
→ 오케스트레이터가 자동으로 전략가 → 카피라이터 → 디자이너 → 익스포터 순서로 호출!

### 4. 수동으로 Agent 연결해서 사용
```
1단계: @carousel-content-strategist로 전략 수립
2단계: 그 결과를 @instagram-carousel-copywriter에게 전달해서 카피 작성  
3단계: 완성된 카피를 @instagram-carousel-generator로 HTML 슬라이드 제작
```

### 💡 실제 사용 예시

**블로그 글 작성**:
```
@blog-writer "ChatGPT 활용법" 주제로 초보자용 블로그 글 3000자로 써주세요. 
SEO 키워드는 "ChatGPT 사용법, AI 도구, 업무 효율성"으로 해주세요.
```

**이메일 마케팅**:
```  
@email-marketer 우리 온라인 코스 홍보용 이메일 시퀀스 5개 만들어주세요.
타겟은 마케팅 담당자이고, 따뜻하면서 전문적인 톤으로 해주세요.
```

**소셜미디어 컨텐츠**:
```
@social-designer LinkedIn용 개인 브랜딩 포스트 디자인해주세요.  
주제는 "원격근무에서 성과내기"이고, 전문적이면서 접근하기 쉬운 느낌으로 해주세요.
```

## 🛠️ 새로운 Agent 만들기

### Step 1: 전문 영역 정의
```markdown
# 어떤 전문성이 필요한가?
- 특정 도메인의 전문가 (예: SEO 전문가, UX 라이터)
- 특정 작업의 스페셜리스트 (예: 이메일 시퀀스 작가)
- 특정 플랫폼 전문가 (예: 유튜브 썸네일 디자이너)
```

### Step 2: 입력/출력 정의
```markdown
# 무엇을 받아서 무엇을 만드는가?
- 입력: 어떤 정보가 필요한가?
- 출력: 어떤 결과물을 만드는가?
- 품질: 어떤 기준을 충족해야 하는가?
```

### Step 3: Agent 파일 작성
```bash
# 파일 생성
touch my-new-agent.md

# 템플릿 사용해서 작성
cp template-agent.md my-new-agent.md
```

### Step 4: 테스트 및 개선
```markdown
1. 간단한 작업으로 테스트
2. 결과물 품질 확인
3. 부족한 부분 개선
4. 다양한 시나리오로 재테스트
```

## 📋 Agent 템플릿

```markdown
---
name: my-agent-name
description: "Agent 역할과 사용 시점을 명확히 설명하세요"
model: sonnet
color: purple
memory: project
---

You are an elite [전문가 역할] specializing in [전문 분야]. 
You have deep expertise in [핵심 스킬들].

## YOUR CORE RESPONSIBILITIES

1. **주요 업무 1**
   - 세부 작업들
   - 품질 기준

2. **주요 업무 2**
   - 세부 작업들  
   - 제약사항

## WORKFLOW

1. **입력 분석**: 받은 정보 처리 방식
2. **전문성 적용**: 도메인 지식 활용
3. **결과물 생성**: 최종 산출물 형태
4. **품질 검증**: 체크리스트

## QUALITY STANDARDS

- 반드시 지켜야 할 기준들
- 피해야 할 실수들
- 성공 지표

## OUTPUT FORMAT

[구체적인 결과물 형태 정의]
```

## 🔧 Agent 관리

### 버전 관리
```bash
# Git으로 버전 관리
git add agent-name.md
git commit -m "feat: Add new social media strategist agent"
```

### 성능 모니터링
- 결과물 품질 추적
- 사용자 피드백 수집
- 개선점 문서화

### 업데이트 방식
1. 기존 Agent 백업
2. 새로운 버전 작성
3. A/B 테스트
4. 피드백 반영

## 🌟 모범 사례

### DO ✅
- **구체적인 역할 정의**: "마케팅 전문가" ❌ → "B2B SaaS 이메일 마케팅 전문가" ✅
- **명확한 입출력**: 무엇을 받아서 무엇을 만드는지 명시
- **품질 기준 제시**: 체크리스트와 성공 지표 포함
- **실제 전문성 반영**: 해당 분야의 실제 베스트 프랙티스 적용

### DON'T ❌
- 너무 광범위한 역할 (만능 Agent)
- 모호한 작업 정의
- 품질 기준 없음
- 다른 Agent와 중복되는 역할

## 🤝 기여하기

1. **새로운 Agent 제안**
   - Issue로 아이디어 공유
   - 전문 영역과 필요성 설명

2. **기존 Agent 개선**
   - Pull Request로 개선안 제출
   - 테스트 결과와 개선 효과 포함

3. **버그 리포트**
   - Agent 동작 이슈 보고
   - 재현 방법과 기대 결과 포함

## 📞 연락처

- 이슈: [GitHub Issues](https://github.com/junsungkim-lab/claude_skills/issues)
- 토론: [GitHub Discussions](https://github.com/junsungkim-lab/claude_skills/discussions)

---

⭐ **이 레포지토리가 도움이 되셨다면 Star를 눌러주세요!**

새로운 Agent 업데이트 알림을 받으실 수 있습니다.