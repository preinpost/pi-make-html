# pi-make-html

에디토리얼 톤의 **HTML 보고서/리포트**를 일관된 디자인 규칙으로 생성하는 [pi](https://pi.dev) 스킬 패키지.

커버 → 사이드 네비게이션 → 섹션 → 콜아웃 → 푸터로 이어지는 출판물 톤의 단일 HTML 문서를, 정의된 컬러 토큰·타입 스케일·레이아웃 토큰에 맞춰 만들어 준다.

## 구성

```
skills/make-html/
├── SKILL.md                       # 스킬 진입점 (적용 조건 + 사용 방법)
├── references/design-system.md    # 전체 디자인 규칙 (토큰·타이포·컴포넌트)
└── assets/example-service-prd.html # 완성 산출물 예시
```

## 설치

```bash
# 로컬 경로로 설치 (사용자 설정)
pi install ~/dev/pi-make-html

# 프로젝트 설정에 설치
pi install -l ~/dev/pi-make-html

# 설치 없이 한 번만 사용
pi -e ~/dev/pi-make-html
```

git/npm 배포 후에는 다음 형태도 가능하다.

```bash
pi install git:github.com/<user>/pi-make-html
```

## 사용

설치하면 `make-html` 스킬이 로드된다. 사용자가 HTML 보고서 생성을 **명시적으로** 요청할 때만 적용된다.

- "이 자료 HTML 보고서로 만들어줘"
- "리포트 형식으로 정리해줘"
- "이 디자인시스템으로 만들어줘"

강제 실행:

```bash
/skill:make-html
```

단순 질문·요약·읽기·표만 필요한 경우에는 적용되지 않는다.

## 라이선스

MIT
