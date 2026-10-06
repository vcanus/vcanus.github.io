# VCANUS 홈페이지 — 작업 규칙

이 레포 하나가 모든 언어의 홈페이지다 (www.vcanus.com, jekyll-polyglot, 2026-10-06 통합).
예전 한국어 레포(sglee-vcanus.github.io, www.vcanus.co.kr)는 통합 후 보관 대상이다.

## 언어 구조
- 언어 목록: `_config.yml` 의 `languages` · `language_names`. 기본(en)은 `/`, 나머지는 `/<lang>/`.
- 영어가 원문이다. 번역은 같은 폴더의 언어 하위 폴더에 같은 파일 이름으로 둔다.
  - `pages/about.md` → `pages/ko/about.md`, `pages/de/about.md`
  - `collections/_services/deepvi.md` → `collections/_services/ko/deepvi.md` …
  - 번역 파일 front matter 첫 줄은 `lang: <code>`. permalink 등 나머지 값은 원문과 같게.
- 번역이 없는 페이지는 영어 원문이 그 언어 경로로 대신 나간다 (블로그는 영어만).
- 메뉴·푸터·폼·주소 같은 공통 문구는 `_data/i18n.yml`. 메뉴는 `_data/menu.yml` 의 name 이 키.
- 글자가 들어간 이미지(SVG)는 `assets/images/gen/<lang>/…` 에 언어별로 둔다. 없으면 영어 그림을 쓴다.

## 정합 규칙
- 내용을 바꿀 때는 영어 원문과 모든 번역 파일을 함께 바꾼다 (제품 소개 자료 기반).
- 경쟁사 제품명·비교표는 쓰지 않는다. DeepVi 모델은 Fast / Standard 두 계열만 표기.
- 언어를 추가할 때: `languages` · `language_names` · `_data/i18n.yml` 에 한 벌씩, 그다음 페이지 번역.

## 빌드 · 배포
- master 에 머지되면 GitHub Actions(`.github/workflows/pages.yml`)가 빌드·배포한다. develop/master 로 가는 PR 은 빌드만.
- 로컬: Ruby 3.2 · `bundle exec jekyll serve`.
