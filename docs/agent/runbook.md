# runbook.md

## 검증 명령어

**E2E 테스트는 요청 시에만 실행합니다.**

| 단계 | 명령어 | 설명 |
|------|--------|------|
| lint | `npm run lint` | ESLint 코드 스타일 검사 |
| typecheck | `npx tsc --noEmit` | TypeScript 타입 검사 |
| build | `npm run build` | Contentlayer 변환 + Next.js 빌드 |
| dev 확인 | `npm run dev` | 로컬 개발 서버 (http://localhost:3000) |

> 이 프로젝트는 별도의 unit/integration 테스트 스위트가 없습니다. 검증은 lint → typecheck → build 순서로 진행합니다.

---

## 콘텐츠 작업 (MDX 포스트 추가/수정)

1. `data/blog/` 에 `.mdx` 파일 작성
2. frontmatter 필수 필드 확인: `title`, `date`
3. `npm run dev`로 로컬 확인
4. `npm run build`로 빌드 통과 확인

## 컴포넌트/레이아웃 작업

1. `components/` 또는 `layouts/` 파일 수정
2. `npm run lint` 통과 확인
3. `npx tsc --noEmit` 통과 확인
4. `npm run build` 통과 확인
5. `export_functions.md` 또는 `component_structure.md` 업데이트 (public API 변경 시)

---

## Git 작업 흐름

검증이 모두 통과된 후 진행합니다.

1. `git status` / `git diff --cached --stat` 으로 변경사항 파악
2. 변경 내용에 맞는 브랜치명으로 새 브랜치 생성 (`git checkout -b <branch>`)
3. 커밋 & push (`git push -u origin <branch>`)
4. 추가 수정 요청이 오면 수정 후 커밋 & push
5. PR 생성 (`gh pr create`)
6. CI 전체 통과 대기 (`gh pr checks <number> --watch`)
7. 통과하면 머지 & 리모트 브랜치 삭제 (`gh pr merge <number> --merge --delete-branch`)
8. 로컬 브랜치 정리 (`git checkout main && git pull origin main && git branch -d <branch>`)

---

## 주의사항

- `contentlayer.config.ts` 스키마 변경 시 반드시 빌드 재실행 (`.contentlayer/` 캐시 무효화)
- `data/siteMetadata.js` 변경은 전역 영향 — 빌드 후 전체 페이지 확인
- `draft: true` 포스트는 빌드에서 제외됨 (로컬 dev에서도 확인 불가)
