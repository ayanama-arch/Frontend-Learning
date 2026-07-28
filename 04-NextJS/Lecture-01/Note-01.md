# Next.js 16 — Routing (Complete Notes)

---

## 1. Core Idea: File-System Based Routing

Next.js turns your folder structure inside the `app/` directory directly into URL routes.

- Every **folder** = a URL **segment**.
- A `page.tsx` (or `.js`) file inside a folder makes that segment **publicly accessible** as a route.
- Only files named `page.tsx`/`page.js` are routable — you can keep components, hooks, utils in the same folder and they will **not** become routes.

```
app/
├─ page.tsx            → /
├─ about/
│  └─ page.tsx          → /about
└─ blog/
   └─ page.tsx          → /blog
```

**Theory:** This is called _convention over configuration_ — there is no central routes file (unlike Express or React Router). The folder tree IS the route table.

---

## 2. Special (Reserved) Files

Inside any route segment folder, Next.js recognizes specific filenames with specific roles:

| File            | Purpose                                                                                       |
| --------------- | --------------------------------------------------------------------------------------------- |
| `page.tsx`      | UI unique to a route, makes the segment publicly accessible                                   |
| `layout.tsx`    | Shared UI for a segment and its children; preserves state on navigation                       |
| `template.tsx`  | Like layout, but re-mounts (fresh state) on every navigation                                  |
| `loading.tsx`   | Instant loading UI using React Suspense boundary                                              |
| `error.tsx`     | Error UI boundary (must be a Client Component)                                                |
| `not-found.tsx` | UI shown when `notFound()` is thrown or route doesn't match                                   |
| `route.tsx`     | Server-side API endpoint (Route Handler) — cannot coexist with `page.tsx` in the same segment |
| `default.tsx`   | Fallback UI for a **Parallel Route** slot                                                     |

**Example — Layout:**

```tsx
// app/blog/layout.tsx
export default function BlogLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <section>
      <nav>Blog Nav</nav>
      {children}
    </section>
  );
}
```

Layouts wrap every nested `page.tsx` under that folder and **persist across navigations** within that segment (no re-render/re-fetch), which is why Next.js 16's layout deduplication optimization (see §10) matters.

---

## 3. Nested Routes

Nesting folders creates nested URL paths automatically.

```
app/
└─ dashboard/
   └─ settings/
      └─ page.tsx        → /dashboard/settings
```

Each level can have its own `layout.tsx`, so layouts nest and compose:

```
RootLayout
 └─ DashboardLayout
     └─ SettingsPage
```

---

## 4. Dynamic Routes

Square brackets `[param]` create a dynamic (variable) URL segment.

```
app/
└─ blog/
   └─ [slug]/
      └─ page.tsx        → /blog/hello-world, /blog/any-string
```

```tsx
// app/blog/[slug]/page.tsx
export default async function Page({
  params,
}: {
  params: Promise<{ slug: string }>;
}) {
  const { slug } = await params;
  return <h1>Post: {slug}</h1>;
}
```

> **Important Next.js 15/16 breaking change:** `params` (and `searchParams`) are now **Promises**, not plain objects. You must `await` them in Server Components, or use `use(params)` in Client Components. This was done to allow better streaming/parallel data fetching.

```tsx
// Client Component version
"use client";
import { use } from "react";

export default function Page({
  params,
}: {
  params: Promise<{ slug: string }>;
}) {
  const { slug } = use(params);
  return <h1>{slug}</h1>;
}
```

### 4.1 Catch-all Segments

`[...slug]` matches one or more path segments.

```
app/docs/[...slug]/page.tsx
```

| URL         | slug value               |
| ----------- | ------------------------ |
| `/docs/a`   | `['a']`                  |
| `/docs/a/b` | `['a','b']`              |
| `/docs`     | **404** (does not match) |

### 4.2 Optional Catch-all Segments

`[[...slug]]` — double brackets — also matches the parent route itself.

```
app/docs/[[...slug]]/page.tsx
```

| URL         | slug value  |
| ----------- | ----------- |
| `/docs`     | `undefined` |
| `/docs/a/b` | `['a','b']` |

### 4.3 Static Params Generation

For static rendering/SSG of dynamic routes, use `generateStaticParams`:

```tsx
export async function generateStaticParams() {
  const posts = await fetch("https://api.example.com/posts").then((r) =>
    r.json(),
  );
  return posts.map((post: any) => ({ slug: post.slug }));
}
```

---

## 5. Route Groups `(folderName)`

Wrapping a folder name in parentheses **organizes files without affecting the URL**.

```
app/
├─ (marketing)/
│  ├─ about/page.tsx     → /about   (not /marketing/about)
│  └─ contact/page.tsx   → /contact
└─ (shop)/
   └─ cart/page.tsx      → /cart
```

**Use cases (theory):**

