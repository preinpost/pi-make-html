# HTML Design System

보고서/리포트 HTML을 만들 때 따르는 디자인 규칙.

---

## 사용 조건 (When to Apply) — **READ FIRST**

> 이 디자인 시스템은 **사용자가 명시적으로 HTML 보고서/리포트 생성을 요청했을 때만** 적용한다. 그 외의 경우엔 절대 자동 적용하지 않는다.

### ✅ 적용하는 경우 (사용자가 명시적으로 요청)
- "HTML 보고서로 만들어줘"
- "리포트 형식으로", "이 디자인시스템으로", "디자인시스템으로"
- "리포트/보고서 HTML 만들어줘"
- "이 PDF/자료를 보고서로 변환해줘"
- 이전 대화에서 같은 보고서를 이어 작성 중인 경우

### ❌ 적용하지 않는 경우 (요청이 없거나 다른 작업)
- **단순 질문·답변** — "이게 뭐야?", "왜 이렇게 돼?", "어떻게 해?"
- **요약·정리·노트** — "정리해줘", "요약해줘" (별도 형식 지정 없음)
- **읽기 전용** — "이 PDF 읽어줘", "내용 알려줘", "확인해줘"
- **데이터/표만 필요** — 마크다운 표·JSON·코드블록으로 충분한 경우
- **코드 리뷰·디버깅·설계 문의** — 이 디자인시스템과 무관
- **다른 형식이 명시됨** — PPT, DOCX, 마크다운, 단일 페이지 웹 등

### 판단 규칙
1. 사용자가 "HTML", "보고서", "리포트", "NDS", "이 디자인" 중 하나를 명시했는가? → **NO면 적용 금지**.
2. 관련 자료가 첨부되었더라도, 요청이 "읽어줘/알려줘/정리해줘"면 **적용 금지**. 마크다운/평문으로 응답한다.
3. 애매하면 **물어본다**: "HTML 보고서로 만들까요, 아니면 텍스트로 정리할까요?"

---

## 0. 디자인 원칙 (Principles)

1. **에디토리얼 톤** — 마케팅 페이지가 아닌 출판물 톤. 그라데이션·그림자 최소화, 검정 잉크 + 라인 위주.
2. **타이포그래피 우선** — 컴포넌트보다 타입 스케일이 먼저. 모든 텍스트는 정의된 토큰을 사용.
3. **하나의 강조** — 페이지당 컬러 강조는 1~2회. 기본은 모두 `--ink` 계열.
4. **숫자는 또렷하게** — 모든 수치 텍스트에 `font-feature-settings: "tnum"`.
5. **공백을 두려워하지 않기** — `--section-py: 72px`, 마지막 섹션 ↔ 푸터는 160px.

---

## 1. 컬러 토큰 (Color Tokens)

### 1.1 브랜드
```css
--brand-black:  #191919;
--brand-white:  #ffffff;
--brand-blue:   #0F80F6;   /* 강조 / 데이터 하이라이트 */
--brand-red:    #EB453D;   /* 위험 / 차감 / 대외비 닷 */
--brand-green:  #01A058;   /* 긍정 추세 / 마진 */
--brand-orange: #FF9000;
--brand-yellow: #FCF683;
--brand-brown:  #DAC0A9;
--brand-gray:   #DCDCDC;
```

### 1.2 잉크 (텍스트 위계)
```css
--ink:   #191919;   /* 본문 강조 / 헤딩 */
--ink-2: #2e2e2e;   /* 본문 기본 */
--ink-3: #545454;   /* 보조 본문 / 설명 */
--ink-4: #767676;   /* 캡션 / 라벨 */
--ink-5: #a1a1a1;   /* 구분점 / 비활성 */
--ink-6: #c8c8c8;
```

### 1.3 표면 / 라인
```css
--surface:    #ffffff;
--surface-1:  #f7f7f7;   /* 콜아웃 배경 */
--surface-2:  #efefef;   /* 차트 트랙 */

--line:        #191919;  /* 강한 구분선 (테이블 상하단) */
--line-soft:   #e3e3e3;
--line-softer: #ededed;
```

### 1.4 시멘틱
```css
--accent:  #0F80F6;   /* = brand-blue */
--danger:  #EB453D;   /* = brand-red  */
--success: #01A058;   /* = brand-green */
```

---

## 2. 타이포그래피 (Typography)

### 2.1 폰트 패밀리

> **모든 타이포그래피는 Pretendard 단일.** 본문·헤딩·라벨·메타·숫자 — 어느 컨텍스트든 동일한 폰트 패밀리를 쓴다. 다른 sans-serif/serif/monospace 패밀리(Inter, Noto Sans, JetBrains Mono 등)는 사용하지 않는다.

```css
--font-sans:    "Pretendard", sans-serif;
--font-mono:    "Pretendard", sans-serif;   /* mono 슬롯도 Pretendard — 한·영이 섞여도 행간·높이 안정 */
--font-display: "Pretendard", sans-serif;
```

