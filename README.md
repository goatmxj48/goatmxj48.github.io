# 조민주 포트폴리오 사이트

`조민주_포트폴리오.docx` 를 본문으로, `조민주 포폴.pdf` 의 화면 캡처를 이미지로 옮긴 정적 웹 포트폴리오입니다.
서버 없이 HTML 파일 하나 + 이미지 폴더로만 동작합니다.

```
chominju-portfolio/
├── index.html      ← 페이지 전부 (HTML·CSS·JS 한 파일)
├── images/         ← PDF 에서 추출한 화면 캡처 20개
└── README.md
```

---

## 1. 이미지 넣는 법  ★ 가장 중요

docx 에는 화면 이미지가 없어서, **초록 빗금 상자**로 자리만 잡아뒀습니다.
브라우저로 열면 `메뉴 이미지 자리` 라고 적힌 상자가 그 자리입니다.

### 넣는 순서

**① 이미지 파일을 `images/` 폴더에 넣습니다.** 상자에 적힌 파일 이름 그대로 저장하면 가장 편합니다.

**② `index.html` 에서 그 이름을 검색합니다.** 예를 들어 `p01-dailyreport.png` 로 검색하면 이런 부분이 나옵니다.

```html
<div class="thumb">
  <!-- 이미지 넣는 법 : 아래 <div class="ph"> 한 줄을 지우고 그 아래 주석의 <img> 를 살리세요 -->
  <div class="ph">
    <svg …></svg>
    <span>메뉴 이미지 자리</span><em>images/p01-dailyreport.png</em>
  </div>
  <!-- <img src="images/p01-dailyreport.png" alt="작업일지 화면"> -->
</div>
```

**③ `<div class="ph"> … </div>` 를 통째로 지우고, 그 아래 `<img>` 줄에서 `<!--` 와 `-->` 만 지웁니다.**

```html
<div class="thumb">
  <img src="images/p01-dailyreport.png" alt="작업일지 화면">
</div>
```

끝입니다. 크기·비율은 자동으로 맞춰집니다.

### 비어 있는 자리 목록

| 위치 | 파일 이름 | 무엇을 넣으면 되는지 |
|---|---|---|
| 카드 1 · 작업일지 | `p01-dailyreport.png` | 작업일지 목록/개요 화면 |
| 상세 1 · 작업일지 | `p01-erd.png` | 작업일지 ERD |
| 상세 1 · 작업일지 | `p01-screen.png` | 작업일지 개요 화면 |
| 상세 1 · 작업일지 | `p01-activity.png` | 액티비티(CBS) 화면 |
| 카드 2 · API 연계 | `p02-api.png` | 연동 구성도 |
| 상세 2 · API 연계 | `p02-architecture.png` | 송신 창구 아키텍처 |
| 상세 2 · API 연계 | `p02-sso.png` | SSO 순차 폴백 흐름도 |
| 카드 3 · 운영 | `p03-ops.png` | 서버 구성도 |
| 카드 6 · 에듀윌 | `p06-eduwill.png` | SmartTM 관리자 화면 |
| 상세 6 · 에듀윌 | `p06-eduwill-01.png` `p06-eduwill-02.png` | 관리자 화면 / IP 추적 |

> 악사손해보험 · SITellAgent · RPA 카드는 PDF 캡처가 이미 들어가 있어 손대지 않아도 됩니다.
> 자리가 필요 없으면 그 `<figure class="slot">` 또는 `<div class="thumb">` 를 통째로 지우면 됩니다.

---

## 2. 그 외에 채워야 할 곳

`index.html` 에서 `직접 넣어주세요` 를 검색하면 2군데 나옵니다.

| 위치 | 무엇을 |
|---|---|
| `<head>` 안 | 링크 공유 썸네일. `images/og.png` (1200×630) 로 저장하면 자동 적용. 없어도 정상 동작합니다. |
| Contact 섹션 | GitHub 주소. 없으면 그 `<a>` 줄을 통째로 지우세요. |

---

## 3. GitHub Pages 에 올리기

주소를 `아이디.github.io` 로 쓰려면 **저장소 이름이 반드시 `아이디.github.io`** 여야 합니다.

1. GitHub → **New repository** → 이름 `아이디.github.io` → **Public** → Create
2. 파일 올리기

```bash
cd D:/intellij/chominju-portfolio
git init
git add .
git commit -m "portfolio"
git branch -M main
git remote add origin https://github.com/아이디/아이디.github.io.git
git push -u origin main
```

