---
title: "Tối ưu Core Web Vitals để cải thiện SEO"
date: 2024-03-10
image: "images/blog7.png"
tags: ["Web Vitals", "Performance", "Optimization"]
author: "Trần Phạm Gia Huy"
---

## Core Web Vitals là gì?

Core Web Vitals là một tập hợp các metrics quan trọng mà Google sử dụng để đánh giá trải nghiệm người dùng trên website. Ba metrics chính là:

1. **LCP (Largest Contentful Paint)**: Thời gian tải nội dung chính
2. **FID (First Input Delay)**: Độ trễ khi người dùng tương tác lần đầu
3. **CLS (Cumulative Layout Shift)**: Độ ổn định của layout

## Tại sao Core Web Vitals quan trọng?

- **SEO**: Google sử dụng Core Web Vitals như một ranking factor
- **User Experience**: Website nhanh = người dùng hài lòng hơn
- **Conversion**: Mỗi giây delay có thể giảm 7% conversion rate

## Tối ưu LCP (Largest Contentful Paint)

LCP đo thời gian từ khi trang bắt đầu load đến khi phần tử lớn nhất hiển thị. Mục tiêu: **< 2.5 giây**

### 1. Optimize Images

```html
<!-- Sử dụng modern image formats -->
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Description" loading="lazy">
</picture>
```

### 2. Preload Critical Resources

```html
<link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="/hero-image.jpg" as="image">
```

### 3. Server-Side Rendering

SSR giúp render HTML trên server, giảm thời gian đến First Contentful Paint.

## Tối ưu FID (First Input Delay)

FID đo độ trễ khi người dùng click/tap lần đầu. Mục tiêu: **< 100ms**

### 1. Code Splitting

Chia nhỏ JavaScript bundle:

```javascript
// Lazy load components
const HeavyComponent = React.lazy(() => import('./HeavyComponent'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <HeavyComponent />
    </Suspense>
  );
}
```

### 2. Minimize JavaScript

- Loại bỏ unused code
- Minify và compress JavaScript
- Sử dụng tree shaking

### 3. Defer Non-Critical JavaScript

```html
<script src="analytics.js" defer></script>
```

## Tối ưu CLS (Cumulative Layout Shift)

CLS đo độ ổn định của layout. Mục tiêu: **< 0.1**

### 1. Set Dimensions cho Images và Videos

```html
<img src="image.jpg" width="800" height="600" alt="Description">
```

### 2. Reserve Space cho Ads và Embeds

```css
.ad-container {
  min-height: 250px; /* Reserve space */
}
```

### 3. Avoid Inserting Content Above Existing Content

Tránh thêm nội dung vào phần trên của trang sau khi đã render.

## Tools để đo Core Web Vitals

### 1. Google PageSpeed Insights

Công cụ miễn phí của Google để đo performance và Core Web Vitals.

### 2. Chrome DevTools

Performance tab trong Chrome DevTools cung cấp detailed metrics.

### 3. Web Vitals Extension

Browser extension để monitor Core Web Vitals trong real-time.

## Best Practices

1. **Monitor regularly**: Kiểm tra Core Web Vitals định kỳ
2. **Test on real devices**: Không chỉ test trên desktop
3. **Optimize incrementally**: Tối ưu từng metric một
4. **Measure impact**: Đo lường kết quả sau mỗi thay đổi

## Kết luận

Core Web Vitals không chỉ quan trọng cho SEO mà còn ảnh hưởng trực tiếp đến trải nghiệm người dùng. Bằng cách tối ưu LCP, FID, và CLS, bạn có thể cải thiện cả ranking và conversion rate của website.

