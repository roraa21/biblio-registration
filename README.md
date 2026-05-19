# 온라인 서점 서지 등록 자동화 페이지

비상교육 AIDT 플랫폼마케팅팀의 온라인 서점 서지 등록 업무를 자동화하는 단일 페이지 웹 도구입니다.

## 주요 기능

- **서지정보 입력 → 워드(.docx) 자동 생성**
  교재 소개 등록 요청서 양식 그대로 표 구조의 워드 파일로 출력
- **교재 표지 4종 자동 분리**
  전체 펼침면 1장을 업로드하면 슬라이더로 분할 지점을 시각적으로 조정해
  앞표지·뒷표지·세네카·전체 이미지 4종을 원본 화질 그대로 추출
- **3단계 교재 선택 캐스케이드**
  교재 구분(초/중/고) → 과목 → 교재명 순서로 선택
- **상세 이미지 업로드**
  온라인 서점 상세페이지용 세로 긴 이미지 등록
- **ZIP 패키지 다운로드 · 메일 발송**
  서지정보·표지·상세 이미지를 한 폴더로 묶어 다운로드 또는 메일 앱 호출
- **등록 이력 영구 저장**
  브라우저 `localStorage` 기반으로 등록 이력 자동 기록 및 재불러오기

## 메뉴 구조

```
01. 서지정보 등록       — 교재 소개 등록 요청서 항목 입력
02. 표지 이미지 등록    — 교재 선택 + 펼침면 → 4종 자동 분리
03. 상세 이미지 등록    — 상세페이지 이미지 업로드
04. 패키지·메일 발송    — ZIP 다운로드 / 메일 앱 발송
05. 등록 내역 조회      — 이력 목록 / 재불러오기 / 삭제
```

## 사용 방법

### 로컬에서 실행

`index.html` 파일을 브라우저로 바로 열면 됩니다. 빌드 과정이 필요 없습니다.

```bash
# macOS
open index.html

# Windows
start index.html

# Linux
xdg-open index.html
```

### 정적 호스팅 배포

빌드가 필요 없는 단일 HTML이므로 어디든 그대로 올리면 됩니다.

#### GitHub Pages

1. 저장소 Settings → Pages
2. Source: `Deploy from a branch`
3. Branch: `main` / `/ (root)` 선택 → Save
4. 배포 URL: `https://<유저명>.github.io/<저장소명>/`

> **참고**: 저장소 root에 빈 `.nojekyll` 파일이 포함되어 있어
> GitHub Pages가 Jekyll 빌드를 건너뛰고 정적 파일을 그대로 서빙합니다.
> 이 파일이 없으면 "Package a Jekyll site..." 같은 빌드 에러가 발생할 수 있습니다.

#### Netlify

1. [Netlify](https://app.netlify.com/) 로그인 → "Add new site" → "Import from Git"
2. GitHub 저장소 연결
3. Build command: 비워두기
4. Publish directory: `/` (또는 `.`)
5. Deploy

## 기술 스택

- 순수 HTML / CSS / Vanilla JavaScript
- [JSZip](https://stuk.github.io/jszip/) — ZIP 패키지 생성 (CDN)
- [docx](https://docx.js.org/) — 워드 파일 생성 (CDN)
- 외부 폰트: Fraunces, Pretendard, JetBrains Mono (Google Fonts CDN)

별도의 빌드 시스템·번들러·백엔드 의존성이 없습니다.

## 교재 마스터 데이터 수정

`index.html` 안의 `BOOK_DATA` 객체에서 교재 라인업을 관리합니다.

```javascript
const BOOK_DATA = {
  '초': {
    '국어': ['완자 초등 국어 1-1', ...],
    '수학': [...],
    ...
  },
  '중': { ... },
  '고': { ... }
};
```

추후 Google Sheets CSV 연동으로 교체할 수 있습니다.

## 브라우저 호환성

- Chrome / Edge / Safari / Firefox 최신 버전
- 모바일 브라우저에서도 동작하나 데스크탑 사용을 권장 (이미지 분할 UI는 화면이 클수록 편리)

## 라이선스

비상교육 내부 운영 도구.
