# index.md

## 프로젝트 개요

Next.js 15 + Contentlayer2 기반 개인 기술 블로그 (Tailwind CSS, MDX 포스트)

## 언어 / 프레임워크 버전

- Node.js: 22.22.2
- TypeScript: 5.9.x
- Next.js: 15.5.12
- React: 19.2.4
- Contentlayer2: 0.5.8
- Tailwind CSS: 4.x
- 패키지 매니저: npm

## 폴더 구조

```
├── app/                  # Next.js App Router (page, layout, blog, about, projects, tags)
├── components/           # 공통 UI 컴포넌트
├── layouts/              # 포스트/목록 레이아웃
├── data/
│   ├── blog/             # MDX 블로그 포스트
│   ├── authors/          # 저자 정보 MDX
│   ├── siteMetadata.js   # 전역 사이트 설정
│   └── projectsData.ts   # 프로젝트 목록
├── public/static/        # 이미지 등 정적 파일
├── css/                  # 전역 스타일
├── scripts/              # postbuild 등 유틸 스크립트
├── contentlayer.config.ts# Contentlayer 스키마 정의
└── docs/                 # 에이전트용 프로젝트 문서
```

## 문서 목록

- [페이지 목록](shared/pages.md)
- [DB 스키마](backend/db_schema.md)
- [API 명세](backend/api_spec.md)
- [Export 함수명](shared/export_functions.md)
- [컴포넌트 구조](frontend/component_structure.md)
- [디자인](frontend/design.html)
- [아키텍처](shared/architecture.md)
- [검증 절차](agent/runbook.md)
- [완료 조건](agent/done_condition.md)
