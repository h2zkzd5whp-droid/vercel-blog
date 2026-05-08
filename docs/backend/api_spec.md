# api_spec.md

> 현재 API는 Newsletter 구독 단 1개입니다. DB 없는 정적 블로그이므로 서버 API가 최소화되어 있습니다.

---

## 공통 규칙

| 항목 | 내용 |
|------|------|
| 인증 | 없음 (모든 엔드포인트 공개) |
| 에러 응답 형식 | `{ error: string }` |
| Content-Type | `application/json` |

---

## 엔드포인트

### 1. Newsletter 구독

`POST /api/newsletter`

- **요청**:
  ```json
  { "email": "user@example.com" }
  ```
- **응답** (201):
  ```json
  { "message": "Successfully subscribed" }
  ```
- **에러**:
  - `400` — 이메일 형식 오류 또는 이미 구독됨
  - `500` — Newsletter 제공자 API 오류

> Newsletter 제공자는 `siteMetadata.js`의 `newsletter.provider` 설정값으로 결정됩니다.
> 현재 설정 없으면 비활성화 상태입니다.

---

## 정적 생성 엔드포인트 (Next.js Route Handlers)

| 경로 | 파일 | 설명 |
|------|------|------|
| `/robots.txt` | `app/robots.ts` | 크롤러 정책 |
| `/sitemap.xml` | `app/sitemap.ts` | 사이트맵 (allBlogs 기반 자동 생성) |