CDN 로드:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css" />
```

#### 왜 Pretendard 하나만 쓰는가
- **한·영 혼용 시 행간·높이가 깨지지 않음** — 영문 폰트(Inter 등)에 한글 fallback이 따로 들어가면 라인 간격이 어긋남.
- 숫자 등폭 정렬이 필요할 땐 폰트 교체가 아닌 `font-feature-settings: "tnum"`(또는 `class="tnum"`)으로 처리.
- 한 폰트 family로 통일하면 토큰 단순화 + 로딩 비용도 작아짐(weight만 다르게).

#### Weight 사용
| 용도 | weight |
|---|---|
| 본문(`<body>`) | 500 |
| 보조 본문 / 라벨 | 500 ~ 600 |
| 모노/캡션·라벨 | 600 |
| 헤딩(H1~H4)·강조(strong) | 700 |
| 디스플레이(커버 타이틀 등) | 700 |

### 2.2 타입 스케일 (~1.27× 모듈러)

**규칙: 가장 작은 폰트 사이즈는 12px. 그 이하 금지.**

| 토큰 | 크기 | 용도 |
|---|---|---|
| `--fs-display-1` | **56px** | 커버 타이틀 / KPI 큰 수치 |
| `--fs-display-2` | **40px** | TOC 섹션 타이틀 |
| `--fs-h1`        | **48px** | **PART(그룹) 헤더** — 여러 섹션을 묶는 상위 분할 |
| `--fs-h2`        | **40px** | **섹션 H2** — 본문 시작 헤딩 (bold) |
| `--fs-h3`        | **20px** | 섹션 소제목 / 카드·컴포넌트 안의 헤딩 |
| `--fs-h4`        | **15px** | 보조 라벨 헤딩 (표 위 제목엔 사용 안 함 — H3 통일) |
| `--fs-lede`      | **17px** | 섹션 도입 문장(리드) |
| `--fs-body`      | **15px** | 본문 |
| `--fs-body-sm`   | **13px** | 보조 본문 / TOC 항목 / 푸터 제목 |
| `--fs-caption`   | **12px** | 캡션 |
| `--fs-micro`     | **12px** | 라벨 / 모노 메타 |
| `--fs-micro-xs`  | **12px** | 최소 사이즈 (12px 미만 금지) |

#### 헤딩 위계 — 라인과 마진 규칙 (중요)

> **선(divider)은 H1·H2만 가진다. H3·H4는 절대 라인을 가지지 않는다.**
> **마진은 위계에 따라 줄어든다: H1(최대) > H2 > H3 > H4(최소).** H4도 본문에서 명확히 분리되도록 충분한 마진은 가진다.

| 헤딩 | 크기 | 라인 | margin-top |
|---|---|---|---|
| **H1 (PART 헤더)** | **48px** / weight 700 | **6px solid 상단** (가장 굵음) | **120px** (가장 큼) — 새 챕터급 분할 |
| **H2 (섹션)** | **40px** / weight 700 | **3px solid 상단** (`.section-tag` 또는 동등) | section padding 72px |
| **H3 (소제목)** | 20px / weight 700 | **선 없음** | 56px |
| **H4 (작은 라벨)** | 15px / weight 700 | **선 없음** | 36px |

표 위 헤딩이 H3였다면 라인은 자동으로 빠진다 (디자인시스템 규칙). 만약 라인이 있던 컴포넌트(`.block-head` 등)였다면 라인을 제거한다.

### 2.3 라인 하이트 토큰
```css
--lh-tight:  1.15;   /* 디스플레이 */
--lh-snug:   1.25;   /* 헤딩 */
--lh-normal: 1.4;
--lh-loose:  1.7;    /* 본문 / lede */
```

### 2.4 자간 (Letter-spacing) — 한글에 맞춘 보수적 자간 정책

> **본문 영역의 헤딩(H2~H4)·소제목·번호 prefix·작은 라벨류는 자간 0으로 통일.** 한글 텍스트는 자간을 음수/양수로 조정하면 오히려 가독성이 떨어진다. 영문 mono uppercase 라벨에 양수 자간(스페이싱)을 주는 디자인 컨벤션도 한글이 함께 등장하면 어색하게 늘어진다.
>
> 양수 자간은 **커버·푸터의 chip/eyebrow** 같은 의도된 영문 영역에만 남긴다.

| 영역 | letter-spacing |
|---|---|
| Display 1 (커버 타이틀, 56px) | `-0.04em` |
| Display 2 (큰 디스플레이, 40px) | `-0.035em` |
| H1 (PART 헤더, 48px) | `0` (또는 `-0.02em` 이내) |
| H2 (섹션, 40px) | **`0`** |
| H3 / H4 (소제목 · 표 라벨) | **`0`** |
| `.num-prefix` (섹션 번호) | **`0`** |
| 본문 라벨류 (`.kpi-label`, `.metric-label`, `.block-head .meta`, `.ph-label`, `.step-num`, `.bar-legend` 등) | **`0`** |
| lede / body | `-0.005em` (한글 보정) |
| **커버·푸터의 영문 chip/eyebrow** (`.cover-eyebrow`, `.cover-confidential`, `.cover-meta-label`, `.footer-confidential`) | `+0.14~0.18em` (편집 자산 컨텍스트, 보존) |

#### 적용 원칙
- 본문 헤딩과 라벨에는 자간을 두지 않는다 — 한글 보고서의 톤을 유지.
- 양수 자간은 "표지/푸터의 영문 메타 chip" 정도에만 한정. 본문 mono 라벨에 무분별하게 양수 자간을 주지 않는다.
- 음수 자간은 36px 이상 큰 디스플레이 텍스트에서만 한글 보정용으로 사용 (`-0.025em` ~ `-0.04em`).

### 2.5 본문(`<body>`) 기본
```css
font-family: var(--font-sans);
font-size:   var(--fs-body);     /* 15px */
line-height: var(--lh-loose);    /* 1.7  */
font-weight: 500;
color:       var(--ink-2);
font-feature-settings: "ss01", "cv11", "tnum";
```

---

## 3. 한국어 표기 규칙 (Korean Writing Rules)

### 3.1 단어 단위 줄바꿈 (필수)
한글이 문장 중간에서 음절 단위로 잘려 어색하게 끊기는 걸 방지.

```css
body {
  word-break: keep-all;
  overflow-wrap: break-word;
}
```

### 3.2 헤딩 표기
- 헤딩은 명사형 (예: "수익 구조", "시장 기회")으로 통일. 의문형 헤딩(`~인가?`)은 사용하지 않음.

> 문체(종결어미·어투)는 부서·문서 성격에 따라 다르므로 디자인시스템에서 규정하지 않는다. 작성자 재량에 맡긴다.

### 3.3 리드(lede) — 섹션 인트로 (시스템 룰)
섹션 헤더 직하단의 도입 문장이다. 길이는 1~2문단, 폭은 본문(`--max`)을 따른다. 내용·문체는 작성자 재량.

> **한 줄 요약 + 본문 + 콜아웃의 3중 중복 금지** (컴포넌트 사용 규칙). 짧은 lede 아래 같은 내용의 본문 단락을 또 두면 반복된다. 인트로는 lede(1~2문단)로 통일하고, 콜아웃은 별도의 takeaway가 있을 때만 둔다(8장 참고).

```css
.lede {
  font-size: var(--fs-lede);
  line-height: var(--lh-loose);
  letter-spacing: -0.005em;
  color: var(--ink-3);
  font-weight: 500;
}
.lede + .lede { margin-top: 16px; }   /* 2문단 인트로일 때 단락 간격 */
.lede b { color: var(--ink); font-weight: 700; }   /* 핵심 어구 강조 */
```

### 3.4 숫자 / 영문 / 한글 혼용
- 영문·숫자에는 자동으로 Pretendard의 라틴 글리프가 사용됨. 별도 처리 불필요.
- 표/KPI 등 정렬이 중요한 곳: `font-feature-settings: "tnum"` 또는 `class="tnum"`.

---

## 4. 레이아웃 토큰 (Layout Tokens)

```css
--max:        800px;    /* 본문 영역 max-width (커버/섹션/푸터 공통) */
--narrow:      760px;   /* 좁은 본문 (긴 글 위주 섹션) */
--pad-x:        56px;   /* 좌우 패딩 (모바일 24px) */
--section-py:   72px;   /* 섹션 상하 패딩 (모바일 64px) */
```

- **모든 영역은 `--max`로 정렬**된다 (커버, 본문, TOC 섹션, 푸터). 가독성과 정렬 일관성의 근간.
- 본문 ↔ 사이드 네비게이션 간격: **40px** (1500px 이상에서 일정).
- 마지막 섹션 ↔ 푸터: `margin-top: 160px` (모바일 96px).

---

## 5. 커버(Cover) 구조

검은색 풀블리드 + 60vh 최소 높이 + `--max` 정렬.

```html
<section class="cover" id="cover">
  <div class="cover-inner">
    <div class="cover-head">
      <div class="cover-head-main">
        <div class="cover-eyebrow">Payment &amp; Coupon Market Analysis</div>
        <h1 class="cover-title">결제 및 쿠폰 시장 분석</h1>
        <p class="cover-summary">
          국내·미국·중국·일본 4개 시장의 페이 결제 환경을 거래액과 수익 구조 관점에서 비교 분석합니다.<br>
          결제 사업의 중장기 전략 수립을 위한 기초 자료입니다.
        </p>
      </div>
      <span class="cover-confidential">대외비</span>
    </div>
    <div class="cover-meta">
      <div class="cover-meta-item"><span class="cover-meta-label">Date</span>   <span class="cover-meta-value mono">-</span></div>
      <div class="cover-meta-item"><span class="cover-meta-label">Team</span>   <span class="cover-meta-value">-</span></div>
      <div class="cover-meta-item"><span class="cover-meta-label">Author</span> <span class="cover-meta-value">-</span></div>
    </div>
  </div>
</section>
```

### 5.1 구조 규칙
- 배경 — **subtle radial gradient** 레이어 위에 `--ink` (#191919) 베이스. 글자 `--surface` (#fff).
  ```css
  .cover {
    background:
      radial-gradient(ellipse 70% 55% at 25% 0%, rgba(15, 128, 246, 0.18), transparent 65%),   /* 좌상 cool spotlight */
      radial-gradient(ellipse 60% 50% at 90% 100%, rgba(235, 69, 61, 0.10), transparent 60%),  /* 우하 warm spotlight (더 약하게) */
      var(--ink);
    overflow: hidden;
  }
  ```
  - 미세한 깊이감 + 모던한 톤. 일반 시야에서는 거의 단색 검정으로 보이고, 가까이서 보면 좌상 brand-blue 18% / 우하 brand-red 10% 글로우.
  - 컨텐츠 가독성에는 영향 없음 (글자 위 배경 톤은 거의 검정 유지).
- `padding: 96px var(--pad-x)`, `min-height: 60vh`.
- 위·아래 영역(`cover-head` ↔ `cover-meta`) 사이에 `flex justify-content: space-between`로 균등 여백.
- **eyebrow**: 영문, 모노, micro size, `letter-spacing: 0.16em`, uppercase.
- **title**: `--fs-display-1` (56px), **line-height 1.25** (두 줄 한글 제목이 붙지 않도록 — `--lh-tight` 1.15보다 넉넉히), weight 700. 한국어 제목.
- **summary**: `--fs-lede` (17px), 흰색 72% alpha, 2~3줄로 간략히 (`<br>` 1~2회). **이것은 표지 전용 부제로, 섹션 lede(1~2문단)와는 다르다** — 표지에서는 길게 쓰지 않는다.
- **대외비**: 우상단 outline chip — 빨간 닷 + uppercase 모노. 본문 푸터의 chip과 시각적으로 동일.
- **meta**: **3컬럼 그리드** — `Date / Team / Author`. 라벨은 영문 uppercase 모노, 값은 한글/숫자.
- 그리드 CSS: `grid-template-columns: repeat(3, auto)`.

### 5.2 메타값 입력 규칙

> **메타 3종(Date · Team · Author)은 사용자(작성자)가 매 보고서마다 입력하는 값**이다. 시스템에 하드코딩된 디폴트가 없으며, 비어 있을 때는 **`-`** (en-dash 또는 hyphen)로 표기한다.

| 필드 | 형식 | 예시 | 미입력 시 |
|---|---|---|---|
| `Date`   | **`YYYY.MM.DD`** (mono) | `2025.05.04` | `-` |
| `Team`   | 한글 부서·파트명         | `UX 파트` | `-` |
| `Author` | 한글 이름               | `홍길동` | `-` |

#### Date 포맷 룰 — `YYYY.MM.DD` 통일
> **커버·푸터의 모든 날짜 표기는 `YYYY.MM.DD`(점 구분, 4자리 연도)로 통일.** 다른 포맷(`YY/MM/DD`, `YYYY-MM-DD`, `YYYY년 M월 D일` 등) 사용 금지.

| 항목 | 옳음 | 틀림 |
|---|---|---|
| 4자리 연도 | `2025.05.04` | `25.05.04` (세기 모호) |
| 구분자 | 점(`.`) | `-`, `/`, `년 월 일` |
| 0 패딩 | `2025.05.04` | `2025.5.4` |
| 폰트 | mono(`tnum`) — `class="mono"` 적용 | regular 본문 |

이유:
- 4자리 연도로 세기 모호 없음.
- 점 구분자는 한국 출판/공문서 관례. mono 폰트와 시각적으로 깔끔.
- 0 패딩으로 등폭 정렬 유지(여러 보고서·파일명에서 일관).
- 푸터의 짧은 한 줄 메타에서도 짧고 식별성 높음.

#### 그 외 규칙
- **Version 필드는 사용하지 않는다.** 버전 관리는 git/파일명에서 다루고, 커버 메타에는 표기하지 않음.
- "Department" 라벨도 사용하지 않음 (Team으로 통일).

---

## 6. 사이드 네비게이션 (Side Nav / TOC)

> **상단 고정 바(Top Nav)는 사용하지 않는다.** 보고서는 단일 문서이며, 페이지 상단을 항상 잡아먹는 sticky bar는 콘텐츠를 가리고 인쇄 시에도 방해가 된다. 문서 내 이동은 **사이드 네비**가 전담한다.

Claude Support 레일 패턴을 차용. 본문 **좌측**에 항상 떠 있고, 활성 섹션을 강조.

### 6.1 마크업 — H1(PART) + H2(섹션) 위계

> **사이드 네비는 H1(PART 그룹)과 H2(섹션) 두 위계만 노출한다.** H3 이하는 노출하지 않는다 (depth 1로 평탄화하면 길이가 폭발). PART가 없는 보고서는 H2만 나열.

```html
<aside class="side-nav" aria-label="Section navigation">
  <ul class="side-nav-list">
    <!-- H1: PART 그룹 헤더 — 더 강한 시각적 위계 -->
    <li><a href="#part-1" data-target="part-1" class="sn-h1">
      <span class="sn-num">PART I</span><span class="sn-title">글로벌 시장</span>
    </a></li>

    <!-- H2: 그 PART 안의 섹션들 (들여쓰기 + 작은 글자) -->
    <li><a href="#exec"     data-target="exec"><span class="sn-num">01</span><span class="sn-title">핵심 지표</span></a></li>
    <li><a href="#overview" data-target="overview"><span class="sn-num">02</span><span class="sn-title">시장 개관</span></a></li>
    <!-- ... -->

    <li><a href="#part-2" data-target="part-2" class="sn-h1">
      <span class="sn-num">PART II</span><span class="sn-title">국내 시장</span>
    </a></li>
    <!-- 다음 PART의 섹션들 ... -->
  </ul>
