# ROBOS 홈페이지 리뉴얼 프로젝트

## 프로젝트 개요
- **결과물**: `robos-renewal/index.html` — ROBOS Re:Branding 2026 원페이지 홈페이지 (단일 파일, 빌드 도구 없음)
- **목적**: IPO(기술특례 상장) 대비 리뉴얼. TECH·확장성 강조.
- **원격 저장소**: https://github.com/rusolee76/testBOS.git (`main` 브랜치)
- **기준 문서**: `ROBOS_홈페이지_취합본_정리_v5.docx`(콘텐츠 설계서) · `[Total] 260205_Branding_BS_V1.1.pdf`(브랜딩)
- ⚠️ 저장소에는 **`robos-renewal/` 폴더만 커밋**한다. 루트의 PDF·DOCX·PPTX·XLSX는 전부 대외비 — 절대 add/push 금지.

## 환경 제약 (중요)
- 이 PC에는 **Node·Python·pandoc·gh CLI가 없다.** npm install, 빌드 스크립트, 프레임워크 도입 금지 — 순수 HTML/CSS/JS 단일 파일 유지.
- docx 텍스트 추출이 필요하면 PowerShell + System.IO.Compression으로 zip을 직접 읽는다.
- 수정 후 검증: 파일이 Launch 프리뷰 패널에 자동 표시된다. 브라우저 도구 연결 시 file:// 로 열어 콘솔 에러 확인.

## 파일 구조 (index.html 내부)
HTML 주석 마커로 섹션이 구분되어 있다. 순서대로:

| 마커 | 섹션 | 앵커 |
|---|---|---|
| `<!-- GNB -->` | 고정 헤더 (로고 SVG + 6메뉴 + IR 문의) | — |
| `<!-- ① HERO -->` | LiDAR 캔버스 + 라이트빔 + 헤드라인 | `#top` |
| `<!-- ② METRIC STRIP -->` | 핵심 지표 6종 카운터 | — |
| `<!-- ③④ ROBOS -->` | 시장 4카드 · 진화 4단계 · 왜 로보스 3카드 | `#robos` |
| `<!-- ⑤ TECH -->` | 기술 3축 · 프로세스 5단계 · 비교표 · 플라이휠 | `#tech` |
| `<!-- ⑥ BUSINESS -->` | 4단계 레일 · 제품 Overview(필터) | `#business` |
| `<!-- ⑦ PERFORMANCE -->` | 고객사 네트워크 SVG · 수상 5 | `#performance` |
| `<!-- ⑧ INVESTORS -->` | 투자 포인트 · 매출 차트 · IPO 로드맵 · 관리체계 | `#investors` |
| `<!-- 회사 -->` | 핵심가치 · 연혁 · 개요 · 뉴스/채용 | `#company` |
| `<!-- CTA BAND -->` / `<!-- FOOTER -->` | 공통 하단 | — |

- **CSS**: `<head>` 안 단일 `<style>`. 디자인 토큰은 최상단 `:root`.
- **JS**: `</body>` 직전 단일 `<script>`. 데이터(제품 배열 등)와 모션 로직이 여기에 있다.

## 디자인 토큰 (브랜딩 BS V1.1 — 변경 금지)
```
--black:#0C0C0C  --white:#F1F4FA  --gray:#A5B4C6  --blue:#1F51FF(액센트, 절제 사용)
폰트: Pretendard(국문) + Satoshi(영문 타이틀·수치, class="en")
```
- 모노톤 + 블루 액센트 원칙. 새 색상 추가 금지.
- 카드류는 `.frame` 클래스(모서리 컷 Expand Frame 모티프)를 재사용한다.
- 영문·숫자에는 `class="en"`(Satoshi)을 붙인다.

## 자주 하는 편집 레시피
- **지표 수치 변경**: `.cnt` 요소의 `data-to` 값 수정 (`data-dec`=소수 자릿수). 예: 일일 학습 데이터 = `data-to="28000"`.
- **제품 추가/삭제**: `<script>`의 `const PRODUCTS=[...]` 배열 수정. 필드: `c`(코드) `n`(명칭) `g`(pig/cattle/meat) `s`(sale/done/dev/plan) `y`(연도 표기) `p`(진행바 %). 필터 버튼의 개수 표기(`전체 9` 등)와 섹션 타이틀(`— 9종`)도 함께 갱신할 것.
- **뉴스 추가**: `#company`의 `.news-item` 블록 복제. 원문 URL 확보 전에는 `href="#" onclick="return false"`.
- **매출 차트**: `#chart`의 `.bar` — `data-h`(높이 %, 최대값 기준)와 `.v` 라벨. 목표치는 `bar target` 클래스(점선 패턴) 유지.
- **연혁 추가**: `.tl-item` 블록 복제 (연도 `.yr` + 본문 `.bd`).
- **모션 파라미터**: 리빌 60ms 스태거·카운터 1.2s·페이드업 24px/0.4s — v5 설계서 확정값이므로 임의 변경하지 않는다.

## 콘텐츠 가드레일 (컴플라이언스 — v5 설계서 '결정 필요' 승계)
1. **'국내 최초' 표현 금지** → '국내 유일의 상용화 실적' 사용 (표시광고법 리스크).
2. 경쟁사 실명(Marel·Frontmatec) 금지 → '글로벌 경쟁사'.
3. 해외 파트너 실명(Smithfield 등) 금지 → '글로벌 톱티어 팩커사'.
4. 재무는 **매출 추이만** 게시. 수주액·영업이익·투자금액·기업가치 게시 금지. '26년 수치는 반드시 '목표' 명기 + 실적과 시각 구분(점선).
5. IPO 로드맵에 밸류에이션·펀딩 금액 게시 금지 (단계 × 기술 자산만).
6. 고객사는 텍스트 사명만 (로고는 동의 확보 전 금지).
7. 스마트팩토리 거점은 '전국 7개 거점 목표'까지만 (지역 실명 금지).

## 확정된 카피 (임의 수정 금지 — 사용자 확정본)
- 히어로/CTA 밴드: "In the Dark, We Are the Light" (We See New Possibilities 아님)
- Company 헤드라인: "In the Dark, We are the Light" / 설명: "어둠 속에서, 우리가 그 빛이 됩니다. 2022년 설립 이후, ROBOS는 비정형 산업을 Data로 재정의하여, 산업에 지속생존이라는 빛을 비추고 있습니다."
- 사업 타이틀: "단품에서 확장성장으로 — 4단계 확장 구조" / STAGE 3 = "자가운영모델" / STAGE 4 = "분야확장"
- 일일 학습 데이터 = 28,000+(지표 스트립) / 2.8만+(DATA MOAT·기술 카드)
- 제품 Overview는 9종만 노출: 상용화 7종(PNC·PBO·PBD·PSP·PWC·CSP·CWC) + 개발완료 2종(PCS·포장자동화). 개발중/예정 제품 재추가 금지(상용화 승격 시에만).

## 작업 절차
1. 수정 전 해당 섹션 주석 마커를 Grep으로 찾아 그 범위만 Edit.
2. 수치·카피 변경 시 같은 값이 여러 곳에 있는지 검색해 일관성 유지 (예: 학습 데이터 건수는 3곳).
3. 커밋 메시지는 한국어로 변경 요지 요약. `robos-renewal/` 외 파일이 staged되지 않았는지 `git status`로 확인 후 push.
