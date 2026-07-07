# Growth Design Lab 홈페이지

## 프로젝트 개요
- **결과물**: `growth-design-lab/index.html` — Growth Design Lab™ 원페이지 홈페이지 (단일 파일, 빌드 도구 없음)
- **브랜드 기준**: Growth Frame™ 브랜드 구조도 (Mission·Vision·Philosophy·Thinking 5원칙·Methodology 구조)
- **원격 저장소**: https://github.com/rusolee76/testBOS.git (`main` 브랜치) — **`growth-design-lab/` 폴더의 파일만 커밋/푸시**. 루트의 PDF·DOCX·PPTX·XLSX는 대외비, 절대 add 금지.
- ROBOS 리뉴얼(`robos-renewal/`, 루트 `index.html`)과는 **별개 프로젝트**. 서로 파일을 섞지 않는다.

## 환경 제약 (중요)
- 이 PC에는 **Node·Python·pandoc·gh CLI가 없다.** npm·빌드 스크립트·프레임워크 도입 금지 — 순수 HTML/CSS/JS 단일 파일 유지.
- 수정 후 파일이 Launch 프리뷰 패널에 자동 표시된다.
- 폰트는 SUIT Variable(jsDelivr CDN). 오프라인이면 시스템 폰트로 폴백 — CDN 링크를 제거하지 말 것.

## 파일 구조 (index.html 내부)
HTML 주석 마커(`<!-- ============ 이름 ============ -->`)로 섹션 구분. 순서대로:

| 마커 | 내용 | 앵커 |
|---|---|---|
| `NAV` | 고정 헤더 (로고 심볼+로고타이프 SVG, 5메뉴, 진단 문의 버튼) | — |
| `HERO` | 헤드라인 4줄(라인 리프트 모션) + 지표 3종 카운터 + 파티클 | `#top` |
| `SIGNATURE` | 인용 밴드 + 좌우 라인아트 장식 | — |
| `IDENTITY` | Growth/Design/Lab 3카드 | `#identity` |
| `MISSION / VISION` | 다크 네이비 2카드 | `#mission` |
| `PHILOSOPHY` | WHY→BELIEF→THEORY→MISSION 4카드 흐름 | `#philosophy` |
| `THINKING` | 5원칙 리스트 + 우측 궤도 휠(로고 중심, P1~P5 회전) | `#thinking` |
| `METHODOLOGY` | 세로 플로우: Lab→Mission→Philosophy→Design→Audit→도구3종→Blueprint→Alignment→Profit Engine | `#methodology` |
| `USP` | 23 YEARS 카운터 + 성장 바 차트 + 포인트 3종 | — |
| `CTA` | 그린 그라디언트 문의 밴드 | `#contact` |
| `FOOTER` | 로고 + 링크 + 카피라이트 | — |

- **CSS**: `<head>` 안 단일 `<style>`. 디자인 토큰은 최상단 `:root`. 반응형 분기: 1020px / 900px / 680px.
- **JS**: `</body>` 직전 단일 `<script>`. 순서: 프로그레스 바 → 파티클 → 스크롤 리빌 → draw/grow 트리거 → 궤도 회전 → 카운터 → 모바일 메뉴.

## 디자인 토큰 (변경 금지)
```
--navy:#0D1B2A(메인)  --green:#10A36A(액센트)  --green-2:#0FBF7C(밝은 그린, 다크 배경 위)
--off:#F6F8FA(밝은 섹션 배경)  --line:#E3E9EF(보더)
폰트: SUIT Variable 단일. 웨이트로만 위계 표현(800 타이틀 / 600~700 본문 강조).
```
- **딥네이비 + 에메랄드 2색 원칙. 새 색상 추가 금지.** 섹션 배경은 white ↔ off ↔ navy 교차.
- 사진·스톡·AI 생성 이미지 넣지 않는다(사용자 확정 방침). 시각 요소는 전부 브랜드 컬러 인라인 SVG.

## 로고 (사용자 확정 — 임의 변형 금지)
- **심볼**: 열린 프레임 + 그린 바 2개. 단일 패스로 통일되어 3곳에 존재 — GNB, 푸터, Thinking 궤도 휠 중앙.
  ```
  <path d="M36 64 L168 16 L168 150 L144 143 L144 44 L62 72 L62 178 L88 196 L36 186 Z"/>
  <rect x="96" y="118" width="18" height="84"/> <rect x="120" y="90" width="20" height="108"/>
  ```
  다크 배경에서는 프레임만 `#F1F4FA`로 반전, 바는 항상 `#10A36A`. **세 곳의 패스는 항상 동일해야 한다.**