</aside>
```

### 6.2 스타일 핵심
```css
.side-nav {
  position: fixed;
  top: 96px;
  /* 본문 좌측 끝 − 40px − nav 폭(200px). 단 화면이 좁으면 뷰포트 좌측 24px 확보 */
  left: max(
    24px,
    calc(50% - (var(--max) / 2) - 40px - 200px)
  );
  z-index: 90;
  width: 200px;
  max-height: calc(100vh - 128px);
  overflow-y: auto;
}
.side-nav-list { border-left: 2px solid var(--line-soft); }
.side-nav-list a {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 8px;
  align-items: baseline;
  padding: 7px 0 7px 12px;
  margin-left: -2px;
  border-left: 2px solid transparent;
  color: var(--ink-4);
}
.side-nav-list a:hover { color: var(--ink); }
/* Active = brand blue (좌측 바·title·num 모두 한 컬러로 통일된 강조) */
.side-nav-list a.active { color: var(--brand-blue); border-left-color: var(--brand-blue); }
.side-nav-list a.active .sn-num { color: var(--brand-blue); }
.side-nav-list a.active .sn-title { color: var(--brand-blue); }

/* H1·H2 공통 — 같은 vertical rail에 stacked. 둘 다 동일 padding/rhythm, 동일 active 좌측 바, 동일 left edge.
   indent 없음 — 차이는 typography만 (H1: weight 700·uppercase eyebrow, H2: weight 500·body-sm). */
.side-nav-list .sn-num   { font-family: var(--font-mono); font-size: var(--fs-micro); font-weight: 600; color: var(--ink-5); letter-spacing: 0; }
.side-nav-list .sn-title { font-size: var(--fs-body-sm); font-weight: 500; line-height: var(--lh-snug); letter-spacing: -0.005em; color: var(--ink-4); }

/* H1 entries (PART 그룹 헤더) — H2와 같은 회색 톤. typography만 prominent (weight 700·uppercase eyebrow). */
.side-nav-list a.sn-h1 { color: var(--ink-4); }
.side-nav-list a.sn-h1 .sn-num   { font-size: 11px; letter-spacing: 0; font-weight: 700; color: var(--ink-4); text-transform: uppercase; }
.side-nav-list a.sn-h1 .sn-title { font-size: 13px; font-weight: 700; color: var(--ink-4); }

/* ⚠ Specificity 함정 — H1 active 별도 룰 필수.
   `.side-nav-list a.active .sn-num`(0,3,1)와 `.side-nav-list a.sn-h1 .sn-num`(0,3,1)이 같은 specificity이고
   H1 default가 source 뒤에 있어 active 룰을 무력화. → `.sn-h1.active`로 specificity (0,4,1) 확보. */
.side-nav-list a.sn-h1.active,
.side-nav-list a.sn-h1.active .sn-num,
.side-nav-list a.sn-h1.active .sn-title { color: var(--brand-blue); }

/* H2 indent — PART(.sn-h1)가 존재하는 네비에서만 적용. H2가 H1 아래에 종속됨을 indent로 표현.
   PART 없는 보고서(평면 H2 나열)에는 적용되지 않음 — :has()로 스코프. */
.side-nav-list:has(a.sn-h1) a:not(.sn-h1) { padding-left: 20px; }

@media (max-width: 1499px) { .side-nav { display: none; } }
```

### 6.3 반응형 동작 규칙

| 뷰포트 | 본문 좌측 ↔ TOC 우측 간격 |
|---|---|
| ≤ 1499px | TOC 숨김 |
| ≥ 1500px | **40px 고정** (본문 기준 정렬) |

> 핵심 원리: TOC를 뷰포트 왼쪽이 아니라 **본문 왼쪽 끝 − 40px** 위치에 고정. `max(24px, …)`로 작은 화면에서 left가 음수가 되어 뷰포트 밖으로 나가지 않게 하한을 둔다.
> 800px 본문에서는 표시 시작 지점(1500px)에서 이미 `50% − 400 − 40 − 200 = 110px`로 여유가 있어, 하한(24px)이 표시 구간에서 트리거되지 않는다 — 하한은 안전장치로만 작동하고 별도 전환 구간이 없다.

### 6.4 첫 진입 위치 + 활성 추적 (JS)
```javascript
document.addEventListener('DOMContentLoaded', function() {
  const nav     = document.querySelector('.side-nav');
  const links   = document.querySelectorAll('.side-nav-list a');
  const map     = {};
  links.forEach(a => { map[a.dataset.target] = a; });
  const sections = Object.keys(map).map(id => document.getElementById(id)).filter(Boolean);
  /* Anchor 결정:
     - 첫 navigated 섹션이 PART(.part-divider)이면 .part-divider 카드 fill 상단을 anchor로 사용.
     - 일반 섹션이면 안쪽 h2(또는 h1)을 anchor로 사용.
     PART는 카드 fill이 있어 카드 상단(=section box top)과 정렬해야 시각적으로 자연스럽고,
     일반 섹션은 padding 위 콘텐츠 시작점(h2)과 맞춰야 자연스러움. */
  const firstSection = sections[0];
  const isPartFirst  = firstSection && firstSection.classList.contains('part-divider');
  const anchorEl     = isPartFirst ? firstSection : (firstSection?.querySelector('h1, h2') || firstSection);
  const PIN_TOP  = 32;

  function getAnchorY() { return anchorEl.getBoundingClientRect().top + window.scrollY; }
  function update() {
    const y = window.scrollY + window.innerHeight * 0.3;
    let active = sections[0];
    for (const s of sections) { if (s.offsetTop <= y) active = s; }
    links.forEach(a => a.classList.remove('active'));
    if (active && map[active.id]) map[active.id].classList.add('active');
    if (nav && anchorEl) {
      const anchorY = getAnchorY();
      nav.style.top = Math.max(PIN_TOP, anchorY - window.scrollY) + 'px';
    }
  }
  window.addEventListener('scroll', update, { passive: true });
  window.addEventListener('resize', update);
  update();
  /* 폰트·이미지 로딩 후 재계산 — 초기 anchorY가 layout 변화로 어긋나는 것 방지 (필수) */
  if (document.fonts && document.fonts.ready) document.fonts.ready.then(update);
  window.addEventListener('load', update);
});
```
- TOC는 첫 섹션의 box top(PART의 경우) 또는 첫 H2의 top(일반 섹션)에서 시작 → 스크롤하면 상단 32px에 핀.
- **`document.fonts.ready` + `window.load` 재계산 필수** — Pretendard 폰트 로드 전에는 헤딩의 height·position이 fallback 폰트 기준으로 계산되어 anchor가 어긋남. 폰트 로드 후 한 번 더 update 해야 정확한 위치에 정렬.
- `.active` 클래스 = 본문 30% 라인을 마지막으로 통과한 섹션 (PART도 포함).

### 6.5 항목 표기 규칙
- **숫자(`sn-num`) + 한글 제목(`sn-title`)**, gap 8px (붙어 보일 정도로 좁게).
- 제목은 정적 명사형 (`수익 구조`, `시장 기회`). 의문형 금지.
- **H2 섹션 번호**는 항상 두 자리 (`01`, `02`, …). 별첨은 `APX`.
- **H1 PART 번호**는 로마자 (`PART I`, `PART II`, …).
- H1 항목은 `class="sn-h1"`을 추가하고, H2와 같은 마크업 구조 유지 (`.sn-num` + `.sn-title`).

### 6.6 Scroll-to-Top 플로팅 버튼 (`.scroll-top`)

> **모든 보고서는 우하단 floating "맨 위로" 버튼을 가진다.** 보고서가 길어 사이드 네비를 클릭하기 위해 한참 위로 스크롤해야 하는 부담을 줄이기 위함. 사이드 네비가 숨겨지는 좁은 화면(<1500px)에서도 작동해야 한다.

#### 마크업
```html
<button class="scroll-top" type="button" aria-label="맨 위로">
  <svg width="14" height="14" viewBox="0 0 14 14" fill="none" aria-hidden="true">
    <path d="M7 11V3M7 3L3 7M7 3L11 7" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>
