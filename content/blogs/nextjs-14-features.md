---
title: "Next.js 14: Những tính năng mới đáng chú ý"
date: 2024-04-05
image: "images/blog5.png"
tags: ["Next.js", "React", "Web Development"]
author: "Trần Phạm Gia Huy"
---

## Giới thiệu Next.js 14

Next.js 14 mang đến nhiều cải tiến đáng kể về performance, developer experience, và các tính năng mới. Trong bài viết này, chúng ta sẽ khám phá những điểm nổi bật nhất.

## Server Components và App Router

Next.js 14 tiếp tục cải thiện Server Components, cho phép bạn render components trực tiếp trên server, giảm JavaScript bundle size và cải thiện performance.

```jsx
// app/page.js - Server Component
export default async function HomePage() {
  const data = await fetch('https://api.example.com/data');
  const posts = await data.json();
  
  return (
    <main>
      <h1>Blog Posts</h1>
      {posts.map(post => (
        <PostCard key={post.id} post={post} />
      ))}
    </main>
  );
}
```

## Turbopack - Build Tool mới

Turbopack là bundler mới của Next.js, nhanh hơn Webpack rất nhiều:

- **700x faster** than Webpack cho dev server
- **10x faster** than Vite cho production builds
- Hỗ trợ hot module replacement (HMR) cực nhanh

## Partial Prerendering

Một tính năng thú vị khác là Partial Prerendering, cho phép bạn kết hợp static và dynamic content một cách linh hoạt:

```jsx
export default function Page() {
  return (
    <div>
      {/* Static content - được prerender */}
      <Header />
      <StaticContent />
      
      {/* Dynamic content - được render on-demand */}
      <Suspense fallback={<Loading />}>
        <DynamicContent />
      </Suspense>
    </div>
  );
}
```

## Server Actions

Server Actions giúp bạn gọi server functions trực tiếp từ client components:

```jsx
// app/actions.js
'use server'

export async function createPost(formData) {
  const title = formData.get('title');
  // Xử lý logic trên server
  await savePost(title);
}

// app/page.js
import { createPost } from './actions';

export default function Page() {
  return (
    <form action={createPost}>
      <input name="title" />
      <button type="submit">Create</button>
    </form>
  );
}
```

## Metadata API cải tiến

Next.js 14 cải thiện Metadata API, giúp SEO dễ dàng hơn:

```jsx
export const metadata = {
  title: 'My Blog',
  description: 'A blog about web development',
  openGraph: {
    title: 'My Blog',
    images: ['/og-image.png'],
  },
};
```

## Kết luận

Next.js 14 tiếp tục khẳng định vị thế là framework React hàng đầu với nhiều cải tiến về performance và developer experience. Nếu bạn đang làm việc với React, đây là thời điểm tốt để nâng cấp lên Next.js 14!

