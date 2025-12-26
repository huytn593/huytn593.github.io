---
title: "Tối ưu hóa hiệu năng Website"
date: 2024-05-20
image: "images/blog3.png"
tags: ["Performance", "Web Vitals", "Optimization"]
author: "Trần Phạm Gia Huy"
---

## Tại sao Performance lại quan trọng?

Trong thế giới web hiện đại, tốc độ tải trang trực tiếp ảnh hưởng đến:
- **User experience**: 53% users rời trang nếu load time > 3 giây
- **SEO ranking**: Google ưu tiên trang web nhanh
- **Conversion rate**: Mỗi giây delay giảm 7% conversions
- **Mobile users**: 4G/5G vẫn có latency cao ở nhiều khu vực

## Core Web Vitals - Metrics quan trọng

Google sử dụng 3 metrics chính để đánh giá UX:

### 1. Largest Contentful Paint (LCP)
**Mục tiêu: < 2.5s**

Thời gian để phần tử lớn nhất trên viewport được render.

```javascript
// Optimize LCP với preload critical resources
<head>
  <link rel="preload" href="/hero-image.jpg" as="image">
  <link rel="preconnect" href="https://fonts.googleapis.com">
</head>
```

### 2. First Input Delay (FID)
**Mục tiêu: < 100ms**

Thời gian từ khi user tương tác đến khi browser phản hồi.

```javascript
// ❌ BAD - Blocking main thread
function processHeavyTask() {
  for (let i = 0; i < 1000000; i++) {
    // Heavy computation
  }
}

// ✅ GOOD - Use Web Workers
const worker = new Worker('heavy-task.js');
worker.postMessage(data);
worker.onmessage = (e) => {
  console.log('Result:', e.data);
};
```

### 3. Cumulative Layout Shift (CLS)
**Mục tiêu: < 0.1**

Tránh layout shifts bất ngờ:

```css
/* ❌ BAD - No dimensions */
img {
  width: 100%;
}

/* ✅ GOOD - Reserve space */
img {
  width: 100%;
  aspect-ratio: 16 / 9;
}
```

## Techniques tối ưu hiệu năng

### 1. Image Optimization

```html
<!-- Modern format với fallback -->
<picture>
  <source srcset="/hero.webp" type="image/webp">
  <source srcset="/hero.avif" type="image/avif">
  <img src="/hero.jpg" alt="Hero" loading="lazy" width="800" height="600">
</picture>

<!-- Responsive images -->
<img 
  srcset="
    /small.jpg 400w,
    /medium.jpg 800w,
    /large.jpg 1200w
  "
  sizes="(max-width: 600px) 400px, (max-width: 900px) 800px, 1200px"
  src="/medium.jpg"
  alt="Responsive"
>
```

### 2. Code Splitting

```javascript
// React lazy loading
import { lazy, Suspense } from 'react';

const HeavyComponent = lazy(() => import('./HeavyComponent'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <HeavyComponent />
    </Suspense>
  );
}

// Next.js dynamic imports
import dynamic from 'next/dynamic';

const DynamicChart = dynamic(() => import('./Chart'), {
  loading: () => <p>Loading chart...</p>,
  ssr: false // Don't render on server
});
```

### 3. Lazy Loading

```javascript
// Intersection Observer for lazy loading
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;
      observer.unobserve(img);
    }
  });
});

document.querySelectorAll('img[data-src]').forEach(img => {
  observer.observe(img);
});
```

### 4. Caching Strategies

```javascript
// Service Worker caching
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      // Cache hit - return cached response
      if (response) {
        return response;
      }
      
      // Cache miss - fetch from network
      return fetch(event.request).then((response) => {
        // Cache the new response
        return caches.open('v1').then((cache) => {
          cache.put(event.request, response.clone());
          return response;
        });
      });
    })
  );
});
```

### 5. HTTP/2 & HTTP/3

```nginx
# Nginx HTTP/2 configuration
server {
  listen 443 ssl http2;
  
  # Enable server push
  http2_push /css/main.css;
  http2_push /js/app.js;
  
  # Optimize buffer sizes
  http2_max_field_size 16k;
  http2_max_header_size 32k;
}
```

