# O2B Lab — Lab Homepage

고려대학교 구로병원 외과학교실 **O2B Lab** (Operation-to-Bench Translational Oncology, Korea University) 공식 홈페이지 저장소입니다.

- **Live site**: https://kasaha11.github.io/o2blab/ (한국어: https://kasaha11.github.io/o2blab/?lang=ko)
- **Hosting**: GitHub Pages — `main` 브랜치에 push하면 자동 배포됩니다.

## 구조

정적 단일 페이지 사이트입니다. 빌드 과정이 없습니다.

```
site/
├── index.html          # 페이지 전체 (마크업 + CSS + JS 인라인)
├── robots.txt
├── sitemap.xml
├── .nojekyll           # GitHub Pages에서 Jekyll 처리 비활성화
└── assets/photos/      # 사진 (원본 + 웹 최적화본)
```

## 주요 기능

- **이중언어 (EN/KO)**: 모든 텍스트는 `data-en` / `data-ko` 속성 쌍으로 관리됩니다. 우측 상단 토글로 전환하며, 선택은 `localStorage`(`o2b-lang`)와 URL 쿼리(`?lang=ko`)에 반영됩니다. 텍스트를 수정할 때는 **두 속성을 모두** 고쳐야 합니다.
- **라이트/다크 모드**: CSS 변수 토큰(`:root`)으로 관리되며 `prefers-color-scheme`을 따릅니다. 색을 추가할 때는 다크 블록(`@media (prefers-color-scheme: dark)`)에도 대응 값을 넣어 주세요.
- **반응형**: 모든 사진은 `max-width:100%; height:auto` 전역 규칙과 `aspect-ratio` 컨테이너로 화면 크기에 맞춰 자동 조정됩니다.
- **접근성 / SEO**: 스킵 링크, 모바일 내비게이션(aria-expanded), hreflang, Open Graph, schema.org(ResearchOrganization) 구조화 데이터 포함.

## 로컬 미리보기

빌드가 필요 없으므로 아무 정적 서버로 열면 됩니다:

```bash
python3 -m http.server 8931
```

이후 http://localhost:8931 접속. (`file://`로 직접 열면 일부 상대 경로 이미지가 보이지 않을 수 있습니다.)

## 사진 추가 규칙

1. 원본을 `assets/photos/`에 두고, 웹에는 **최적화본**(JPEG 품질 ~60–72, 필요 시 WebP 병행)을 사용합니다.
   ```bash
   sips -s format jpeg --setProperty formatOptions 62 원본.png --out 최적화본.jpg
   ```
2. `<img>`에는 `width`/`height` 속성(CLS 방지)과 `loading="lazy" decoding="async"`를 붙입니다. 히어로처럼 처음 보이는 이미지는 `fetchpriority="high"`를 사용합니다.
3. WebP가 있으면 `<picture><source type="image/webp">` 패턴으로 감쌉니다.

## 콘텐츠 수정 위치 (index.html 내 섹션 id)

| 섹션 | id |
|---|---|
| 히어로 / 소속·CTA | `.hero` |
| 한눈에 보기 스트립 | `.glance` |
| 연구실 소개 | `#about` |
| 연구 분야 | `#research` |
| 연구비 | `#grants` |
| 책임교수 | `#pi` |
| 연구진 | `#team` |
| 논문 | `#publications` |
| 합류 안내 | `#join` |
| 연락처(푸터) | `#contact` |

## 문의

- Principal Investigator: Sanghee Kang, M.D., Ph.D. — kasaha1@korea.ac.kr
- ORCID: https://orcid.org/0000-0002-6097-8831
