# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

- `npm run dev` — Start dev server at localhost:4321
- `npm run build` — Build production site to `./dist/`
- `npm run preview` — Preview production build locally

No test runner or linter is configured.

## Architecture

Astro 5 블로그 (한식 수익화 블로그). 정적 사이트 생성(SSG) 방식이며, MDX와 sitemap 통합 사용.

**콘텐츠 시스템:** 블로그 글은 `src/content/blog/`에 `.md` 또는 `.mdx` 파일로 저장. 컬렉션 스키마는 `src/content.config.ts`에 정의되어 있으며, frontmatter 필수 필드: `title`, `description`, `pubDate`. 선택 필드: `updatedDate`, `heroImage`. `getCollection('blog')`으로 조회.

**라우팅:** `src/pages/` 기반 파일 라우팅. 개별 블로그 글은 `src/pages/blog/[...slug].astro` 동적 라우트 사용. RSS 피드는 `src/pages/rss.xml.js`에서 생성.

**레이아웃:** `BaseHead.astro`(SEO 메타, Open Graph, 폰트, 글로벌 CSS) → `Header.astro` / `Footer.astro` 셸. 블로그 글은 `BlogPost.astro` 레이아웃 사용.

**전역 상수:** 사이트 제목과 설명은 `src/consts.ts`에서 관리.

**TypeScript:** strict 모드, `strictNullChecks` 활성화.

---

## 한식 블로그 글 작성 규칙

이 블로그는 **한식(Korean Food) 수익화 블로그**입니다. 아래 규칙을 반드시 따릅니다.

### 글 작성 트리거

사용자가 **"새 글 작성"** 이라고 입력하면, 아래 규칙에 따라 새로운 블로그 글을 자동으로 작성합니다.

### 글 작성 규칙

1. **주제:** 매번 새로운 한식 관련 주제로 작성 (이전 글과 중복되지 않도록 기존 `src/content/blog/` 글 목록 확인)
2. **분량:** 최소 5000자 이상
3. **말투:** AI 느낌이 나지 않는 자연스럽고 친근한 한국어 (블로그 운영자가 직접 쓴 느낌)
4. **SEO 최적화:**
   - `title`: 검색 유입에 유리한 키워드 포함 (예: "집에서 만드는 김치찌개 레시피")
   - `description`: 핵심 키워드를 포함한 2~3문장 요약
   - 본문에 관련 키워드 자연스럽게 반복 배치
   - h2, h3 소제목을 활용한 구조화된 글
5. **이미지:** 본문 중간에 Unsplash 이미지를 1장 이상 삽입 (마크다운 `![alt](URL)` 형식, 해당 한식과 관련된 검색어로 Unsplash에서 검색)
6. **파일 형식:** `src/content/blog/` 디렉토리에 `.md` 파일로 생성
7. **파일명:** 영문 슬러그 (예: `kimchi-jjigae-recipe.md`)
8. **frontmatter 형식:**
   ```yaml
   ---
   title: 'SEO 최적화된 한국어 제목'
   description: '핵심 키워드 포함 요약'
   pubDate: '현재 날짜'
   heroImage: '' # 비워두거나 로컬 이미지 경로
   ---
   ```
