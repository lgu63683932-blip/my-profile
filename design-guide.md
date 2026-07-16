# 자기소개 홈페이지 디자인 가이드

에디토리얼 톤의 개인 자기소개 페이지 디자인 시스템. 다른 사람의 자기소개 페이지를 만들 때 이 문서를 프롬프트로 붙여넣어 재사용한다.

## 폰트

- **본문**: Noto Sans KR (weight 400 기본, 강조 시 500/700) — 산세리프, 가독성 중심
- **포인트 세리프**: Cormorant Garamond (weight 300/400/600) — 로고, 섹션 번호, 연도·날짜, 히어로 제목 강조(이탤릭)에만 사용
- Google Fonts CDN 로드, `<head>`에 `preconnect` 2줄 포함

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&family=Cormorant+Garamond:wght@300;400;600&display=swap" rel="stylesheet">
```

## 색상 (라이트 / 다크 자동 대응)

| 역할 | 라이트 | 다크 |
|---|---|---|
| 배경 | `#F5F2EC` (웜 크림) | `#1A1917` |
| 카드 배경 | `#FFFFFF` | `#22211E` |
| 본문 글자 | `#1C1C1C` | `#EDEAE3` |
| 보조 글자 | `#4A463E` | `#C3BEB0` |
| 테두리 | `#DFD9CF` | `#3A382F` |
| 포인트(악센트) | `#2F4F3E` (딥 그린) | `#8FCBAA` |
| CTA 버튼 3색 | 앰버 `#E8B23D` · 코랄 `#E07856` · 틸 `#6FB3AA` | 동일 |

`prefers-color-scheme: dark` 미디어쿼리로 CSS 변수만 교체하는 방식.

## 폰트 크기 체계

| 요소 | 크기 / 굵기 | 비고 |
|---|---|---|
| 히어로 제목 (h1) | 76px / 300 | 모바일 52px |
| 히어로 부제 (h3) | 18px / 500 | |
| 히어로 소개문 | 17px | 보조색 |
| 섹션 번호 (01, 02…) | 25px / 600 | 세리프 |
| 섹션 제목 (h2) | 28px / 400 | |
| 본문 문단 | 16px | |
| 경력 날짜 | 21px / 600 | 세리프 |
| 경력 역할명 | 17px / 500 | |
| 경력 설명 | 15px | 보조색 |
| 성과 카드 연도 | 17px / 600 | 세리프 |
| 성과 카드 제목 | 17px / 500 | |
| 성과 카드 설명 | 14px | 보조색 |
| 역량 카드 | 15px / 500 | |
| Focus 리스트 | 16px | 굵은 리드 문구 + 설명 |
| 연락처 라벨 | 13px | 대문자 |
| eyebrow 라벨 | 18px / 700 | letter-spacing .35em, 대문자 |

## 레이아웃 구성 (섹션 순서)

1. **상단 고정 네비(sticky nav)** — 로고(좌) + Resume / Projects / Contact 3개 링크(우), 배경 반투명 블러
2. **히어로** — 사진(원형 아님, 둥근 사각형 + 그림자, 실제 비율 유지) + eyebrow 라벨 + 큰 제목 + 소개문 + 원형 CTA 버튼 3개(컬러풀)
3. **소개** — 섹션 번호+제목 + 2~3문단 본문
4. **경력** — 세로 타임라인(날짜 | 역할 + 설명), 구분선, 현재 항목엔 "현재" 배지
5. **주요 성과** — 2열 카드 그리드, 최신/진행중 항목이 맨 앞
6. **역량** — 한 줄 카드 그리드(둥근 모서리, 짧은 키워드, 단어 안 잘림)
7. **지금 하고 있는 일** — 굵은 리드 문구 + 설명의 리스트, 왼쪽에 작은 틱 마크
8. **Contact** — 라벨-값 박스 리스트 (Email 등)
9. **Footer** — 한 줄 태그라인

## 레이아웃 시스템

- 최대 콘텐츠 폭 1080px, 좌우 패딩 40px (모바일 24px)
- 섹션 세로 패딩 80px (모바일 56px), 섹션 사이 하단 구분선(`border-bottom`)
- 카드/역량/타임라인 모두 `border-radius: 16~20px`로 둥글게
- 반응형 분기점 760px: 히어로 세로 스택, 그리드 1열, 네비 메뉴 숨김, CTA 원 축소(88px)

## 기술적 디테일 (재사용 가치 높음)

- `word-break: keep-all` + `overflow-wrap: break-word`를 `body`에 적용 → 한글 단어 중간 줄바꿈 방지
- 사진에 `aspect-ratio` 고정 + `overflow-anchor: none` → 이미지 로딩 중 레이아웃 밀림 방지
- 해시(`#섹션`)가 붙은 URL로 재방문해도 항상 맨 위부터 보이도록, `<head>`에서 동기적으로 해시 제거 + `DOMContentLoaded`/`load` 시점에 `scrollTo(0,0)` 실행
- `history.scrollRestoration = 'manual'`로 브라우저의 스크롤 위치 자동 복원 방지

## 재사용 프롬프트 예시

> "위 디자인 가이드(design-guide.md) 톤과 동일하게, [이름/직업/소개] 정보로 자기소개 페이지를 만들어줘. 히어로엔 사진+eyebrow 라벨+큰 제목+CTA 버튼 3개, 그 아래 소개/경력/주요 성과/역량/지금 하는 일/Contact 섹션 구성으로."
