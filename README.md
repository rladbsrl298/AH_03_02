# 🩺 KiniQ — 만성콩팥병 환자 생활습관 관리 서비스

> 환자가 일상에서 실천 가능한 챌린지를 함께 수행하며 작은 성공을 누적시켜 행동 변화를 유도하는 헬스케어 웹 서비스.

<p align="left">
  <a href="https://healthypeople.kr"><img src="https://img.shields.io/badge/Live-healthypeople.kr-0075de?style=for-the-badge&logo=safari&logoColor=white" alt="Live Demo"></a>
  <img src="https://img.shields.io/badge/HTTPS-Let's%20Encrypt-success?style=for-the-badge&logo=letsencrypt&logoColor=white" alt="HTTPS">
  <img src="https://img.shields.io/badge/CI/CD-GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="CI/CD">
</p>

**🌐 Live Demo**: https://healthypeople.kr · **데모 계정**: `b-male@healthypeople.kr` / `Demo1234!`

---

## 📌 한 줄 요약

> **30일 / 180 commits / 84,000줄 — 풀스택 + DevOps + 게이미피케이션을 단독 구현한 헬스케어 서비스**

부트캠프 팀 프로젝트(4인 + 멘토)에서 **백엔드·프론트엔드·OCR·게이미피케이션·관리자 페이지·인프라(CI/CD·HTTPS)·접근성**을 단독으로 구축. 의료 도메인 안전 가드(진단자/비진단자 분기·출처 표시·정서 가드)를 코드 한 줄까지 일관 적용.

---

## 🎯 본인(김윤기) 핵심 기여

### 📊 수치로 보는 임팩트

| 지표 | 값 |
|---|---|
| 총 commits | **180개** (팀 최다, 다른 팀원 평균의 4.5배) |
| 작업 기간 | 2026-05-19 ~ 2026-06-17 (30일) |
| 코드 추가 | **+84,051 lines** |
| 코드 삭제 | -4,248 lines |
| 머지된 PR | **12+ 건** |
| 단독 구현 도메인 | **7개** (OCR·게이미피케이션·관리자·인프라·접근성·인증·캐릭터) |

### 🏆 단독 구현 영역