1. Organize routes by team/feature/concern without polluting the URL.
2. Create **multiple root layouts** — each top-level route group can have its own `layout.tsx` (opt out of a shared root layout for a section, e.g. separate layouts for `(marketing)` vs `(app)`).

```
app/
├─ (marketing)/layout.tsx   → different layout for marketing pages
└─ (app)/layout.tsx         → different layout for app/dashboard pages
```

> Note: When using multiple root-level route groups like this, each must have its own `<html>` and `<body>` since there's no shared root layout unless you add one above them.

---

## 6. Parallel Routes `@slotName`

Parallel routes let you render **two or more pages in the same layout simultaneously**, each independently loadable/error-able. A folder prefixed with `@` defines a **slot** (does not affect the URL).

```
app/
├─ layout.tsx
├─ page.tsx           // default/children slot
├─ @analytics/
│  ├─ page.tsx
│  └─ default.tsx      // required fallback
└─ @team/
   ├─ page.tsx
   └─ default.tsx      // required fallback
```

```tsx
// app/layout.tsx
export default function Layout({
  children,
  analytics,
  team,
}: {
  children: React.ReactNode;
  analytics: React.ReactNode;
  team: React.ReactNode;
}) {
  return (
    <>
      {children}
      {analytics}
      {team}
    </>
  );
}
```

**Theory / use cases:**

- Dashboards with independently-loading widgets (each slot gets its own `loading.tsx` / `error.tsx`).
- Conditional rendering of slots based on auth state, role, etc.
- Modals (often paired with intercepting routes — see §7).

> **Next.js 16 requirement (important, tightened rule):** Every parallel route slot **must have a `default.tsx` file**, or the **build will fail**. `default.tsx` tells Next.js what to render for that slot when the current URL doesn't match anything inside it (e.g. on initial load or unmatched sub-navigation).

```tsx
// app/@analytics/default.tsx
export default function Default() {
  return null;
}
```

**Rendering rule:** if one slot is dynamically rendered, all sibling slots at that segment level become dynamic too (this only matters for static/PPR rendering, not for fully dynamic pages).

---

## 7. Intercepting Routes `(.)`, `(..)`, `(..)(..)`, `(...)`

Intercepting routes let a route "intercept" another route and render it **within the current layout/context** (e.g., a photo opens as a modal over the feed instead of a full page navigation) while keeping the URL shareable — a direct visit/refresh renders the real, full page.

| Convention       | Matches                        |
| ---------------- | ------------------------------ |
| `(.)folder`      | same level (same directory)    |
| `(..)folder`     | one level above                |
| `(..)(..)folder` | two levels above               |
| `(...)folder`    | from the root `app/` directory |

**Example — Photo modal pattern (classic Instagram-style feed):**

```
app/
├─ feed/
│  ├─ page.tsx                → /feed
│  └─ @modal/
│     ├─ (.)photo/[id]/page.tsx   → intercepted /feed/photo/[id] (renders as modal)
│     └─ default.tsx
└─ photo/
   └─ [id]/
      └─ page.tsx             → /photo/[id] (full page, used on direct load/refresh)
```

```tsx
// app/feed/@modal/(.)photo/[id]/page.tsx
export default async function PhotoModal({
  params,
}: {
  params: Promise<{ id: string }>;
}) {
  const { id } = await params;
  return (
    <Modal>
      <img src={`/photos/${id}.jpg`} />
    </Modal>
  );
}
```

**Theory / key behavior:**

- Interception only applies to **soft navigation** (via `<Link>` or `router.push`), not hard navigation/refresh — a hard refresh renders the canonical route (`/photo/[id]`) instead.
- Commonly combined with **Parallel Routes** (`@modal` slot above) so the modal can render alongside the underlying page.
- Layouts/Server Components are preserved across the interception **only if the route segment hierarchy stays unchanged**; if a parent segment changes, Next.js may invalidate the router cache and remount the subtree.

---

## 8. Linking & Navigating

### 8.1 `<Link>` Component

Primary way to navigate client-side between routes (like an SPA, no full page reload).

```tsx
import Link from "next/link";

export default function Nav() {
  return <Link href="/dashboard">Go to Dashboard</Link>;
}
```

Key props:

- `prefetch` — controls prefetching behavior (`true`/`false`/`null` default logic).
- `replace` — replaces current history entry instead of pushing a new one.
- `scroll` — controls scroll-to-top behavior on navigation.

### 8.2 `useRouter` (Client Components)

```tsx
"use client";
import { useRouter } from "next/navigation";

export default function Button() {
  const router = useRouter();
  return <button onClick={() => router.push("/dashboard")}>Go</button>;
}
```

Common methods: `router.push()`, `router.replace()`, `router.back()`, `router.forward()`, `router.refresh()`.

### 8.3 Reading Params/Search Params in Client Components