## CSS Optimization

```css
/* ❌ BAD - Inline styles everywhere */
<div style="color: red; font-size: 16px;">...</div>

/* ✅ GOOD - CSS classes */
.error-text {
  color: red;
  font-size: 16px;
}

/* CSS containment for rendering performance */
.card {
  contain: layout style paint;
}

/* Use CSS variables for theme switching */
:root {
  --primary-color: #007bff;
  --text-color: #333;
}

.dark-mode {
  --primary-color: #0056b3;
  --text-color: #fff;
}
```

## JavaScript Performance

```javascript
// ❌ BAD - Multiple DOM queries
for (let i = 0; i < items.length; i++) {
  document.getElementById('list').innerHTML += `<li>${items[i]}</li>`;
}

// ✅ GOOD - Batch DOM updates
const list = document.getElementById('list');
const fragment = document.createDocumentFragment();
items.forEach(item => {
  const li = document.createElement('li');
  li.textContent = item;
  fragment.appendChild(li);
});
list.appendChild(fragment);

// Debounce expensive operations
function debounce(func, wait) {
  let timeout;
  return function executedFunction(...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func(...args), wait);
  };
}

window.addEventListener('resize', debounce(() => {
  // Expensive resize handler
}, 250));
```

## Monitoring & Measuring

### Lighthouse CI

```yaml
# .github/workflows/lighthouse.yml
name: Lighthouse CI
on: [push]
jobs:
  lighthouse:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Lighthouse
        uses: treosh/lighthouse-ci-action@v9
        with:
          urls: |
            https://example.com
            https://example.com/blog
          uploadArtifacts: true
```

### Real User Monitoring (RUM)

```javascript
// Track real user metrics
import { getCLS, getFID, getFCP, getLCP, getTTFB } from 'web-vitals';

function sendToAnalytics(metric) {
  // Send to analytics service
  fetch('/analytics', {
    method: 'POST',
    body: JSON.stringify(metric)
  });
}

getCLS(sendToAnalytics);
getFID(sendToAnalytics);
getFCP(sendToAnalytics);
getLCP(sendToAnalytics);
getTTFB(sendToAnalytics);
```

## CDN & Edge Computing

```javascript
// Cloudflare Workers example
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});

async function handleRequest(request) {
  // Cache at edge
  const cache = caches.default;
  let response = await cache.match(request);
  
  if (!response) {
    response = await fetch(request);
    // Cache for 1 hour
    response = new Response(response.body, response);
    response.headers.set('Cache-Control', 'max-age=3600');
    event.waitUntil(cache.put(request, response.clone()));
  }
  
  return response;
}
```

## Performance Budget

Đặt giới hạn cho các metrics:

| Metric | Budget |
|--------|--------|
| Total page size | < 1.5 MB |
| JavaScript bundle | < 300 KB |
| CSS bundle | < 100 KB |
| Images | < 500 KB |
| LCP | < 2.5s |
| FID | < 100ms |
| CLS | < 0.1 |

## Best Practices Checklist

✅ **Images**
- Sử dụng WebP/AVIF formats
- Lazy load images below fold
- Set explicit dimensions
- Use responsive images

✅ **JavaScript**
- Code splitting
- Tree shaking
- Minification & compression
- Remove unused code

✅ **CSS**
- Critical CSS inline
- Defer non-critical CSS
- Remove unused styles
- Use CSS containment

✅ **Fonts**
- Limit font families (≤ 2)
- Use font-display: swap
- Preload critical fonts
- Subset fonts

✅ **Caching**
- Cache static assets
- Use service workers
- Set proper cache headers
- Version assets

## Kết luận

Performance optimization không phải là một lần làm xong mà là quá trình liên tục:

1. **Measure**: Sử dụng Lighthouse, Web Vitals
2. **Optimize**: Implement các techniques phù hợp
3. **Monitor**: Track real user metrics
4. **Iterate**: Continuous improvement

Một website nhanh không chỉ làm user hài lòng mà còn tăng SEO ranking và conversion rate. Hãy đầu tư vào performance từ đầu, không đợi đến khi có vấn đề! ⚡