#### 1. 🔐 인증·보안 시스템 (REQ-AUTH 전체)
- 회원가입·로그인·JWT (Access 15분 / Refresh 7일 Rotation)
- 비밀번호 5회 실패 30분 잠금 (REQ-AUTH-007)
- 회원 탈퇴 시 민감의료 즉시 파기 (REQ-SEC-008)
- 이메일 인증 풀스택 (REQ-AUTH-003)
- 이메일 중복 확인 (PR #126)
- Rate Limit (slowapi) · Gmail SMTP / Resend 자동 강등

#### 2. 📷 OCR 시스템 (검진지 자동 매핑) ⭐
- **`app/services/ocr.py` 885줄 단독 구현**
- CLOVA OCR V2 + **토큰 좌표 기반 페어 매칭 알고리즘 직접 구현**
- 다중 페이지 PDF 자동 분할 + 부분 성공 처리
- **표 형식 검진지 정확도 4단계 알고리즘 강화** (옵션 A·B·C·D)
- HDL/LDL 분리 셀 전용 룰 (가장 복잡한 트러블슈팅)
- 자동 매핑 10종 (혈압·혈당·콜레스테롤·BMI 등)

#### 3. 🎮 게이미피케이션 시스템 ⭐
- **DB 모델 5종** (Point · Transaction · Egg · Skin · EquippedItem)
- **API 9개 + 백엔드 단위 테스트 28건**
- 알 부화 3단계 진화 (10·40·100건, 보너스 +100·+400·+750 pt)
- 스트릭 보호권·충전 모드(쉬어가기 페널티 없음)·Goal Gradient 알림
- 체크인 결과 모달 (컨페티·럭키·스트릭·부화 강조)
- 5종 캐릭터 × 3진화 = 15장 + 알 (Gemini AI 일러스트 33장)

#### 4. ☁️ 인프라·CI/CD·HTTPS ⭐
- **GitHub Actions 3 jobs (`.github/workflows/deploy.yml` 179줄)**
- Docker Compose 7-container (`docker-compose.prod.yml` 156줄)
- AWS EC2 (Ubuntu 24.04 · t3.large · Elastic IP)
- **Let's Encrypt HTTPS** (certbot 48h 자동 갱신)
- nginx TLS 1.2/1.3 · HSTS 1년 · HTTP→HTTPS 301
- **부하 테스트 (Locust) — GET API 평균 5~10ms, 실패율 0%**

#### 5. 🛡 관리자 페이지 ⭐
- 5개 페이지 풀스택 (통계·사용자·챌린지·세이프티·로그)
- **PHI 마스킹** (이메일·이름·전화 · CLAUDE.md §5)
- **위험 액션 사유 강제 입력** (탈퇴·잠금·임퍼소네이션)
- **세이프티 이벤트 자동 감지** (혈압≥180·혈당≥400·eGFR<15)
- N+1 픽스 + 사용자 목록 성능 최적화

#### 6. 📊 대시보드·시뮬레이션 (REQ-DASH)
- 대시보드 1~8 단계 (워터마크·G1~G5·잔디 히트맵·라디알·주간 달성)
- What-if eGFR 시뮬레이션 풀스택 (REQ-DASH-003)
- 진단자/비진단자 분기 가드 (PR #103)
- 임신 안전 안내 (REQ-DASH-005)

#### 7. ♿ 접근성·UX (a11y)
- **돋보기 모드** (PR #132) — WCAG 1.4.4 충족 수준
- 본문 16→24px (+50%)
- 뒤로가기 버튼 9페이지 추가
- Notion 톤 디자인 시스템 전면 적용 (38페이지)
- 회원가입 약관 아코디언 + 입력 UX 보강

---

## 🐛 트러블슈팅 핵심 5건

### 1. 마이그레이션 race condition
**증상**: 3 uvicorn 워커가 동시에 `aerich upgrade` → `pg_type_typname_nsp_index` 충돌
**해결**: 메인 컨테이너 기동 전 `docker compose run --rm fastapi aerich upgrade`로 외부 1회 실행

### 2. OCR HDL/LDL 매핑 오류 (가장 복잡)
**증상**: 표 형식 검진지에서 `총콜레스테롤`이 `HDL/LDL` 값을 가로채는 오탐 다수
**해결 4단계**:
- **옵션 A**: 일반 fallback 모호 케이스 차단
- **옵션 B**: 토큰 좌표 기반 페어 매칭 (boundingPoly 활용)
- **옵션 C**: HDL/LDL 분리 셀 토큰 결합 ("고밀도/저밀도" + "mg/dL")
- **옵션 D**: HDL 두 줄 셀 전용 룰 + total 가로채기 차단 → **최종 해결**

### 3. RAG 벡터 차원 불일치
**증상**: 추론 시 `text-embedding-3-large(3072d)` vs `text-embedding-3-small(1536d)` 불일치 → 검색 실패
**해결**: 환경변수 통일 (`OPENAI_EMBEDDING_MODEL=text-embedding-3-large`로 단일화)

### 4. CI/CD scp-action multi-line 버그
**증상**: `tar empty archive` 에러 (compose + nginx 한 step에서 두 파일 SCP 실패)
**해결**: scp step을 2개로 분리 (compose 1개 · nginx 1개) → multi-line yaml 우회

### 5. nginx upstream DNS 캐시
**증상**: 컨테이너 재배포 후 nginx가 옛 FastAPI IP로 호출 → 502 에러
**해결**: deploy 스크립트에 `docker compose restart nginx` 추가하여 DNS 캐시 갱신

---

## 🏗 시스템 아키텍처

```
                     🌐 healthypeople.kr (HTTPS)
                              │
                       ┌──────┴──────┐
                       │   Nginx     │ ← Let's Encrypt
                       │ Reverse     │   (48h 자동 갱신)
                       └──┬───────┬──┘
                /static    │       │  /api/*
                          ▼       ▼
                  React SPA   FastAPI ─── PostgreSQL 16
                               (uvicorn)
                                 │
                                 ├── Redis Stream ─── AI Worker
                                 │                    (RAG · CKD 예측)
                                 └── Qdrant (1만+ 청크)
```

### 컨테이너 구성 (7-container)
| 컨테이너 | 역할 |
|---|---|
| `nginx` | 리버스 프록시 + HTTPS |
| `certbot` | Let's Encrypt 자동 갱신 |
| `postgres` | DB |
| `redis` | 메시지 브로커 |
| `qdrant` | 벡터 DB (RAG) |
| `fastapi` | API 서버 (Producer) |
| `ai-worker` | ML 추론 + RAG 챗봇 (Consumer) |

---

## 🛠 기술 스택

### Backend
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)
![Python 3.13](https://img.shields.io/badge/Python-3.13-3776AB?style=flat&logo=python&logoColor=white)
![PostgreSQL 16](https://img.shields.io/badge/PostgreSQL-16-336791?style=flat&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-Stream-DC382D?style=flat&logo=redis&logoColor=white)
![Qdrant](https://img.shields.io/badge/Qdrant-Vector%20DB-DC244C?style=flat)

- FastAPI (ASGI/uvicorn, uv 패키지 관리)
- Tortoise ORM + aerich (마이그레이션)
- Redis Stream (Producer/Consumer 패턴)
- Qdrant (RAG 의료 문헌 벡터 DB)

### AI / ML
![LightGBM](https://img.shields.io/badge/LightGBM-ROC--AUC%200.902-success?style=flat)
![OpenAI](https://img.shields.io/badge/OpenAI-Embedding%20+%20GPT-412991?style=flat&logo=openai&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-Self--RAG-1C3C3C?style=flat)
![CLOVA OCR](https://img.shields.io/badge/CLOVA-OCR-03C75A?style=flat)

- LightGBM CKD 위험 예측 (Test ROC-AUC **0.902**)
- OpenAI text-embedding-3-large + gpt-4o-mini
- LangGraph Self-RAG (관련성 + 환각 검증 재시도)
- Naver CLOVA OCR + 좌표 기반 페어 매칭 (직접 구현)

### Frontend
![React](https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-6-646CFF?style=flat&logo=vite&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-Notion%20Tone-06B6D4?style=flat&logo=tailwindcss&logoColor=white)

- React 19 + Vite 6 + TypeScript
- Tailwind CSS (Notion 톤 디자인 시스템)
- TanStack Query (서버 상태 캐싱)
- Recharts (eGFR 추세 차트)

### Infra
![AWS EC2](https://img.shields.io/badge/AWS%20EC2-Ubuntu%2024.04-FF9900?style=flat&logo=amazonec2&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-Let's%20Encrypt-009639?style=flat&logo=nginx&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?style=flat&logo=githubactions&logoColor=white)

- AWS EC2 (t3.large · Elastic IP)
- Docker Compose 7-container
- Nginx + Let's Encrypt HTTPS
- GitHub Actions CI/CD (PR push → 10분 자동 배포)

---

## 📊 평가 지표 (부트캠프 평가 기준 충족)

| 평가 | 기준 | 결과 |
|---|---|---|
| **5-1** | API P95 < 3,000ms | ✅ GET API 평균 **5~10ms** (목표의 0.3%) |
| **5-4** | JWT 인증 | ✅ Access 15분 / Refresh 7일 Rotation |
| **2-1** | AI/RAG 핵심 스택 ADR | ✅ ADR 4건 작성 |
| **3-1** | CKD 모델 평가 | ✅ ROC-AUC **0.902** / F1 0.266 / Recall 0.840 |
| **3-3** | 추론 결정론 | ✅ 학습 시드 명시 + 재현성 검증 |
| **필수 1·2·3** | 예측·대시보드·챌린지 | ✅ 모두 충족 |
| **선택 가산** | LLM·OCR·알림 | ✅ 모두 충족 |

---

## 🎯 차별점 5가지

| # | 차별점 |
|---|---|
| 1 | 🩺 **진단자/비진단자 분기** — 위험 예측·시뮬레이션·리포트 차별 노출 (defense in depth) |
| 2 | 🧠 **RAG 의료 안전 가드** — 1만+ 청크 (KDIGO·KSN) · Self-RAG 환각 검증 · 출처 표시 |
| 3 | 📷 **OCR 자동 매핑** — 검진지 사진 → 10종 수치 → 즉시 eGFR 계산 |
| 4 | 👁 **고령 친화 UX** — 돋보기 모드 +50% (WCAG 1.4.4) · 뒤로가기 9페이지 |
| 5 | 🌐 **단일 URL · HTTPS · 자동 배포** — healthypeople.kr (Let's Encrypt + CI/CD) |

---

## 🏃‍♂️ 실행 방법

### 사전 요구
- Docker Desktop
- `envs/.local.env` 설정 (`.env.example` 참고)

### 로컬 실행
```bash
# 1. 의존성 동기화
uv sync

# 2. 컨테이너 기동
docker compose up -d redis postgres qdrant

# 3. 마이그레이션
docker compose run --rm fastapi uv run aerich upgrade

# 4. 메인 서비스
docker compose up -d fastapi ai-worker nginx

# 5. 프론트엔드
cd frontend/ckd-care-app && npm install && npm run dev
```

브라우저: http://localhost:5173

---

## 📂 폴더 구조

```
.
├── app/                    # FastAPI 백엔드
│   ├── apis/v1/            # 라우터 (auth · health_check · gamification · ...)
│   ├── services/           # 비즈니스 로직 (ocr.py 885줄 · gamification · ...)
│   ├── models/             # Tortoise ORM 모델
│   ├── repositories/       # DB 조회
│   ├── core/               # config · middleware · validators
│   └── tests/              # pytest (게이미피케이션 28건 등)
│
├── ai_worker/              # AI 워커 (RAG · CKD 예측)
│   ├── rag/                # LangGraph Self-RAG
│   └── ckd/                # LightGBM 모델
│
├── frontend/ckd-care-app/  # React 19 + Vite 6 SPA
│   ├── src/pages/          # 38개 페이지
│   ├── src/components/     # 공통 컴포넌트
│   └── src/hooks/          # useLargeFont · useDiagnosed
│
├── infra/                  # 인프라
│   ├── docker/             # docker-compose.prod.yml
│   └── nginx/              # prod.conf (TLS · HSTS)
│
├── .github/workflows/      # CI/CD
│   └── deploy.yml          # 179줄 단독 구현
│
├── docs/                   # 문서
│   ├── 05-adr/             # ADR 4건 (평가 2-1)
│   ├── load-test/          # Locust 부하 테스트 결과
│   └── model-eval/         # CKD 모델 평가
│
└── scripts/                # 시드·평가·유틸
```

---

## 👤 About

**김윤기** · 백엔드 · 풀스택 · DevOps

- 📧 rladbsrl298@gmail.com
- 🌐 GitHub: [@rladbsrl298](https://github.com/rladbsrl298)
- 🌐 Live: [healthypeople.kr](https://healthypeople.kr)

---

## 📝 라이선스 & 면책

본 프로젝트는 학습 목적의 프로토타입입니다.
**임상적 의사결정 도구가 아니며, 일반적 생활습관 가이드 수준의 정보를 제공합니다.**

원본 팀 레포: [AI-HealthCare-03/AH_03_02](https://github.com/AI-HealthCare-03/AH_03_02)