</button>
```

#### 스타일
```css
.scroll-top {
  position: fixed;
  right: 32px;
  bottom: 32px;
  width: 44px;
  height: 44px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: var(--ink);
  color: var(--surface);
  border: none;
  border-radius: 8px;
  cursor: pointer;
  opacity: 0;
  pointer-events: none;
  transform: translateY(8px);
  transition: opacity var(--dur) var(--ease),
              transform var(--dur) var(--ease),
              background var(--dur) var(--ease);
  box-shadow: 0 6px 20px rgba(25, 25, 25, 0.18),
              0 1px 2px rgba(25, 25, 25, 0.08);
  z-index: 100;
}
.scroll-top.visible {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}
.scroll-top:hover  { background: var(--ink-2); }
.scroll-top:active { transform: translateY(0) scale(0.96); }
.scroll-top:focus-visible {
  outline: 2px solid var(--brand-blue);
  outline-offset: 2px;
}
@media (max-width: 880px) {
  .scroll-top { right: 20px; bottom: 20px; }
}
```

#### JS — 표시·동작
```javascript
document.addEventListener('DOMContentLoaded', function() {
  const btn = document.querySelector('.scroll-top');
  if (!btn) return;
  /* 첫 화면(viewport 1개) 이상 스크롤 시 노출. 너무 빨리 뜨면 시각 노이즈 */
  const SHOW_AFTER = Math.max(600, window.innerHeight * 0.6);
  function toggle() {
    btn.classList.toggle('visible', window.scrollY > SHOW_AFTER);
  }
  btn.addEventListener('click', () => {
    window.scrollTo({ top: 0, behavior: 'smooth' });
  });
  window.addEventListener('scroll', toggle, { passive: true });
  window.addEventListener('resize', toggle);
  toggle();
});
```

#### 규칙
- **위치**: 뷰포트 우하단 고정. `right: 32px; bottom: 32px` (모바일 20px).
- **크기**: 44×44px (터치 타겟 최소). `border-radius: 8px` (라운드 사각).
- **컬러**: 배경 `var(--ink)`, 아이콘 흰색. 사이드 네비 active 컬러(brand-blue)와 다른 검정으로 분리해 시각 위계 구분.
- **아이콘**: 위 화살표 SVG(`↑`). 크기 14×14px, 1.5px stroke. 이모지·유니코드 화살표 사용 금지(렌더링 일관성).
- **노출 조건**: `scrollY > 600px` 또는 `0.6 × innerHeight` (둘 중 큰 값). 첫 화면에서는 숨김.
- **사라짐**: 맨 위 도달 시 자동 숨김. transition으로 부드럽게.
- **shadow**: `0 6px 20px rgba(25,25,25,0.18)` — 본문 위로 떠 있는 인상. NDS의 일반적인 그림자 절제 원칙의 **예외** (floating UI는 그림자가 필수).
- **사이드 네비와 z-index 분리**: side-nav `z-index: 90`, scroll-top `z-index: 100` — 두 요소가 겹쳐도 항상 버튼이 위.
- **a11y**: `aria-label="맨 위로"` 필수, 키보드 포커스 시 `outline` 표시(focus-visible).
- **클릭 동작**: `window.scrollTo({ top: 0, behavior: 'smooth' })`로 부드러운 스크롤. `html { scroll-behavior: smooth }`도 함께 활성화 권장(11. 모션 참고).

---

## 7. 섹션 (Section)

```html
<section class="section [muted]" id="...">
  <div class="section-inner">

    <!-- 7.1 섹션 라인 — 라인만, 텍스트 없음 -->
    <div class="section-tag"></div>

    <!-- 7.2 섹션 헤드 — H2 + lede 단순 구조 -->
    <div class="section-head">
      <h2><span class="num-prefix">01</span>수익 구조</h2>
      <p class="lede">…(섹션 인트로, 1~2문단)…</p>
    </div>

    <!-- 7.3 본문 소제목 + 컴포넌트 — 제목과 표는 .block으로 함께 감싼다 -->
    <div class="block">
      <div class="block-head"><h3>소제목</h3></div>
      <div class="table-wrap">…</div>
    </div>

    <!-- 7.4 섹션 마무리 콜아웃 -->
    <div class="callout">…</div>

  </div>
</section>
```

> **레이아웃 구조: `--max` 정렬은 `.section-inner`가 담당.** `main`(또는 `.section`)이 좌우 `--pad-x` 패딩을 갖고, 안쪽 `.section-inner`가 `max-width: var(--max); margin: 0 auto`로 본문 폭을 잡는다. 커버(`.cover-inner`)·푸터(`.footer-inner`)와 동일한 구조라 네 영역의 좌우 모서리가 한 수직선에 정렬된다. `max-width`를 `main`에 직접 걸고 그 위에 패딩을 또 주면 본문이 `--max − 2×pad-x`로 좁아져 커버·푸터와 어긋나므로 금지.

```css
main { padding: 0 var(--pad-x); }
.section { padding: var(--section-py) 0; }
.section-inner { max-width: var(--max); margin: 0 auto; }
```

### 7.1 섹션 라인 (`section-tag`)

> **`section-tag`는 라인 1개**만을 그린다. 안의 어떤 요소도 표시하지 않는다(레거시 마크업 호환을 위해 자식 hide). 영문 메타는 두지 않는다.

```css
.section-tag { border-top: 3px solid var(--line); margin-bottom: 28px; min-height: 0; }
.section-tag > * { display: none !important; }
```

### 7.2 섹션 헤드 — H2 + lede 단순 구조

> **섹션 헤드는 H2(번호 + 한글 타이틀) + lede(도입 문장) 만으로 구성한다.** 제목 우측에 영문 메타 라벨을 두지 않는다 — 시선이 분산되고, 한국어 본문의 톤을 약화시킨다.

```html
<div class="section-head">
  <h2><span class="num-prefix">01</span>수익 구조</h2>
  <p class="lede">…(섹션 인트로, 1~2문단)…</p>
</div>
```

```css
.section-head { display: block; margin-bottom: 56px; }
.section-head > h1, .section-head > h2 { margin-bottom: 24px; }

/* H2는 항상 토큰 사이즈(40px)로 강제 — display-xl 등 다른 클래스 무력화 (!important) */
.section-head h2,
.section-head h2.display-xl,
.section-head h2.display-xxl {
  font-family: var(--font-sans) !important;
  font-size: var(--fs-h2) !important;     /* 40px */
  line-height: var(--lh-snug) !important;
  letter-spacing: 0 !important;
  font-weight: 700 !important;
  color: var(--ink) !important;
}

/* 번호 prefix — H2와 동일하게 weight 700 */
.section-head h2 .num-prefix {
  display: inline-block;
  margin-right: 16px;
  color: var(--ink-4);
  font-weight: 700;
}
```

#### 헤드 작성 규칙
- `<h2>`에 `.num-prefix`(섹션 번호) + 한글 타이틀. 번호는 두 자리(`01`, `02`, …), 별첨은 `APX`.
- **모든 섹션 H2는 동일한 40px / weight 700**로 강제한다. 다른 디스플레이 클래스(`display-xl` 등)와 함께 붙여도 자동으로 40px이 적용되도록 CSS에서 `!important`로 명시한다.
- **`.num-prefix`도 weight 700** — 번호와 타이틀이 같은 굵기로 한 단위처럼 읽히게 한다.
- 제목은 **정적 명사형**. 의문형(`~인가`) 금지.
- `<p class="lede">` 도입 문장은 **1~2문단** (3.3 참고). 짧은 한 줄로 자르지 않으며, 별도 본문 단락을 또 두어 중복시키지 않는다.
- ❌ **제목 우측 영문 메타 라벨 사용 금지.**

### 7.3 본문 소제목 — 2가지 패턴 중 선택

본문 소제목은 **상황에 맞는 2가지 패턴 중 하나**를 쓴다. 결정 기준은 H3 단독으로 둘지, H3 + 우측 메타를 한 줄에 묶을지이다.

> **표 위 제목은 항상 H3(패턴 A).** 크기와 무관하게 표·차트·KPI 등 데이터 컴포넌트 위 제목은 H4로 격하하지 않는다. 표가 여러 개 연속으로 나와도 모두 H3로 통일한다 — 위계 일관성이 가독성보다 우선한다.

#### A. **섹션 직속 H3 (20px, 라인 없음)** — 컴포넌트가 자체 상단 라인을 가질 때 (디폴트)
표(`.table-wrap`), KPI 행(`.kpi-row`), 분배 리스트 등 대부분의 NDS 컴포넌트는 자체 `border-top`을 가진다. 이때 H3에 underline을 주면 **이중 라인 문제**가 발생한다. → H3는 **마진만으로 분리**.

> **❗ 제목과 컴포넌트는 `.block`으로 함께 감싼다.** H3와 표를 `.section-inner` 직속에 나란히 두면 표가 섹션 리듬(`.section-inner > * { margin-top: 56px }`)을 그대로 받아 **제목과 표 사이가 56px**로 벌어진다 — 무관한 두 블록 사이 간격과 같아져, 제목이 자기 표에서 분리돼 보인다. 제목+컴포넌트를 한 `.block` 안에 넣으면 둘 다 블록 리듬(`.block > * + * { margin-top: 24px }`)을 받아 **표가 제목에 24px로 붙고**, 56px는 `.block`의 바깥 가장자리에서만 적용된다. 즉 56px(블록 사이)·24px(블록 안)이 각자 제 위치에서 작동.

```html
<div class="block">
  <div class="block-head"><h3>분기별 거래량 (2024)</h3></div>
  <div class="table-wrap"><table>…</table></div>