- **로고타이프**: `.brand-lt` — 전부 SVG 패스(폰트 아님). GROWTH(lt1) 크게, DESIGN LAB(lt2) 작게·그린, 가운데 정렬.
  - **W 규칙**: VV 오버랩 구조에서 **첫 번째 V의 업스트로크 획 전체가 그린(#10A36A)**. 일부만 그린으로 하거나 위치를 바꾸지 말 것.
- 수정 시 GNB·푸터 두 곳을 항상 동시에 갱신.

## 모션 파라미터 (확정값 — 임의 변경 금지)
- 스크롤 리빌: `.rv`(위로), `.rv-l`/`.rv-r`(좌우) — 60ms 스태거, IntersectionObserver threshold .15
- 히어로 헤드라인: 라인별 마스크 리프트 .85s, 130ms 간격, 그린 밑줄 스윕 1.15s 딜레이
- 카운터: `.cnt` 1.2s ease-out cubic
- 라인 드로잉 `.draw` / 바 성장 `.grow`: 뷰포트 35% 진입 시 1회 재생
- 궤도 휠: 회전 속도 0.0022 rad/frame
- ⚠️ **마퀴(무한 흐름 배너)는 사용자가 명시적으로 제거함 — 재추가 금지.**

## 콘텐츠 가드레일 (사용자 확정)
1. **"식품·외식" 표현 전면 금지** — 산업 한정 없이 "기업"으로 표기 (Mission·Vision·태그라인 포함 전체).
2. 히어로 우측 일러스트(Growth Audit 대시보드 그래프)는 사용자가 제거함 — 재추가 금지. 히어로는 텍스트+지표 중심.
3. 확정 카피 (임의 수정 금지):
   - 시그니처: "우리는 성장을 컨설팅하지 않습니다. 성장이 작동하는 구조를 설계합니다."
   - 인용 밴드: "성장이 멈추는 이유는 성장을 제한하는 병목이 존재하기 때문입니다."
   - 지표: 23년 실전 경험 / 5대 원칙 / 1개의 목표(Sustainable Profit Engine™)
4. 상표 표기: Growth Design Lab™, Growth Audit™ 등 **™ 유지**. 방법론 명칭은 영문 그대로 + 한글 부연.
5. 문의 이메일 `contact@growthdesignlab.com`은 플레이스홀더 — 실제 주소 확정 시 CTA와 푸터에서 교체.

## 자주 하는 편집 레시피
- **지표 수치 변경**: `.cnt`의 `data-to` 값 수정. 히어로 3종 + USP의 23(2곳 존재 여부 확인).
- **원칙 추가/수정**: THINKING 섹션 `.pr` 블록 복제 (`.pic` 아이콘 SVG + `.tx`의 Principle 번호·문장). 궤도 휠 노드(P1~P5)의 개수·라벨도 함께 갱신.
- **방법론 단계 수정**: METHODOLOGY의 `.fl`(solid=네이비/line=그린 보더, 교차 배치) + `.fl-arrow` 쌍으로 편집. 진단 도구 3종은 `.fl-tools` 그리드.
- **픽토그램 추가**: 24×24 viewBox, `fill="none" stroke-width="1.8~1.9" stroke-linecap="round"` 라인 아이콘으로 통일. 색은 컨텍스트에 따라 currentColor/그린/화이트.
- **섹션 추가**: 기존 마커 형식을 따르고, 배경색은 인접 섹션과 교차(white↔off↔navy)시킬 것. 리빌 클래스(`.rv` 계열) 부착.
- **모바일 확인**: 680px(1열 전환), 900px(햄버거 메뉴), 1020px 분기 3곳을 모두 확인.

## 작업 절차
1. 수정 전 해당 섹션 주석 마커를 Grep으로 찾아 그 범위만 Edit.
2. 카피·수치 변경 시 같은 값이 여러 곳에 있는지 검색해 일관성 유지 (예: 로고 2곳, 23년 2곳).
3. 커밋 메시지는 한국어 요약. `git status`로 `growth-design-lab/` 외 파일(특히 대외비 문서)이 staged되지 않았는지 확인 후 push.
