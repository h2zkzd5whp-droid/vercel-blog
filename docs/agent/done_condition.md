# done_condition.md

## 공통 완료 조건

- [ ] 요청된 기능이 구현됐다
- [ ] 변경이 관련 문서를 따른다
- [ ] lint 통과 (`npm run lint`)
- [ ] typecheck 통과 (`npx tsc --noEmit`)
- [ ] build 통과 (`npm run build`)
- [ ] 관련 없는 파일이 수정되지 않았다
- [ ] 계약 변경이 있으면 문서에 반영됐다

---

## 작업 유형별 추가 조건

### 프론트엔드 작업 (컴포넌트/레이아웃)

- [ ] 컴포넌트 구조가 `component_structure.md`와 일치한다
- [ ] public API(props, export명) 변경 시 `export_functions.md` 업데이트됐다
- [ ] `npm run dev`로 로컬 렌더링 확인했다

### 콘텐츠 작업 (MDX 포스트/저자)

- [ ] frontmatter 필수 필드(`title`, `date`) 존재한다
- [ ] `npm run build`에서 Contentlayer 변환 에러가 없다
- [ ] 새 태그 추가 시 `tag-data.json`이 정상 생성된다

### API 작업

- [ ] API 응답 형식이 `api_spec.md`와 일치한다

### 설정 변경 (`siteMetadata.js`, `contentlayer.config.ts`, `next.config.js`)

- [ ] `architecture.md` 또는 관련 문서가 업데이트됐다
- [ ] 빌드 후 영향받는 전체 페이지를 확인했다

### 문서 작업

- [ ] `docs/` 내 관련 파일이 업데이트됐다
- [ ] 코드와 문서 간 불일치가 없다
