# project-to-blog

기존 소프트웨어 프로젝트를 분석해 한국어 기술 블로그(Mazora) 연재물로 재구성하는 Claude Code Skill.

소스·README·문서·Git 이력을 교차 검증한 근거만 사용하며, 설계 이유나 공개 범위가 불분명하면 **질문을 모아 사용자 답변을 받은 뒤** 진행한다.

## 특징

- ML, LLM/RAG, 업무 자동화, ETL, Web/SaaS, Vision/OCR 등 복수 유형 조합 분석
- 모든 공개 주장에 증거 등급 부여 (`A` 직접 확인 / `B` 일부 확인 / `U` 사용자 진술 / `C` 미확인)
- 원본 프로젝트 **읽기 전용**. 커밋·푸시·배포·게시 금지, 원고는 별도 작업 경로에 저장
- 내부 약점·민감정보 비공개, 사실과 다른 과장도 금지

## 구성

| 파일 | 내용 |
|------|------|
| `SKILL.md` | 스킬 본체 (절차·원칙) |
| `references/analysis-profiles.md` | 프로젝트 유형별 분석 체크리스트 |
| `references/editorial-policy.md` | 편집·공개 정책 |
| `references/human-review.md` | 사용자 확인 질문 작성법 |
| `references/workspace-templates.md` | 작업 산출물 템플릿 |
| `INSTALL.md` | 설치 가이드 (Windows PowerShell) |

## 설치

전역 설치 (모든 프로젝트):

```powershell
$dest = Join-Path $HOME '.claude\skills\project-to-blog'
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item SKILL.md, references -Destination $dest -Recurse -Force
```

프로젝트 한정 설치와 ZIP 설치는 [INSTALL.md](INSTALL.md) 참조. 설치 후 Claude Code 세션을 재시작한다.

## 사용

Claude Code 대화 입력창에서 실행한다.

```text
/project-to-blog <프로젝트 경로> blog=<Mazora 저장소> output=<작업 경로> mode=all
```

| 인자 | 설명 |
|------|------|
| 프로젝트 경로 | 분석 대상 (필수, 열린 저장소가 대상이면 `.`) |
| `blog=` | Mazora Astro 저장소 (선택, 형식 분석용) |
| `output=` | 비공개 작업 폴더 (선택, 원본 Git 저장소 밖) |
| `mode=` | `all`(기본) / `analyze` / `draft` / `review` |

다른 저장소를 함께 읽으려면 `claude --add-dir <경로>`로 시작한다.

## 산출물

작업 폴더에 생성: `PROJECT_ANALYSIS.md`, `EVIDENCE_MAP.md`, `DECISIONS.md`, `PUBLICATION_REVIEW.md`, 이후 연재 기획과 초안.

## 주의

분석 결과에 내부 구현 정보가 포함될 수 있으므로 작업 폴더를 공개 Git 저장소나 웹 공개 경로에 두지 않는다.