</div>
```

```css
h3, .h3 { font-size: var(--fs-h3); line-height: var(--lh-snug); letter-spacing: 0; font-weight: 700; color: var(--ink); }   /* --fs-h3 = 20px, weight 700 — 아래 .section-inner h3와 동일 값 */

/* 섹션 안 모든 h3 (descendant) — 어떤 깊이에 있어도 56px 위 마진.
   margin-bottom은 0 — 다음 요소의 자체 마진이 갭을 결정 (이중 합산 방지). */
/* 베이스 h3(20px/700)를 그대로 상속 — 여기서는 섹션 안 리듬(마진)만 추가 */
.section-inner h3 {
  margin-top: 56px;
  margin-bottom: 0;
}
.section-inner h3:first-child { margin-top: 0; }

/* 카드 컴포넌트 내부 h3 — 카드 자체 레이아웃이 처리, 위 마진 0 */
.problem-card h3, .brand-card h3, .phase h3 { margin-top: 0; }

/* .block — 제목+컴포넌트 페어링. 바깥은 56px 섹션 리듬, 안은 24px 블록 리듬 */
.block > * + * { margin-top: 24px; }
.block > .callout { margin-top: 32px; }
```

> **margin-bottom을 0으로 두는 이유** — 헤딩에 bottom 마진을 주면 다음 요소의 top 마진과 겹쳐(또는 더해져) 시각 갭이 들쭉날쭉해진다. 헤딩은 위 갭만, 본문 요소는 자체 위 갭만 주는 단방향 룰로 가면 어떤 조합에서도 갭이 일정.

> **descendant selector(`.section-inner h3`)를 쓰는 이유** — h3가 `.block` 안, 또는 `.g2 > .block > .block-head` 안 등 다양한 깊이에 들어가도 일관된 56px 위 마진을 보장한다. `.section-inner > h3`(직속 자식)만 쓰면 직속 h3에만 적용돼 깊이가 다른 h3 마진이 누락된다.

#### B. **`.block-head` 래퍼 (20px, 라인 없음)** — H3 + 우측 메타를 한 줄에 두고 싶을 때
`.block-head`는 H3와 우측 메타(단위·메모 등)를 한 행으로 묶는 **레이아웃 래퍼**일 뿐이다. **자체 라인을 그리지 않는다** (헤딩 룰: H3는 선 없음).

```css
.block { margin-top: 56px; }
.block:first-child { margin-top: 0; }
.block-head {
  margin-bottom: 20px;
  padding-bottom: 0;            /* 라인 없음 */
  border-bottom: none;          /* ❗ 절대 라인 추가 금지 */
  display: flex;
  justify-content: flex-start;  /* meta는 h3 바로 옆에 inline */
  align-items: baseline;
  gap: 12px;
  flex-wrap: wrap;
}
.block-head h3 {
  font-size: 20px;
  font-weight: 700;
  line-height: var(--lh-snug);
  letter-spacing: 0;
  color: var(--ink);
}
.block-head .meta {
  font-family: var(--font-mono);
  font-size: var(--fs-micro);
  color: var(--ink-4);
  letter-spacing: 0;
  text-transform: uppercase;
}
```

#### 패턴 선택 기준 (요약 표)

| 상황 | 패턴 | 헤딩 위계 |
|---|---|---|
| 섹션 안의 소제목 / 표·차트 위 제목 (단독 H3) | **A: `<h3>`** (20px, no line) | 강 |
| H3 + 우측 메타(단위·기간 등)를 한 줄에 두고 싶을 때 | **B: `.block-head h3`** (20px, no line) | 강 |

#### 공통 규칙
- **H3는 절대 라인을 가지지 않는다.** (위 토큰표의 헤딩 위계 규칙 참고)
- **소제목은 본문 데이터 값보다 시각적으로 강해야 한다.**
- **표·차트·KPI 등 데이터 컴포넌트 위 제목은 항상 H3.** H4로 격하하지 않는다. 한 섹션에 표가 여러 개 연속으로 나와도 모두 H3로 통일한다.
- H4(15px)는 본문 소제목으로 사용하지 않는다 — 표/컴포넌트 제목은 H3로 통일한다.

### 7.4 섹션 vertical rhythm — `.section-inner > *` 룰

> **섹션 안 모든 최상위 자식은 일관된 56px의 상단 마진을 가진다.** 컴포넌트 자체에 margin-top을 박지 말고, 부모 컨테이너가 일괄 관리한다 — 한 곳에서 리듬을 통제하는 것이 들쭉날쭉을 막는 핵심.

```css
/* 1단: section 직속 자식 — 일관된 56px 간격 */
.section-inner > * { margin-top: 56px; }
.section-inner > *:first-child { margin-top: 0; }
.section-inner > .section-tag,
.section-inner > .section-head { margin-top: 0; }   /* 섹션 시작부 자체 — 추가 마진 없음 */

/* 2단: 그리드 안에서는 자식 margin이 grid gap과 중복된다. 항상 grid gap만 사용 */
.g2 > *, .g3 > * { margin-top: 0 !important; }

/* 3단: .block 내부 — 24px 균일 리듬 (callout만 32px).
   ❌ `.block { margin-top: 0 }` 같은 룰을 추가하지 말 것 — 1단 룰과 specificity가 같아 source 뒤로 와서 1단을 무력화함 (아래 함정 참고). */
.block > * + * { margin-top: 24px; }
.block > .callout { margin-top: 32px; }

/* .callout: 위쪽만 호흡, 아래쪽은 다음 형제의 margin-top이 처리 (이중 카운트 방지) */
.callout { margin-top: 32px; margin-bottom: 0; }
```

#### Specificity 주의 — 컴포넌트에 마진을 박지 말 것
`.section-inner > *`(specificity 0,1,0)는 `.block { margin:0 }`(0,1,0)과 같은 등급이라, 컴포넌트 클래스에서 `margin`을 재선언하면 source 순서로 충돌해 56px·24px 리듬이 무력화된다(헤딩이 위 콘텐츠에 붙어버림).
- 컴포넌트 클래스에 **`margin:0`을 재선언하지 않는다.** 글로벌 `*{margin:0}` 리셋이 이미 처리하므로, 컴포넌트는 양수 마진이 필요할 때만 명시한다. (예: `.bul{list-style:none;padding:0;}` — `margin:0` 빼기)
- 컨테이너 리듬은 `.section-inner > *`(1단)·`.g2/.g3 > *`(2단)·`.block > * + *`(3단)이 전담한다. 더 강한 우선순위가 필요하면 `.section-inner > .block`(0,2,0)처럼 클래스 둘로 명시.
- 의도: 컴포넌트마다 자체 마진을 주면 조합에 따라 합쳐지거나 collapse돼 간격이 들쭉날쭉해진다. 리듬을 한 곳에서 통제해야 일정해진다.

#### 마진 스케일 요약
| 위치 | 갭 |
|---|---|
| 섹션 직속 자식 사이 (`.section-inner > * + *`) | **56px** |
| 그리드(`.g2`, `.g3`) 자식 사이 | grid `gap: 56px` |
| 블록(`.block`) 내부 자식 사이 | **24px** |
| 블록 안 callout 위 (`.block > .callout`) | **32px** |
| 헤딩 위 (h1/h2/h3/h4) | 위계별 (2.2 헤딩 위계 표 참고) |

### 7.5 섹션 내 레이아웃 — 위/아래 배치를 우선

> **두 개의 데이터 블록(표·차트·리스트)을 좌우로 두는 것은 기본적으로 금지.** 한국어 본문 + 표가 겹치면 가로 폭이 좁아져 텍스트가 깨지고, 표가 줄바꿈되며 가독성이 무너진다. **세로(위/아래)로 쌓는 것을 디폴트**로 한다.

```css
/* g2: 두 자식을 세로로 (NDS 디폴트) */
.g2 { display: grid; grid-template-columns: 1fr; gap: 56px; }

