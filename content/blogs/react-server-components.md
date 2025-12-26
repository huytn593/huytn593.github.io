---
title: "Tìm hiểu về React Server Components"
date: 2024-05-01
image: "images/blog1.png"
tags: ["React", "Next.js", "Web Development"]
author: "Trần Phạm Gia Huy"
---

## Giới thiệu

React Server Components (RSC) là một tính năng mới mang tính cách mạng trong hệ sinh thái React, cho phép các component được render trên server mà không cần gửi JavaScript xuống client. Đây là bước tiến quan trọng trong việc tối ưu hóa hiệu năng web applications.

## Server Components là gì?

Server Components là các React components chạy hoàn toàn trên server. Khác với Server-Side Rendering (SSR) truyền thống, Server Components:

- **Không gửi JavaScript xuống client**: Chỉ gửi HTML đã render
- **Có thể truy cập trực tiếp vào backend resources**: Database, file system, internal APIs
- **Tự động code splitting**: Chỉ tải những gì cần thiết
- **Giảm bundle size**: Các dependencies của Server Components không được đưa vào client bundle

## Lợi ích chính

### 1. Hiệu năng tốt hơn
```jsx
// Server Component - chạy trên server
async function BlogPost({ id }) {
  // Truy cập database trực tiếp
  const post = await db.posts.find(id);
  
  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}
```

### 2. Bundle size nhỏ hơn
Các thư viện lớn như markdown parsers, syntax highlighters có thể được sử dụng trong Server Components mà không làm tăng kích thước bundle của client.

### 3. Automatic Code Splitting
React tự động chia nhỏ code dựa trên Server Components tree, đảm bảo client chỉ tải những gì cần thiết.

## Server Components vs Client Components

| Tính năng | Server Components | Client Components |
|-----------|------------------|-------------------|
| Render location | Server | Client |
| Interactivity | ❌ Không | ✅ Có |
| Hooks (useState, useEffect) | ❌ Không | ✅ Có |
| Access backend | ✅ Trực tiếp | ❌ Qua API |
| Bundle impact | ✅ Không ảnh hưởng | ❌ Tăng bundle size |

## Sử dụng trong Next.js 13+

Next.js 13 đã tích hợp sẵn React Server Components với App Router:

```jsx
// app/page.js - Server Component by default
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

Để tạo Client Component, thêm directive `'use client'`:

```jsx
'use client';

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

## Best Practices

1. **Giữ Server Components làm mặc định**: Chỉ chuyển sang Client Components khi cần interactivity
2. **Kết hợp thông minh**: Sử dụng Server Components cho data fetching, Client Components cho UI interactions
3. **Tránh prop drilling**: Server Components có thể fetch data trực tiếp thay vì truyền props qua nhiều layers

## Kết luận

React Server Components đại diện cho sự thay đổi lớn trong cách chúng ta xây dựng ứng dụng React. Bằng cách tận dụng sức mạnh của server, chúng ta có thể tạo ra các ứng dụng nhanh hơn, nhẹ hơn và dễ bảo trì hơn.

Với sự hỗ trợ từ Next.js 13+ và các framework khác, RSC đang trở thành tiêu chuẩn mới cho React development trong năm 2024 và những năm tiếp theo.
