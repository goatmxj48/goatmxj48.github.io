# CLAUDE.md

이 파일은 조민주 포트폴리오 사이트 저장소에서 클로드가 지켜야 할 규칙을 담는다.
개인 전역 규칙(`~/.claude/CLAUDE.md`)이 항상 위에 적용되고, 이 파일은 이 저장소에만 더해지는 규칙이다.

---

## 프로젝트 개요

서버 없이 동작하는 정적 웹 포트폴리오다. `index.html` 한 파일에 HTML·CSS·JS 가 모두 들어 있고,
화면 캡처는 `images/` 폴더에만 있다. 빌드 도구·패키지 매니저·프레임워크를 쓰지 않는다.

```
chominju-portfolio/
├── index.html      ← 페이지 전부 (구조 · 스타일 · 스크립트)
├── images/         ← 화면 캡처와 프로필 사진
├── README.md       ← 사용자용 사용 설명서 (이미지 넣는 법 · 배포 · 색 변경)
└── CLAUDE.md
```

`index.html` 안에서 찾을 위치

줄 번호는 고칠 때마다 밀리니 아래 표시를 검색해서 찾는다.

- `<style>` : 색·서체·여백 토큰이 맨 위 `:root` 에 모여 있다
- `<nav id="nav">` · `<header class="hero">` : 상단 내비게이션과 첫 화면
- `<section id="about">` 부터 : About / Career / Skills / Projects / Result / Contact
- `<div id="d1" data-title=` 부터 : 프로젝트 상세 내용 (`d1` ~ `d10`, 화면에서는 모달로 열린다)
- `<div id="lb"` : 이미지 크게 보기 (확대·이동·앞뒤 이미지)
- `<script>` : 부드러운 스크롤 · 등장 연출 · 모달 · 이미지 크게 보기

프로젝트 카드는 `<button class="pcard" data-detail="d1">` 이고, 그 `data-detail` 값이 상세 블록의 `id` 와 짝이 된다.
카드를 추가·수정할 때는 반드시 짝을 함께 맞춘다.

---

## 이 포트폴리오의 베이스는 GaiA-CaiRos 소스다

포트폴리오에 적힌 PMIS 관련 내용의 근거는 전부 아래 저장소의 실제 코드다.

```
D:\intellij\gaia-cairos
```

해당하는 카드 — 작업일지(`d1`) · 기성관리(`d8`) · 계약관리(`d9`) · 위험성평가(`d10`) ·
시스템 API 연계(`d2`) · 서비스 운영 및 장애 대응(`d3`)

이 내용을 새로 쓰거나 고칠 때는 **문장을 상상해서 만들지 않고 GaiA-CaiRos 소스와 업무 명세를 먼저 읽는다.**

- 업무 설명 근거 : `D:\intellij\gaia-cairos\claude-specs\docs\01_business\` 의 해당 메뉴 명세 파일
- 코드 근거 : 같은 저장소의 `comp` / `web` / `batch` 모듈
- 연동 규격·apiId : 같은 저장소의 연동 클라이언트와 연동 이력 규칙

근거를 찾지 못하면 문장을 만들지 말고 사용자에게 묻는다. 포트폴리오는 채용 담당자가 읽는 문서라
사실과 다른 한 줄이 남으면 되돌리는 비용이 크다.

---

## git 스토리는 develop 브랜치의 jomj@ideait.co.kr 만 조회한다

"내가 무슨 작업을 했는지", "이 기능 언제 했는지" 처럼 작업 이력을 근거로 삼아야 할 때는
GaiA-CaiRos 저장소에서 **develop 브랜치**의 **jomj@ideait.co.kr** 커밋만 본다.

```bash
cd /d/intellij/gaia-cairos
git log develop --author=jomj@ideait.co.kr --oneline
```

지키는 이유와 범위

- develop 이 팀 공용 상위 브랜치라 실제로 반영된 작업만 남는다. feature 브랜치에는 되돌린 시도와 중간 커밋이 섞여 있다
- 다른 사람 커밋은 포트폴리오 근거가 될 수 없다. 반드시 작성자 필터를 함께 준다
- `main` · `backup/*` · `feature/*` 브랜치는 이력 조회 대상이 아니다

자주 쓰는 형태

```bash
# 기간별로 무엇을 했는지
git log develop --author=jomj@ideait.co.kr --since=2026-06-01 --until=2026-08-31 --date=short --pretty=format:"%ad %s"

# 특정 메뉴 관련 이력
git log develop --author=jomj@ideait.co.kr --oneline --grep=위험성평가

# 특정 파일이나 폴더를 누가 언제 만졌는지
git log develop --author=jomj@ideait.co.kr --oneline -- comp/src/main/java/.../riskasmnt
```

커밋 메시지 앞의 `[mjjo]` 표기는 작성자 본인 커밋 표시다. 필터 결과를 교차 확인할 때 참고한다.

---

## 문구를 쓸 때

- 채용 담당자가 읽는 문서다. 클래스명·메서드명을 나열하지 않고 **그 일이 업무상 무엇을 해결했는지** 쓴다
- 숫자(연동 건수 · 서버 대수 · 기여도 · 기간)는 근거 없이 바꾸거나 새로 만들지 않는다
- 기존 카드의 문장 호흡과 어휘를 그대로 따른다. 카드마다 톤이 다르면 한 사람이 쓴 문서로 읽히지 않는다
- 상세 모달의 항목 구성(개요 → 한 일 → 결과)도 기존 블록과 같게 맞춘다

## 화면을 고칠 때

- 색은 `:root` 의 `--accent` 계열 세 줄만 만진다. 개별 규칙에 색을 직접 박지 않는다
- 스크롤·등장 연출 값은 `<script>` 맨 위 `FOLLOW` · `WHEEL_STEP` · `PAD_STEP` 한 줄에 모여 있다. 여기만 조절한다
- 라이브러리를 새로 넣지 않는다. 서체를 제외하면 외부 의존이 없는 상태를 유지한다
- 동작 줄이기(Reduce Motion)를 켠 사용자에게 애니메이션이 꺼지고 내용이 바로 보이는 동작을 깨지 않는다
- `README.md` 는 사용자가 직접 보는 설명서다. 구조나 조절 값을 바꿨으면 해당 표도 같이 고친다

## 이미지

- 파일은 `images/` 에만 둔다. 새 캡처를 넣으면 `<img>` 의 `alt` 를 업무 이름으로 적는다
- 자리만 잡아둔 초록 빗금 상자(`<div class="ph">`)는 캡처가 준비되면 통째로 지우고 아래 `<img>` 주석을 살린다
- 아직 비어 있는 자리와 채우는 방법은 `README.md` 1장에 정리돼 있다

---

## 하지 않는 것

- `git push` 는 어떤 상황에서도 실행하지 않는다 (전역 규칙 7장)
- `.md` 파일은 `git add` · `git commit` 하지 않는다. 수정한 경로만 보고하고 멈춘다 (전역 규칙 7-1장)
- GaiA-CaiRos 저장소의 파일을 이 작업 때문에 수정하지 않는다. 읽기만 한다
- 근거 없는 성과 문장·수치를 만들지 않는다

---

## 보고 형식

작업 결과는 항상 네 가지로 정리한다.

1. 변경 요약
2. 수정 파일 목록
3. Open Questions
4. Next actions

정적 파일이라 빌드가 없다. 대신 **무엇을 어떻게 확인했는지**(브라우저로 열어본 항목, 모달 열림, 반응형 폭)를 있는 그대로 적는다.