```tsx
"use client";
import { useParams, useSearchParams, usePathname } from "next/navigation";

export default function Info() {
  const params = useParams(); // { slug: 'hello' }
  const searchParams = useSearchParams(); // ?query=... → URLSearchParams
  const pathname = usePathname(); // '/blog/hello'
  return <div>{pathname}</div>;
}
```

### 8.4 Redirects

```tsx
import { redirect } from "next/navigation";

export default async function Page() {
  const user = await getUser();
  if (!user) redirect("/login");
  return <div>Welcome</div>;
}
```

`redirect()` works in Server Components, Route Handlers, and Server Actions. There's also `permanentRedirect()` for 308s.

### 8.5 `notFound()`

```tsx
import { notFound } from "next/navigation";

export default async function Page({
  params,
}: {
  params: Promise<{ id: string }>;
}) {
  const { id } = await params;
  const post = await getPost(id);
  if (!post) notFound();
  return <div>{post.title}</div>;
}
```

Triggers rendering of the nearest `not-found.tsx`.

---

## 9. Route Handlers (`route.tsx`) — API Routing

A `route.ts` file inside `app/` defines a server-side endpoint instead of a UI page. **Cannot coexist with `page.tsx` in the same segment.**

```
app/
└─ api/
   └─ users/
      └─ route.ts        → GET/POST /api/users
```

```tsx
// app/api/users/route.ts
import { NextResponse } from "next/server";

export async function GET() {
  return NextResponse.json({ users: [] });
}

export async function POST(request: Request) {
  const body = await request.json();
  return NextResponse.json({ created: body }, { status: 201 });
}
```

Supported exported functions: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, `OPTIONS`.

---

## 10. What's New in Routing for Next.js 16 Specifically

Next.js 16 shipped **a complete overhaul of routing and client-side navigation** for leaner, faster page transitions:

1. **Layout Deduplication** — when prefetching multiple links that share a layout (e.g., 50 product links sharing one parent layout), the shared layout is now downloaded **once** instead of once per link, drastically cutting network transfer.
2. **Incremental Prefetching** — instead of prefetching whole pages, Next.js now only prefetches the parts **not already in the client cache**.
3. **Smarter Prefetch Cache**:
   - Cancels a prefetch request if the link leaves the viewport before it completes.
   - Prioritizes prefetching on hover or re-entry into the viewport.
   - Re-prefetches a link automatically when its underlying data is invalidated.
   - Designed to work seamlessly with the new **Cache Components** feature.
4. **Cache Components (new caching model)** — refined, explicit caching APIs. By default now, all dynamic code in any page/layout/route is executed at request time (more predictable, "what you write is what runs" behavior), while still supporting **Partial Prerendering (PPR)** so static shells can stream in dynamic (Suspense-boundary) content. Enabled via `next.config.ts`:

   ```ts
   // next.config.ts
   import type { NextConfig } from "next";

   const nextConfig: NextConfig = {
     cacheComponents: true,
   };

   export default nextConfig;
   ```

5. **`params` / `searchParams` as Promises** — carried over/solidified from Next.js 15, this enables the streaming and parallel-data-fetching model that underpins the new prefetching behavior (see §4).
6. **Stricter Parallel Route rule** — every `@slot` **must** ship a `default.tsx`, or the production build fails (previously more lenient) — see §6.
7. **`@next/routing` adapter (experimental)** — a low-level package to reproduce Next.js's route-matching behavior outside of the framework (e.g., for custom hosting adapters), exposing `resolvedPathname`, `resolvedQuery`, `invocationTarget`, `resolvedHeaders`, and `status` from `onBuildComplete`.

---

## 11. Quick Reference Cheat Sheet

| Convention                               | Meaning                                          |
| ---------------------------------------- | ------------------------------------------------ |
| `folder/page.tsx`                        | Static route segment                             |
| `[folder]/page.tsx`                      | Dynamic segment                                  |
| `[...folder]/page.tsx`                   | Catch-all segment                                |
| `[[...folder]]/page.tsx`                 | Optional catch-all segment                       |
| `(folder)/`                              | Route group — organizational only, no URL impact |
| `@folder/`                               | Parallel route slot                              |
| `(.)folder`, `(..)folder`, `(...)folder` | Intercepting route                               |
| `layout.tsx`                             | Persistent shared UI                             |
| `template.tsx`                           | Non-persistent shared UI (remounts)              |
| `loading.tsx`                            | Suspense fallback                                |
| `error.tsx`                              | Error boundary                                   |
| `not-found.tsx`                          | 404 UI                                           |
| `route.tsx`                              | API/Route Handler                                |
| `default.tsx`                            | Required fallback for parallel route slots       |

---

_Sources: Next.js official docs (nextjs.org/docs/app, nextjs.org/blog/next-16) — current stable version referenced: 16.2.11._
