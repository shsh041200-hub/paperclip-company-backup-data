---
name: "[FEAT] /guides 섹션 chrome 통일 — guides/layout.tsx 머지 + [slug] footer 중복 정리"
assignee: "cto"
---

## 배경
PACAA-359 stash 분석 중 발견. 보드님이 작업하다 untracked 로 남긴 app/guides/layout.tsx (64줄) 가 stash 에 보관 중. 보드 OK 받아 정식 PR 진행.

## 현재 사이트 chrome 구조 (분석)
- app/layout.tsx (root): header/nav/footer 0건. 그냥 <html><body> + analytics.
- app/guides/page.tsx: header/footer 0건. chrome 없음 (사용자가 layout 만든 동기).
- app/guides/[slug]/page.tsx: footer 7개 (slug 별 분기), header 0건.

## Scope

### 1. layout.tsx 추가
경로: app/guides/layout.tsx (64줄)

내용 (전문):

```tsx
import Link from "next/link";
import { PacklinxLogo } from "@/components/PacklinxLogo";

export default function GuidesLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="min-h-screen bg-white flex flex-col">
      <header className="bg-[#0F172A] sticky top-0 z-50 border-b border-white/[0.06]">
        <div className="max-w-7xl mx-auto px-5 sm:px-8 h-16 flex items-center justify-between">
          <Link href="/" className="flex items-center gap-3">
            <PacklinxLogo variant="dark" />
            <span className="hidden sm:inline text-slate-400 text-[11px] font-medium tracking-widest uppercase">
              패키징 업체 검색 플랫폼
            </span>
          </Link>
          <nav className="flex items-center gap-2 s
