# project-to-blog — Claude Code 설치 가이드 (Windows PowerShell)

## 구성

압축 파일 안의 `project-to-blog/` 폴더 전체가 하나의 Claude Code Skill입니다. 폴더 이름과 `SKILL.md` 이름을 유지하십시오.

## 방법 A — 모든 프로젝트에서 사용 (권장)

1. 다운로드한 ZIP 파일을 예컨대 `Downloads` 폴더에 저장합니다.
2. PowerShell을 열고 다음을 실행합니다.

```powershell
$zip = Join-Path $HOME 'Downloads\project-to-blog.zip'
$dest = Join-Path $HOME '.claude\skills'
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Expand-Archive -LiteralPath $zip -DestinationPath $dest -Force
Test-Path (Join-Path $dest 'project-to-blog\SKILL.md')
```

`True`가 나오면 설치 파일이 있습니다. 기존 `project-to-blog` 폴더가 있다면 덮어쓰기 전에 백업하세요.

## 방법 B — 특정 프로젝트에서만 사용

```powershell
$zip = Join-Path $HOME 'Downloads\project-to-blog.zip'
$dest = 'D:\workspace\your-project\.claude\skills'
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Expand-Archive -LiteralPath $zip -DestinationPath $dest -Force
```

※ `D:\workspace\your-project`는 실제 프로젝트 경로로 변경합니다.

## 다운로드한 ZIP이 최상위 폴더를 포함한 경우

본 ZIP은 `project-to-blog/`와 최상위 `INSTALL.md`를 포함합니다. `INSTALL.md`는 Skill 폴더 옆에 풀려도 정상 작동에 영향이 없습니다.

## 사용법

1. VS Code 터미널 또는 PowerShell에서 원본 프로젝트로 이동합니다.
2. Claude Code 세션을 시작합니다. 두 저장소를 함께 참조해야 하면 `--add-dir`를 사용합니다.

```powershell
cd 'D:\work\my-project'
claude --add-dir 'D:\work\mazora'
```

3. Claude Code **대화 입력창에서** 다음처럼 실행합니다 (PowerShell에 입력하는 명령이 아닙니다).

```text
/project-to-blog . blog=D:\work\mazora output=D:\blog-workspace mode=all
```

- `mode=analyze`: 분석 보고서와 사용자 확인 질문 작성
- `mode=all`: 분석·질문·시리즈 기획·초안 검증까지. 중요한 질문이 나오면 **답을 받고 계속** 진행
- `mode=draft`: 기존 분석 및 사용자 결정 자료를 바탕으로 초안 생성
- `mode=review`: 기존 초안의 사실관계·공개 위험·문체 검토

프로젝트 경로에 공백이 있으면 따옴표로 감싸 전달하세요. 인자는 Claude에게 전달되는 자유 텍스트이며, 실제 셸 옵션 파서가 아닙니다.

## 정상 동작 확인

- Claude Code의 `/` 목록에서 `project-to-blog`를 찾습니다.
- `/project-to-blog . mode=analyze`로 테스트합니다.
- 결과가 `PROJECT_ANALYSIS.md`, `EVIDENCE_MAP.md`, `DECISIONS.md` 등에 기록되는지 확인합니다.
- 중요한 기술 선택·공개 범위가 불명확하면 **Q-ID를 가진 묶음 질문을 제시하고 답을 기다리는지** 확인합니다.
- 사용자 지시 없이는 실제 블로그 콘텐츠 경로, 원본 코드, 커밋·푸시·배포를 변경하지 않는지 확인합니다.

## 유의사항

- 다른 폴더의 프로젝트/블로그를 읽으려면 해당 경로에 대한 Claude Code 접근 권한이 필요합니다.
- 스킬을 추가했는데 목록에 없으면 Claude Code 세션을 재시작한 다음 경로·파일 이름·YAML frontmatter를 확인하세요.
- 분석 결과에는 회사 프로젝트의 내부 구현 관련 정보가 포함될 수 있으므로 `blog-workspace`는 공개 Git 저장소나 웹 서버의 공개 경로 밖에 두세요.

공식 문서: https://code.claude.com/docs/en/skills