/* g3: 짧은 stat 3개 비교용 (가로 유지 OK) */
.g3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
```

#### 가로 배치를 사용할 때
다음 조건을 **모두** 만족할 때만 가로 비교를 허용한다.
- 자식 블록이 **표를 포함하지 않음**.
- 각 블록의 본문 텍스트가 짧음(2–3줄 이내).
- "A vs B" 처럼 **명시적인 좌우 비교**가 의미를 가질 때.

이 외에는 모두 세로(`.g2`)로 둔다.

### 7.6 표 (Table) — 헤더와 셀 정렬 일관성

```css
.table-wrap { border-top: 1px solid var(--ink); border-bottom: 1px solid var(--ink); overflow-x: auto; }
table { width: 100%; border-collapse: collapse; font-size: 13px; }
/* thead 배경은 light gray (--surface-2 = #efefef) + 짙은 글자. 한 페이지에 표가 여러 개여도 본문 흐름을 끊지 않는 가벼운 톤 */
thead th { text-align: left; padding: 12px 16px; background: var(--surface-2); color: var(--ink); font-family: var(--font-mono); font-size: var(--fs-micro); text-transform: uppercase; letter-spacing: 0; font-weight: 600; white-space: nowrap; }
thead th.num, td.num { text-align: right; font-feature-settings: "tnum"; }
tbody td { padding: 14px 16px; border-bottom: 1px solid var(--line-softer); color: var(--ink-2); vertical-align: top; font-size: 13.5px; }
tbody tr:last-child td { border-bottom: none; }
```

#### thead 배경 색 룰
- 배경은 **`--surface-2` (#efefef)** — pale gray. 검정(`--ink`)·짙은 회색(`--ink-3`)을 쓰지 않는다.
- 짙은 헤더는 시각 무게가 너무 강해 한 페이지에 표가 여러 개 있으면 본문 흐름을 끊는다. 옅은 그레이가 헤더 식별성은 유지하면서 톤을 가볍게.
- 짙은 글자(`var(--ink)`) 사용 — `--surface-2` 위 ink 대비 약 14:1 (WCAG AAA 통과).

#### 정렬 룰
- **모든 숫자 컬럼은 `class="num"`을 헤더(`<th>`)와 모든 셀(`<td>`)에 빠짐없이 붙인다.** 한쪽만 빠지면 헤더와 셀의 정렬이 어긋난다.
- 숫자 셀에는 `class="num tnum"` (또는 `font-feature-settings: "tnum"`)으로 등폭 숫자 활성화.
- 모든 `tbody td`의 `vertical-align: top` 통일. middle을 쓰지 않는다(다중 라인 셀에서 위계가 어긋남).
- 표는 항상 `.table-wrap`으로 감싼다. 표 폭이 컨텐트 영역(`--max`)을 넘을 수 있는 경우 `overflow-x: auto`로 가로 스크롤.
- 셀 내용을 줄바꿈으로 강제하지 않는다.

#### 라인 두께 룰 — 모든 표 라인 1px MAX

> **표(`.table-wrap`, `.steps`, `.flow`, `.breakdown-list`, `.geo-grid` 등 표/리스트형 컴포넌트)의 모든 외곽선은 1px이 최대다.** 2px 이상의 두꺼운 선은 시각 무게가 너무 강해 본문 흐름을 깨고, 한 페이지에 표가 여러 개 등장하면 시각적 어수선함을 만든다.

| 라인 | 두께 |
|---|---|
| `.table-wrap` border-top | **1px solid var(--ink)** (MAX) |
| `thead th` 배경 | — (행 자체가 헤더 시각 무게 담당) |
| `tbody td` border-bottom | **1px solid var(--line-softer)** (행 구분, 더 옅게) |
| `.table-wrap` border-bottom | **1px solid var(--ink)** (top과 동일) |
| 기타 list-like 컴포넌트(`.steps`, `.flow`, `.geo-grid`, `.breakdown-list`, `.fee-math`, `.insight-list`) 외곽 | **1px solid var(--ink)** (top·bottom 모두) |

**2px 이상 절대 금지** — 디자인시스템 위반. (예외: H2 위 `.section-tag` 3px·H1 위 `.part-divider`는 헤딩 디바이더로, 표 영역과 다른 레이어이므로 별도)

#### 컴포넌트 외곽선 패턴 — 데이터 행(A) vs 카드(B)

> **그리드형 컴포넌트의 외곽선은 두 패턴 중 하나. 섞어 쓰지 않는다.**
> 가로 그리드형은 모두 Pattern B 디폴트. Pattern A는 화살표/단계로 연결된 흐름 컴포넌트(`.flow`, `.steps`)와 표(`.table-wrap`)에만 한정.

##### Pattern B — 자기완결 카드 (디폴트)
각 셀이 self-contained 박스. 시각적으로 분리되어 그리드 형태로 떠 있는 인상.

```css
.problem-grid {
  display: grid;
  gap: 1px;
  background: var(--line-soft);            /* gap이 라인으로 비침 */
  border: 1px solid var(--line-soft);      /* 사방 외곽 박스 */
}
.problem-card { background: var(--surface); padding: 32px; }    /* 흰 카드가 채움 */
```

| 적용 컴포넌트 |
|---|
| `.problem-grid`, `.brand-cards` (자기완결 인사이트/프로필 카드) |
| `.kpi-row`, `.metric-grid`, `.geo-grid` (수치 비교 그리드) |

##### Pattern A — 데이터 행 / 흐름 (예외)
화살표·단계로 의미가 연결되는 컴포넌트, 그리고 표(table) 본체에만 한정. 본문 흐름에 자연스럽게 녹아드는 가벼운 톤.

```css
.flow {
  display: grid;
  border-top:    1px solid var(--ink);    /* 검정 상단 1px */
  border-bottom: 1px solid var(--ink);    /* 검정 하단 1px */
}
.flow-step { border-left: 1px solid var(--line-soft); }
.flow-step:first-child { border-left: none; }
.flow-step::after { content: "→"; }                   /* 단계 사이 화살표 */
```

| 적용 컴포넌트 |
|---|
| `.flow`, `.steps` (화살표/단계로 연결된 흐름) |
| `.table-wrap` (표 본체 — thead·tbody 구조) |

##### 결정 기준

| 콘텐츠 성격 | 패턴 |
|---|---|
| 가로 비교 데이터 그리드 (수치·라벨·짧은 설명) | **B: 카드** (디폴트) |
| 각 셀이 self-contained 콘텐츠 (헤딩+본문+stat) | **B: 카드** |
| **화살표/단계로 연결된 흐름** (process flow, sequential steps) | **A: 데이터 행** |
| **표 본체** (thead + tbody) | **A: 데이터 행** |

**판단 가이드**:
- "이건 카드 그리드인가, 흐름인가?" — 흐름이면 A, 그 외엔 B.
- A는 화살표·번호 단계 등 **순서/연결**의 의미가 시각에 담겨야 할 때만.
- 단순한 4개 KPI / 4개 시장 비교는 **B**.

### 7.7 PART 그룹 헤더 (`.part-divider` / H1)

> **섹션이 약 6개를 넘으면 H1 PART 헤더로 묶는다.** 평평한 1–15 번호 나열은 시선이 길어져 흐름을 잃는다. PART 헤더는 보고서 안에 "챕터 표지" 역할을 한다.

```html
<section class="part-divider" id="part-2">
  <div class="section-inner">
    <div class="part-eyebrow">PART II</div>
    <h1>국내 시장 분석</h1>
    <span class="part-meta">Korea Market — 시장 현황부터 IP 라이선스까지</span>
  </div>
