# export_functions.md

## 페이지 컴포넌트

| 파일 | export명 | URL | 설명 |
|------|----------|-----|------|
| `app/page.tsx` | `HomePage` (default) | `/` | 홈 (최신 5개 포스트) |
| `app/blog/page.tsx` | `BlogPage` (default) | `/blog` | 블로그 목록 |
| `app/blog/[...slug]/page.tsx` | `Page` (default) | `/blog/[slug]` | 포스트 상세 |
| `app/blog/page/[page]/page.tsx` | `Page` (default) | `/blog/page/[n]` | 블로그 페이지네이션 |
| `app/about/page.tsx` | `Page` (default) | `/about` | 어바웃 |
| `app/projects/page.tsx` | `Page` (default) | `/projects` | 프로젝트 |
| `app/tags/page.tsx` | `Page` (default) | `/tags` | 태그 목록 |
| `app/tags/[tag]/page.tsx` | `Page` (default) | `/tags/[tag]` | 태그별 포스트 |
| `app/tags/[tag]/page/[page]/page.tsx` | `Page` (default) | `/tags/[tag]/page/[n]` | 태그별 페이지네이션 |

---

## API Route Handlers

| 파일 | export명 | HTTP | URL |
|------|----------|------|-----|
| `app/api/newsletter/route.ts` | `POST` (named) | POST | `/api/newsletter` |
| `app/robots.ts` | `robots` (default) | GET | `/robots.txt` |
| `app/sitemap.ts` | `sitemap` (default) | GET | `/sitemap.xml` |

---

## 레이아웃 컴포넌트

| 파일 | export명 | 타입 | 설명 |
|------|----------|------|------|
| `layouts/PostLayout.tsx` | `PostLayout` (default) | default | 포스트 기본 레이아웃 |
| `layouts/PostSimple.tsx` | `PostSimple` (default) | default | 포스트 심플 레이아웃 |
| `layouts/PostBanner.tsx` | `PostBanner` (default) | default | 포스트 배너 레이아웃 |
| `layouts/ListLayout.tsx` | `ListLayout` (default) | default | 포스트 목록 레이아웃 |
| `layouts/ListLayoutWithTags.tsx` | `ListLayoutWithTags` (default) | default | 포스트 목록 + 태그 사이드바 |
| `layouts/AuthorLayout.tsx` | `AuthorLayout` (default) | default | 저자 프로필 레이아웃 |

---

## 공유 컴포넌트

| 파일 | export명 | 타입 | 설명 |
|------|----------|------|------|
| `components/Header.tsx` | `Header` (default) | default | 전역 헤더 |
| `components/Footer.tsx` | `Footer` (default) | default | 전역 푸터 |
| `components/Link.tsx` | `Link` (default) | default | 내/외부 링크 핸들러 |
| `components/MobileNav.tsx` | `MobileNav` (default) | default | 모바일 메뉴 |
| `components/ThemeSwitch.tsx` | `ThemeSwitch` (default) | default | 테마 토글 |
| `components/SearchButton.tsx` | `SearchButton` (default) | default | 검색 버튼 |
| `components/Tag.tsx` | `Tag` (default) | default | 태그 링크 |
| `components/Card.tsx` | `Card` (default) | default | 프로젝트 카드 |
| `components/Image.tsx` | `Image` (default) | default | Next.js Image 래퍼 |
| `components/PageTitle.tsx` | `PageTitle` (default) | default | 페이지 h1 제목 |
| `components/Comments.tsx` | `Comments` (default) | default | Giscus 댓글 |
| `components/ScrollTopAndComment.tsx` | `ScrollTopAndComment` (default) | default | 스크롤 상단/댓글 버튼 |
| `components/TableWrapper.tsx` | `TableWrapper` (default) | default | 스크롤 가능한 테이블 래퍼 |
| `components/LayoutWrapper.tsx` | `LayoutWrapper` (default) | default | Header + Footer 래퍼 |
| `components/SectionContainer.tsx` | `SectionContainer` (default) | default | 최대 너비 컨테이너 |
| `components/MDXComponents.tsx` | `components` (default) | default | MDX 커스텀 컴포넌트 맵 |
| `components/social-icons/index.tsx` | `SocialIcon` (default) | default | 소셜 아이콘 |

---

## 유틸리티 / 설정

| 파일 | export명 | 타입 | 설명 |
|------|----------|------|------|
| `app/seo.tsx` | `genPageMetadata` | named | 페이지별 metadata 생성 |
| `app/theme-providers.tsx` | `ThemeProviders` (default) | default | next-themes Provider |
| `data/siteMetadata.js` | `siteMetadata` (default) | default | 사이트 전역 설정 |
| `data/headerNavLinks.ts` | `headerNavLinks` (default) | default | 네비게이션 링크 배열 |
| `data/projectsData.ts` | `projectsData` (default) | default | 프로젝트 데이터 배열 |

> - **default**: `import X from '...'`
> - **named**: `import { X } from '...'`
>
> 컴포넌트·함수 추가 시 이 문서를 함께 업데이트할 것.