터미널이 불편하면 저장소 화면에서 **Add file → Upload files** 로 `index.html` 과 `images` 폴더를 끌어다 놓아도 됩니다.

3. 저장소 → **Settings → Pages** → Source `Deploy from a branch`, Branch `main` / `/ (root)` → Save

1~2분 뒤 `https://아이디.github.io` 로 열립니다.

---

## 4. 고치는 법

전부 `index.html` 한 파일 안에 있습니다.

| 고치고 싶은 것 | 찾을 곳 |
|---|---|
| **테마 색** | 파일 맨 위 `:root` 의 `--accent` — 이 한 줄로 사이트 전체 색이 바뀝니다 |
| 카드 문구 | 해당 한글을 그대로 검색 |
| 상세(모달) 내용 | 파일 아래쪽 `<div hidden>` 안의 `id="d1"` ~ `id="d7"` |
| 카드 추가 | `<button class="pcard" …>` 블록을 복사하고 `data-detail` 을 새 id 로 |
| 순서 바꾸기 | `<button class="pcard">` 블록 순서를 바꾸면 그대로 반영 |

### 스크롤 감각 조절  ★

휠을 굴리면 바로 그만큼 뛰지 않고 목표 지점까지 미끄러지듯 따라갑니다.
`index.html` 아래쪽 `<script>` 안에서 **이 한 줄**만 만지면 됩니다.

```js
var FOLLOW = 0.06, WHEEL_STEP = 2.2, PAD_STEP = 1.0, FORCE = false;
```

| | 의미 | 추천 범위 |
|---|---|---|
| `FOLLOW` | 목표를 따라가는 비율. **작을수록 더 길게 미끄러짐** | `0.04` ~ `0.14` |
| `WHEEL_STEP` | **마우스 휠 한 칸에 가는 거리 배율** | `1.0` ~ `3.0` |
| `PAD_STEP` | 터치패드처럼 잘게 들어올 때 배율 | `0.8` ~ `1.2` |
| `FORCE` | OS 의 "동작 줄이기" 를 무시하고 켜기 | `true` / `false` |

현재 설정에서 실제 이동 거리입니다.

| 입력 | 이동 |
|---|---|
| 마우스 휠 1칸 | **220 px** |
| 마우스 휠 3칸 연속 | 660 px |
| 터치패드 (합계 300) | 300 px (그대로) |

> **`WHEEL_STEP` 과 `PAD_STEP` 을 나눠 둔 이유** — 마우스 휠은 한 칸에 100 안팎으로 크게 들어오고
> 터치패드는 20씩 잘게 여러 번 들어옵니다. 같은 배율을 곱하면 터치패드가 몇 배로 튑니다.
> 그래서 입력 크기(60 기준)로 구분해 다르게 적용합니다.

**아예 끄려면** `smoothScroll` 함수 첫 줄에 `return;` 을 넣으면 됩니다.
마우스가 있는 데스크톱에서만 동작하며, 휴대폰·태블릿은 이미 관성이 있어 건드리지 않습니다.

**적용됐는지 확인** — F12 → Console 에 이 줄이 떠야 합니다.

```
[부드러운 스크롤] 켜짐 — FOLLOW=0.06, WHEEL_STEP=2.2, PAD_STEP=1
```

### 등장 애니메이션 조절

| 하고 싶은 것 | 고칠 곳 |
|---|---|
| 전체를 더 빠르게/느리게 | `.rv` 의 `transition` 시간 (`1.05s` `1.15s`) |
| 등장 곡선 | `:root` 의 `--ease-out` |
| 카드가 하나씩 뜨는 간격 | `<div class="cards" data-stagger="110">` 의 숫자 (ms) |
| 첫 화면이 밀려 올라가는 정도 | JS `onScroll` 안의 `y * 0.16` |
| 애니메이션 끄기 | `<div class="rv">` 의 `rv` 클래스와 `data-stagger` 속성 제거 |

> OS 에서 “동작 줄이기(Reduce Motion)”를 켠 사용자에게는 애니메이션이 자동으로 꺼지고
> 모든 내용이 바로 보이게 되어 있습니다.

### 색 바꿔보기

```css
--accent:#14654a;    /* 딥 파인 그린 (현재) */
--accent-2:#2e9b6f;  /* 밝은 그린 — 강조·인터랙션 */
--accent-3:#0c3b2a;  /* 가장 진한 그린 — 제목·모달 헤더 */
```

세 줄을 같은 계열로 맞춰 바꾸면 톤이 유지됩니다.