</section>
```

```css
/* PART DIVIDER — solid brand-blue 배경 밴드. 색상은 .section-inner(body width = --max)에 한정해 화면 풀폭이 아닌 본문 폭에 맞춤 */
.part-divider {
  padding: 0 var(--pad-x);                           /* 외곽: 좁은 화면에서 가장자리 여백만 */
  margin-top: 120px;
}
.part-divider:first-of-type { margin-top: var(--section-py); }   /* 첫 요소가 PART일 때 커버와 붙지 않도록 — 일반 섹션 상단 패딩(72px)과 동일 */
.part-divider .section-inner {
  max-width: var(--max);                              /* body width = --max 한정 */
  margin: 0 auto;
  width: 100%;
  background:
    linear-gradient(115deg, rgba(15, 128, 246, 0.10) 0%, transparent 35%, transparent 65%, rgba(1, 160, 88, 0.06) 100%),
    var(--ink);                                       /* 검정 베이스 + 미세한 대각 sheen — 좌상 brand-blue 10% / 우하 brand-green 6% */
  color: var(--surface);                              /* 어두운 배경에 흰 글자 */
  padding: 40px;
  border-radius: 16px;                                /* 모서리 라운드 — 챕터 카드처럼 분리감 부여 */
  overflow: hidden;                                    /* gradient가 라운드 모서리 밖으로 안 나가게 */
}
/* PART eyebrow/meta는 mono uppercase, 자간 0 */
.part-divider .part-eyebrow {
  font-family: var(--font-mono);
  font-size: 14px;          /* 본문 micro(12px)보다 한 단계 위, H1(48px)과 호흡 맞춤 */
  letter-spacing: 0;
  text-transform: uppercase;
  color: rgba(255,255,255,0.70);
  font-weight: 700;
  margin-bottom: 12px;
}
.part-divider h1 { color: var(--surface); letter-spacing: 0; }
.part-divider .part-meta {
  display: block;
  margin-top: 12px;
  font-family: var(--font-mono);
  font-size: 14px;
  letter-spacing: 0;
  text-transform: uppercase;
  color: rgba(255,255,255,0.70);
  font-weight: 600;
}
```

#### 작성 규칙
- **PART 번호**는 로마자(`PART I`, `PART II`, `PART III`, …). 영문 mono uppercase.
- **PART 타이틀**은 한글(`국내 시장 분석`, `전략 시사점` 등). H1 토큰(48px) 사용.
- **part-meta**는 영문 부제 + 짧은 설명. mono uppercase.
- 6개 미만 섹션이면 PART 그룹화 불필요. 6~8개라도 단일 흐름이 자연스러우면 평면 구조 유지.
- PART 디바이더는 그 자체로 navigator의 H1 항목으로 노출된다.

#### 별첨(APX) 영역의 디바이더는 사용하지 않는다
- 별첨(`APX`) 섹션 안의 하위 블록(예: Phase 1·2·3 로드맵)은 **상단 디바이더 라인 없이** 마진만으로 분리한다.
- 본문 섹션과 달리 별첨은 부가 자료 성격이므로 디바이더가 강하게 그어지면 본문급 무게로 잘못 읽히기 쉽다.

```css
/* APX Phase block — 디바이더 없음, 마진만으로 분리 */
.phase { border-top: none; padding-top: 0; margin-top: 56px; }
.phase:first-child { margin-top: 0; }
```

---

## 8. 콜아웃 / 하이라이트 박스 (Callout / Highlight Box) — 섹션 요약 박스 통일

> **하나의 클래스 `.callout`이 모든 "강조 박스" 역할을 한다.**
> 즉 _Highlight 박스_, _Key Takeaway 박스_, _So What 박스_, _Implication 박스_ 모두 같은 구조 `.callout`을 쓰고 **상단 라벨 텍스트만 바꿔서** 용도를 구분한다.

### 8.1 구조

기본 구조는 모두 동일. 라벨에 따라 modifier 클래스만 추가.

```html
<!-- 기본 (pale yellow): Key Takeaway / So What / Implication / Highlight -->
<div class="callout">
  <div class="lbl">Key Takeaway</div>
  <p>…요약 문장…</p>
</div>

<!-- Note: pale blue -->
<div class="callout callout-note">
  <div class="lbl">Note</div>
  <p>…주의사항·전제·각주…</p>
</div>

<!-- Important: pale red -->
<div class="callout callout-important">
  <div class="lbl">Important</div>
  <p>…놓치면 안 되는 결정적 정보…</p>
</div>
```

### 8.2 스타일

```css
/* Default — pale yellow. Key Takeaway / So What / Implication / Highlight 모두 사용. 좌측 강조선 없음. */
.callout {
  margin-top: 32px;
  margin-bottom: 0;                                       /* 다음 형제의 margin이 갭 결정 */
  padding: 24px 28px;
  background: rgba(252, 246, 131, 0.30);                  /* brand-yellow 30% */
  border-left: none;                                       /* ❗ 좌측 강조선 사용 안 함 — 배경 색상만으로 강조 */
}

/* Tone variants — modifier 클래스로 배경 색상만 교체 (좌측선은 없음) */
.callout.callout-note      { background: rgba(15, 128, 246, 0.08); }    /* pale blue */
.callout.callout-important { background: rgba(235, 69, 61, 0.08); }     /* pale red */

.callout .lbl {
  font-family: var(--font-mono);
  font-size: var(--fs-micro);            /* 12px */
  text-transform: uppercase;
  color: var(--ink-4);
  margin-bottom: 10px;
  font-weight: 600;
  letter-spacing: 0;                     /* ❗ 자간 없음 — 박스 라벨 톤이 차분해짐 */
}
.callout p {
  font-size: var(--fs-body);             /* 15px */
  color: var(--ink);                     /* 본문보다 진한 검정 — 강조용 박스이므로 */
  line-height: var(--lh-loose);
}
.callout p + p { margin-top: 8px; }
```

### 8.3 라벨 사용 가이드 (6종)

| 라벨 | 색상 | modifier 클래스 | 언제 쓰는가 |
|---|---|---|---|
| `Key Takeaway`  | **pale yellow (default)** | (없음) | 섹션이 전달하는 한 줄 결론. **기본값**. |
| `Highlight`     | **pale yellow (default)** | (없음) | 데이터 속 특이값·놀라운 사실 강조 |
| `So What`       | **pale yellow (default)** | (없음) | "그래서 무엇을 해야 하나" — 액션·의사결정 함의 |
| `Implication`   | **pale yellow (default)** | (없음) | 시장/조직/제품 파급 효과 |
| `Note`          | **pale blue** | `.callout-note` | 주의사항·전제·각주 |
| `Important`     | **pale red** | `.callout-important` | 놓치면 안 되는 결정적 정보 (자주 쓰지 않음) |

> 의미적 강조(요약·하이라이트·시사점·결론)는 모두 같은 옅은 노랑 톤으로 한 묶음. **다른 톤은 의도가 분명히 다를 때만**: Note는 보조 정보(blue), Important는 위험·경고급 결정 정보(red).
> 좌측 강조선(border-left)은 모든 변형에서 사용하지 않는다 — 배경 색상만으로 충분히 시각 식별이 됨.

### 8.4 작성 규칙
- **구조는 항상 동일**: `.callout > .lbl + <p>…`. 변형 금지.
- 색상은 modifier 클래스로만 — 인라인 style 금지.
- **라벨은 영문 uppercase**, **본문은 한글**.
- 본문은 1~2 단락. 3단락 이상 길어지면 본문 섹션으로 빼기.
- 박스에 데코레이션(삼각형, 따옴표, 아이콘 등) 추가 금지.
- 한 섹션에 `.callout`은 **1회만**. 두 개 이상 쌓지 않음 (강조의 의미가 희석됨).
- 위치는 보통 섹션 마지막 — 데이터/본문이 다 나온 뒤 마무리 박스로 등장.

---

## 9. 푸터 (Footer)

밝은 톤 + 작은 글자 (헤더보다 글자 작음) + 헤더 정보의 푸터 버전.

```html
<footer class="footer" role="contentinfo">
  <div class="footer-inner">
    <div class="footer-row">
      <div class="footer-left">
        <div class="footer-line">
          <span class="footer-doc-title">결제 및 쿠폰 시장 분석</span>
        </div>
        <div class="footer-line footer-line-sub">
          <span>-</span><span class="dot">·</span>
          <span>-</span><span class="dot">·</span>
          <span class="mono">-</span>
        </div>
      </div>
      <div class="footer-right">
        <span class="footer-confidential">대외비</span>
      </div>
    </div>
    <p class="footer-disclaimer">
      본 문서는 대외비 자료입니다. 허가된 사용자 이외의 접근 및 배포를 금지하며, 이를 위반하는 경우 인사 및 민형사상 책임을 질 수 있습니다.
    </p>
    <div class="footer-copyright">© All Rights Reserved.</div>
  </div>
</footer>
```

### 9.1 푸터 규칙
- 배경 `--surface` (흰색), 위쪽에 `border-top: 1px solid var(--line-soft)`.
- `padding: 28px var(--pad-x)`. 마지막 섹션과의 간격은 `margin-top: 160px`.
- 좌측: **제목(굵게, ink) + 한 줄 메타(작고 옅은 ink-3)**.
  - 메타 한 줄: **`팀 · 이름 · 날짜`** (3개, 모두 한 줄에).
  - **날짜 포맷은 `YYYY.MM.DD`** (커버와 동일, 5.2 참고). 날짜 span에 `class="mono"` 필수.
  - **Version은 표기하지 않는다** (5.2 참고).
  - **미입력 메타는 푸터에서 숨긴다** — 커버는 `-`로 표시하지만, 푸터는 한 줄 메타가 짧고 빈 자리가 더 어색하므로 **해당 span 자체를 제외**한다 (JS로 자동 제거 또는 마크업에서 omit). 이웃 구분점(`·`)도 함께 정리.
  - 항목 사이 `gap: 4px` (헤더보다 좁게).

#### JS — 푸터 미입력 메타 자동 숨김
```javascript
/* 푸터의 .footer-line-sub 안에서 text가 `-`인 메타 span 제거.
   남은 dot(`·`) 중 양 끝의 것 + 연속된 것 정리. 결과: `팀 · 날짜` 처럼 깔끔. */
