# 저장소 가이드라인

## 프로젝트 구조와 파일 구성

이 저장소는 애플리케이션 실행 코드가 아니라 리서치 자료와 Codex 스킬을 관리합니다.

- `리서치/[리서치 결과]_*.txt`: UTF-8로 저장된 기본 리서치 자료입니다. 읽기 전용 원본으로 취급합니다.
- `리서치/homepage-reference-analyzer/SKILL.md`: 스킬의 실행 조건과 전체 작업 절차입니다.
- `리서치/homepage-reference-analyzer/agents/openai.yaml`: 사용자에게 표시되는 스킬 이름과 설명입니다.
- `리서치/homepage-reference-analyzer/references/`: 추후 확정할 분류 기준과 결과 작성 형식을 보관합니다.
- 루트의 `.txt` 파일: 설계 메모와 명령어 규칙 초안입니다. 메모에 등장하는 예시 프로젝트명이나 파일명을 실제 입력 자료로 간주하지 않습니다.

분석 결과는 원본 리서치 자료와 섞지 말고, 저장 위치가 확정되면 별도의 출력 폴더에 생성합니다.

## 개발 및 검증 명령어

별도의 빌드 시스템이나 애플리케이션 패키지는 없습니다. 저장소 루트에서 PowerShell을 사용합니다.

```powershell
rg --files
```

현재 작업 폴더의 파일 목록을 빠르게 확인합니다.

```powershell
Get-Content -LiteralPath "리서치\homepage-reference-analyzer\SKILL.md" -Encoding UTF8
```

한글 인코딩이 깨지지 않는지 확인하면서 스킬 내용을 읽습니다.

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-creator\scripts\quick_validate.py" "리서치\homepage-reference-analyzer"
```

스킬 이름과 YAML 앞부분의 형식을 검사합니다. 실행하는 Python 환경에 `PyYAML`이 설치되어 있어야 합니다.

## 작성 방식과 이름 규칙

Markdown은 짧고 명확한 제목을 사용하고, 작업 지시는 실행형 문장으로 작성합니다. `SKILL.md`는 핵심 절차만 간결하게 유지합니다. 확정된 세부 기준은 중복해서 작성하지 말고 `references/`에 분리합니다.

스킬 폴더 이름은 `homepage-reference-analyzer`처럼 영문 소문자와 하이픈을 사용합니다. `SKILL.md`의 YAML 앞부분에는 `name`과 `description`만 작성합니다.

Markdown, YAML과 리서치 TXT 파일은 UTF-8로 저장합니다. 기본 자료 파일명에는 `[리서치 결과]`를 포함합니다. PowerShell에서는 대괄호가 와일드카드로 처리될 수 있으므로 `-LiteralPath`를 사용합니다.

## 시험 및 검증 지침

자동 테스트 시스템은 아직 없습니다. 스킬 배포 전에 다음 항목을 확인합니다.

1. 공식 스킬 검사 도구를 실행합니다.
2. `TODO` 문구가 남아 있지 않은지 확인합니다.
3. 홈페이지 자료 3~5개로 시험합니다.
4. 출처 연결, 중복 통합, UTF-8 결과와 파일당 홈페이지 100개 제한을 검사합니다.
5. 원본 리서치 파일이 수정되지 않았는지 확인합니다.

## 커밋 및 검토 지침

현재 작업 폴더에는 확인 가능한 Git 기록이 없으므로 기존 커밋 규칙을 추정하지 않습니다. `docs: 홈페이지 분석 절차 보완`처럼 변경 내용을 현재형으로 간결하게 작성합니다.

변경 사항을 검토할 때는 수정한 규칙, 영향받은 파일과 수행한 검증을 기록합니다. 스킬 동작이 달라졌다면 작은 결과 예시를 함께 제공합니다.

## 자료 보호

원본 리서치와 기존 결과를 덮어쓰지 않습니다. 중복 홈페이지를 통합하더라도 발견된 모든 출처를 보존합니다. 확인할 수 없거나 근거가 부족한 내용은 `추가 조사 필요`로 표시합니다.
