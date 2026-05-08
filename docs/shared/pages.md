# pages.md

## 페이지 목록

| 경로 | 페이지명 | 설명 | 인증 필요 |
|------|---------|------|----------|
| `/` | 홈 | 최신 블로그 포스트 5개 + Newsletter 폼 | 아니오 |
| `/blog` | 블로그 목록 | 전체 포스트 목록, 검색 기능 포함 | 아니오 |
| `/blog/[...slug]` | 블로그 상세 | MDX 포스트 렌더링, 댓글(Giscus) | 아니오 |
| `/blog/page/[page]` | 블로그 목록 (페이지네이션) | 5개/페이지 | 아니오 |
| `/about` | 어바웃 | 저자 프로필 (authors/default.mdx 렌더링) | 아니오 |
| `/projects` | 프로젝트 | 프로젝트 카드 갤러리 (projectsData.ts 기반) | 아니오 |
| `/tags` | 태그 목록 | 전체 태그 + 포스트 수 | 아니오 |
| `/tags/[tag]` | 태그별 포스트 | 특정 태그로 필터링된 포스트 목록 | 아니오 |
| `/tags/[tag]/page/[page]` | 태그별 포스트 (페이지네이션) | 5개/페이지 | 아니오 |

> 현재 인증이 필요한 페이지 없음. 모든 콘텐츠 공개.

---

## 화면 흐름

```
홈(/)
├─ "All Posts" 링크 → /blog
└─ 포스트 제목 클릭 → /blog/[slug]

블로그 목록(/blog)
├─ 포스트 클릭 → /blog/[slug]
├─ 태그 클릭 → /tags/[tag]
└─ 페이지네이션 → /blog/page/[page]

블로그 상세(/blog/[slug])
├─ 태그 클릭 → /tags/[tag]
├─ Prev/Next 포스트 링크
└─ 댓글 (Giscus, GitHub Discussions)

태그 목록(/tags)
└─ 태그 클릭 → /tags/[tag]

태그별 목록(/tags/[tag])
├─ 포스트 클릭 → /blog/[slug]
└─ 페이지네이션 → /tags/[tag]/page/[page]
```

---

## 레이아웃 종류

포스트별로 frontmatter의 `layout` 필드로 선택.

| layout 값 | 파일 | 특징 |
|-----------|------|------|
| `PostLayout` (기본) | `layouts/PostLayout.tsx` | 저자 정보, prev/next, 태그, 댓글 |
| `PostSimple` | `layouts/PostSimple.tsx` | 최소 레이아웃 |
| `PostBanner` | `layouts/PostBanner.tsx` | 상단 배너 이미지 |