document.querySelectorAll('.footer-line-sub').forEach(line => {
  Array.from(line.children).forEach(el => {
    if (!el.classList.contains('dot') && el.textContent.trim() === '-') el.remove();
  });
  let kids = Array.from(line.children);
  for (let i = kids.length - 1; i >= 0; i--) {
    const el = kids[i];
    if (!el.classList.contains('dot')) continue;
    const p = el.previousElementSibling, n = el.nextElementSibling;
    if (!p || !n || p.classList.contains('dot') || n.classList.contains('dot')) el.remove();
  }
});
```

> **커버는 변경 없음.** 커버 메타 3종(Date · Team · Author)은 항상 3개 라벨이 보이는 그리드 구조이므로 빈 자리에 `-`을 표시. 푸터는 자유 흐름 한 줄이라 빈 자리가 시각적으로 어색해 숨김 처리가 자연스러움.
- 우측: **대외비 chip** — 커버의 칩과 동일한 디자인 (outline + 빨간 닷 + uppercase 모노).
- Disclaimer는 `--fs-micro` (12px), `--ink-4`, max-width 720px.
- Copyright는 모노, `--ink-5`, 위에 얇은 라인 1px (`var(--surface-1)`, #f7f7f7) — 거의 보이지 않는 가벼운 구분선. `var(--line-softer)`(#ededed)보다 한층 더 밝아서 푸터 마지막 줄이 시각적으로 떠 있는 느낌이 안 듦.

### 9.2 위계 규칙
- **푸터 글자는 헤더(상단 nav)보다 작거나 같다.**
- `.footer-doc-title`만 ink + bold + `--fs-body-sm` (13px).
- 메타 한 줄은 `--fs-micro` (12px) + `--ink-3`. 너무 옅으면 (`--ink-5` 이하) 사용 금지.

---

## 10. 컴포넌트 카탈로그 (Component Reference)

본 보고서에서 사용한 데이터/콘텐츠 표현 컴포넌트. 모두 흑백 + 한 가지 강조 컬러 원칙.

| 컴포넌트 | 클래스 | 용도 |
|---|---|---|
| KPI Row | `.kpi-row > .kpi` | 주요 지표 4개 가로 배치 |
| Exec Card | `.exec-card` | 익스큐티브 서머리 컨테이너 |
| Bar Chart | `.bar-chart > .bar-row` | 연도별/항목별 가로 막대 |
| Stack Bar | `.stack > .stack-seg` + `.stack-legend` | 구성비 누적 막대 + 범례 |
| Breakdown List | `.breakdown-list > .bd-row` | 행별 라벨/설명/막대/값 |
| Problem Cards | `.problem-grid > .problem-card` | 3분할 인사이트 카드 |
| Geo Cells | `.geo-grid > .geo-cell` | 4개국/지역 비교 |
| Comp Table | `.comp-table` | 경쟁사 재무 비교 표 |
| Brand Cards | `.brand-cards > .brand-card` | 국내 플레이어 카드 |
| Flow | `.flow > .flow-step` | 5단계 흐름 (`→` 화살표 자동) |
| Fee Math | `.fee-math > .fee-side` | 좌우 비교 수식 / 마진 계산 |
| Insight List | `.insight-list > .insight-row` | 큰 번호 + 헤딩 + 본문 |

각 컴포넌트는 모두 **상하단 1px 검정 라인**으로 시작/종료. 셀 사이는 `--line-soft`.

---

## 11. 모션 (Motion)

```css
--ease: cubic-bezier(0.32, 0.72, 0, 1);   /* iOS-like */
--dur:  240ms;
```

- 색·border·transform만 트랜지션. opacity 페이드인 등 무거운 모션은 사용하지 않음.
- `html { scroll-behavior: smooth; }` 활성화.

---

## 12. 접근성 / 마크업 위생

- 본문 언어: `<html lang="ko">`.
- 사이드 네비게이션은 `<aside aria-label="Section navigation">`.
- 푸터는 `<footer role="contentinfo">`.
- 시멘틱 헤딩(h1 → h2 → h3) 위계 유지. 헤딩 점프 금지.
- 색만으로 의미 전달 금지 — 차감/위험/긍정은 항상 라벨이나 부호와 함께.

---

## 13. 작성·운영 체크리스트

새 보고서를 만들 때 확인:

- [ ] `<html lang="ko">` 설정
- [ ] Pretendard CDN 로드
- [ ] 본문에 `word-break: keep-all; overflow-wrap: break-word;`
- [ ] 모든 폰트 사이즈가 `--fs-*` 토큰 사용 (12px 미만 금지)
- [ ] **본문 기본 폭 `--max: 800px`** — 커버·섹션·푸터 공통, 한 토큰으로 일괄 정렬
- [ ] **`--max` 정렬은 `.section-inner`/`.cover-inner`/`.footer-inner`가 담당** — `main`에 `max-width`와 패딩을 함께 걸지 않는다 (본문이 좁아져 커버·푸터와 어긋남)
- [ ] **상단 고정 바(top nav) 사용 안 함** — 네비게이션은 사이드 네비만
- [ ] **사이드 네비는 본문 좌측에 고정** — `left: max(24px, calc(50% - (--max/2) - 40px - 200px))`
- [ ] **TOC 표시 구간 ≥1500px**, 그 미만은 숨김 (800px 본문에서는 전환 구간 없이 항상 40px gap)
- [ ] **Scroll-to-Top 플로팅 버튼(`.scroll-top`) 포함** — 우하단 고정, 600px 스크롤 후 노출
- [ ] 커버: eyebrow(영문) + title(한글) + summary(2~3줄, 표지 전용) + 대외비 chip + meta **3종**(Date / Team / Author)
- [ ] **메타값 미입력 시 `-` 로 표기**, Version 사용 안 함
- [ ] **날짜는 `YYYY.MM.DD` 포맷** (예: `2025.05.04`) — 커버·푸터 모두. mono 적용 (`class="mono"`)
- [ ] 사이드 네비 항목: 정적 명사형 제목 + 두 자리 번호
- [ ] 섹션 lede는 **1~2문단**(본문 폭 따름) · 한 줄 요약+본문+콜아웃 3중 중복 금지
- [ ] **`section-tag`는 라인 1개만** (안에 텍스트 두지 않음)
- [ ] **섹션 헤드는 H2 + lede만** — 제목 우측 영문 메타 라벨 사용 금지
- [ ] **헤딩 라인 규칙: H1·H2만 라인을 가진다.** H3·H4는 라인 없음 (`.block-head` border 포함 절대 X)
- [ ] **헤딩 마진 스케일: H1(120) > H2(72) > H3(56) > H4(36)** — 위계 따라 줄어듦. H4도 본문과 충분히 분리
- [ ] **모든 H2는 40px / weight 700로 통일** (`--fs-h2` 토큰), H1은 48px — `display-xl` 등 다른 클래스 무시 (CSS `!important`로 강제)
- [ ] **`.num-prefix`도 weight 700** — H2 본문과 동일한 굵기
- [ ] **섹션 vertical rhythm 단일 룰**: `.section-inner > * { margin-top: 56px }`, 그리드 안에서는 `.g2 > *, .g3 > * { margin-top: 0 }` — 컴포넌트 자체 margin 금지
- [ ] **`.callout` margin-bottom: 0** — 다음 형제의 margin-top이 갭 결정 (이중 합산 방지)
- [ ] **섹션 6개 이상이면 H1 PART 헤더로 그룹화** (`.part-divider`)
- [ ] **사이드 네비는 H1·H2 두 위계만 표기** — H1은 `.sn-h1` 클래스로 prominent 처리, H2는 들여쓰기
- [ ] **제목+컴포넌트(표·차트·KPI)는 `.block`으로 함께 감싼다** — 제목이 표에 24px로 붙음. 바깥 56px 섹션 리듬과 분리. 직속에 나란히 두면 56px로 벌어짐
- [ ] **소제목 패턴 2가지** 중 선택: A) `<h3>` 20px no-line (기본) / B) `.block-head h3` 20px no-line (H3+우측 메타 래퍼). **표·차트·KPI 등 데이터 컴포넌트 위 제목은 항상 H3** (H4로 격하 금지)
- [ ] **표 포함 두 블록은 가로(g2) 금지**, 세로로 쌓기
- [ ] **표의 모든 숫자 컬럼은 헤더·셀 양쪽에 `class="num"`** 일관 적용
- [ ] **모든 표·리스트형 컴포넌트 외곽선은 1px MAX** (`.table-wrap`·`.steps`·`.flow`·`.geo-grid` 등 모두) — 2px 이상 금지
- [ ] **별첨(APX) 영역은 디바이더 없이 마진만으로 분리** (`.phase` border-top 제거)
- [ ] **본문 영역의 모든 헤딩(H2~H4)·번호 prefix·작은 라벨류는 letter-spacing 0** — 양수 자간은 커버/푸터 영문 chip에만 한정
- [ ] **PART 디바이더(`.part-divider`)는 brand-blue 10% 배경 + 40px 패딩 밴드** — 굵은 라인 fill 대신 색상 fill로 챕터 표지 효과
- [ ] **H3 마진 룰은 descendant selector(`.section-inner h3`)** — 모든 깊이의 h3에 일관 적용, `:first-child`는 0
- [ ] 모든 섹션 하단 요약은 `.callout` 단일 패턴
- [ ] 푸터: 제목(굵게) + 한 줄 메타(팀·이름·날짜) + 대외비 chip + disclaimer + copyright
- [ ] 마지막 섹션 ↔ 푸터 `margin-top: 160px`
- [ ] 의문형 헤딩(`~인가?`) 사용 안 함
