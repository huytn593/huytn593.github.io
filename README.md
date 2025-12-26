 Portfolio Website - Trần Phạm Gia Huy

[![Hugo](https://img.shields.io/badge/Hugo-0.100+-00ADD8?style=flat-square&logo=hugo)](https://gohugo.io/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-huytn593-181717?style=flat-square&logo=github)](https://github.com/huytn593)
[![Vercel](https://img.shields.io/badge/Vercel-%23000000.svg?logo=vercel&logoColor=white)](#)

Portfolio website cá nhân được xây dựng bằng Hugo Static Site Generator, kết hợp với theme Hugo Profile. Website bao gồm portfolio cá nhân và blog chia sẻ kiến thức về công nghệ, lập trình và phát triển phần mềm.

🌐 Live Demo: [https://huytn593.github.io/](https://huytn593.github.io/)



 📋 Mục lục

- [Giới thiệu](giới-thiệu)
- [Tính năng](tính-năng)
- [Công nghệ sử dụng](công-nghệ-sử-dụng)
- [Cấu trúc dự án](cấu-trúc-dự-án)
- [Cài đặt và chạy](cài-đặt-và-chạy)
- [Cấu hình](cấu-hình)
- [Tùy chỉnh](tùy-chỉnh)
- [Tính năng đã phát triển](tính-năng-đã-phát-triển)
- [Cấu trúc Blog](cấu-trúc-blog)
- [Deployment](deployment)
- [Tác giả](tác-giả)
- [License](license)



 🎯 Giới thiệu

Đây là website portfolio cá nhân được phát triển để:
- Giới thiệu bản thân, kỹ năng và kinh nghiệm
- Chia sẻ kiến thức thông qua blog cá nhân
- Trình bày các dự án đã thực hiện
- Tạo kênh liên hệ với nhà tuyển dụng và cộng đồng developer

Website được xây dựng với focus vào:
- Performance: Tối ưu tốc độ tải trang
- SEO: Tối ưu hóa cho công cụ tìm kiếm
- Responsive: Tương thích mọi thiết bị
- User Experience: Giao diện hiện đại, dễ sử dụng



 ✨ Tính năng

 🏠 Trang chủ
- Hero Section: Giới thiệu cá nhân với avatar và social links
- About Section: Thông tin về bản thân và mục tiêu nghề nghiệp
- Education Section: Thông tin học vấn
- Projects Section: Hiển thị các dự án đã thực hiện
- Contact Section: Thông tin liên hệ

 📝 Blog System
- Blog List: Danh sách bài viết với preview cards
- Single Post: Trang chi tiết bài viết với TOC, tags, social share
- Tags & Categories: Phân loại bài viết theo tags và categories
- Pagination: Phân trang cho danh sách bài viết
- RSS Feed: Hỗ trợ RSS feed cho blog

 🎨 UI/UX Features
- Dark/Light Theme Toggle: Chuyển đổi giữa chế độ sáng/tối
- Responsive Design: Tối ưu cho mobile, tablet, desktop
- Smooth Animations: Hiệu ứng chuyển động mượt mà
- Modern Design: Giao diện hiện đại, chuyên nghiệp

 🔍 SEO & Performance
- Meta Tags: Đầy đủ meta tags cho SEO
- Sitemap: Tự động generate sitemap.xml
- Robots.txt: Cấu hình robots.txt
- Optimized Images: Lazy loading và responsive images
- Fast Loading: Tối ưu tốc độ tải trang



 🛠 Công nghệ sử dụng

 Core Technologies
- [Hugo](https://gohugo.io/) (v0.100+): Static Site Generator
- [Hugo Profile Theme](https://github.com/gurusabarish/hugo-profile): Base theme

 Frontend Technologies
- HTML5: Cấu trúc website
- CSS3: Styling và animations
- JavaScript: Tương tác và functionality
- Bootstrap 5: Responsive framework
- Font Awesome 6: Icons

 Build Tools
- Hugo CLI: Build và development server
- Git: Version control
- GitHub Pages: Hosting

 Development Tools
- Markdown: Content writing
- YAML: Configuration files
- Go Templates: Hugo templating engine



 📁 Cấu trúc dự án

```
Portfolio/
├── archetypes/           Content templates
├── assets/               Asset files
├── content/              Website content
│   ├── blogs/           Blog posts
│   │   ├── _index.md    Blog index page
│   │   └── *.md         Individual blog posts
│   └── _index.md        Homepage content
├── layouts/             Custom layouts (override theme)
│   ├── _default/        Default layouts
│   │   └── list.html    List page layout
│   ├── blogs/           Blog-specific layouts
│   │   ├── baseof.html  Blog base template
│   │   ├── list.html    Blog list layout
│   │   └── single.html  Single post layout
│   ├── partials/        Partial templates
│   │   ├── navbar.html  Navigation bar
│   │   └── sections/    Section partials
│   └── index.html       Homepage layout
├── static/              Static files
│   ├── css/             Custom CSS
│   │   └── custom.css   Main custom stylesheet
│   └── images/          Images
│       ├── avatar.png    Profile avatar
│       └── blog*.png     Blog post images
├── themes/              Hugo themes
│   └── hugo-profile/    Hugo Profile theme
├── config.yaml          Site configuration
├── README.md            This file
└── public/              Generated site (gitignored)
```



 🚀 Cài đặt và chạy

 Yêu cầu
- [Hugo Extended](https://gohugo.io/installation/) (v0.100+)
- [Git](https://git-scm.com/)
- Terminal/Command Prompt

 Cài đặt Hugo

Windows:
```powershell
 Sử dụng Chocolatey
choco install hugo-extended

 Hoặc tải từ: https://github.com/gohugoio/hugo/releases
```

macOS:
```bash
brew install hugo
```

Linux:
```bash
sudo apt-get install hugo
```

 Clone và chạy dự án

```bash
 Clone repository
git clone https://github.com/huytn593/Portfolio.git
cd Portfolio

 Chạy development server
hugo server

 Website sẽ chạy tại: http://localhost:1313
```

 Build cho production

```bash
 Generate static site
hugo

 Output sẽ nằm trong thư mục public/
```



 ⚙️ Cấu hình

 File `config.yaml`

File cấu hình chính của website:

```yaml
baseURL: "https://huytn593.github.io/"
languageCode: "vi-vn"
title: "Trần Phạm Gia Huy | Portfolio"
theme: "hugo-profile"

params:
  title: "Trần Phạm Gia Huy"
  description: "Sinh viên Công nghệ Phần mềm | Portfolio cá nhân"
  
  theme:
    disableThemeToggle: false
    defaultTheme: "dark"
  
  hero:
    enable: true
    title: "Trần Phạm Gia Huy"
    subtitle: "Sinh viên Công nghệ Phần mềm"
     ... more config
```

 Cấu hình Blog

Blog posts được lưu trong `content/blogs/` với format:

```markdown

title: "Tiêu đề bài viết"
date: 2024-05-20
image: "images/blog1.png"
tags: ["Tag1", "Tag2"]
author: "Trần Phạm Gia Huy"


Nội dung bài viết...
```



 🎨 Tùy chỉnh

 Custom CSS

File `static/css/custom.css` chứa các style tùy chỉnh:

- Theme Toggle Button: Styling cho nút chuyển đổi theme
- Blog Cards: Design cho blog post cards
- Responsive Styles: Media queries cho mobile/tablet
- Animations: Hover effects và transitions

 Custom Layouts

Các layout tùy chỉnh trong `layouts/`:

- `layouts/blogs/list.html`: Layout danh sách blog
- `layouts/blogs/single.html`: Layout bài viết đơn
- `layouts/_default/list.html`: Layout cho tags/categories
- `layouts/partials/navbar.html`: Navigation bar

 Thêm bài viết mới

```bash
 Tạo bài viết mới
hugo new blogs/my-new-post.md

 Hoặc tạo thủ công trong content/blogs/
```



 🎯 Tính năng đã phát triển

 1. Blog System Customization

 ✅ Blog List Page
- Card-based Layout: Hiển thị bài viết dạng cards với ảnh
- Uniform Display: Tất cả cards có chiều cao đồng đều
- Content Truncation: Cắt gọn nội dung preview (90 ký tự, 3 dòng)
- Image Support: Hỗ trợ ảnh đại diện cho mỗi bài viết
- Metadata Display: Hiển thị ngày đăng và tags
- Responsive Grid: Grid layout responsive (3 cột desktop, 2 cột tablet, 1 cột mobile)

 ✅ Single Post Page
- Featured Image: Ảnh nổi bật ở đầu bài viết
- Table of Contents: Tự động generate TOC từ headings
- Tags Display: Hiển thị tags với links
- Social Share: Buttons chia sẻ lên social media
- Reading Time: Tính toán thời gian đọc
- Scroll Progress: Progress bar khi scroll

 ✅ Tags & Categories Pages
- Tag Filtering: Lọc bài viết theo tags
- Category Pages: Trang danh mục bài viết
- Consistent Layout: Sử dụng cùng layout với blog list

 2. Theme Toggle Enhancement

 ✅ Improved Design
- Icon-based Toggle: Icon mặt trăng (light mode) / mặt trời (dark mode)
- Visual Feedback: Hover effects và animations
- Color Scheme: Màu vàng (fbbf24) để dễ nhận biết
- Responsive: Tự điều chỉnh kích thước trên mobile

 3. Navigation Improvements

 ✅ Fixed Navigation Issues
- Correct Blog Link: Sửa link từ `/ blogs` thành `/blogs`
- Consistent Navigation: Navigation nhất quán trên mọi trang

 4. Image Optimization

 ✅ Blog Images
- Proper Sizing: Ảnh fit đúng với cards (200px height)
- Object-fit: Sử dụng `object-fit: cover` để ảnh không bị méo
- Lazy Loading: Lazy load ảnh để tối ưu performance
- Error Handling: Ẩn wrapper nếu ảnh không load được
- Path Handling: Tự động xử lý đường dẫn ảnh (thêm "/" nếu thiếu)

 5. Responsive Design

 ✅ Mobile Optimization
- Breakpoints: 
  - Desktop: 992px+
  - Tablet: 768px - 991px
  - Mobile: < 768px
- Adaptive Heights: Chiều cao cards điều chỉnh theo màn hình
- Touch-friendly: Buttons và links dễ bấm trên mobile

 6. Performance Optimizations

 ✅ Loading Performance
- Content Truncation: Giảm kích thước preview content
- Lazy Loading: Lazy load images
- CSS Optimization: Minify và optimize CSS
- Fast Navigation: Smooth transitions



 📚 Cấu trúc Blog

 Danh sách bài viết hiện có (10 bài)

1. Tối ưu hóa hiệu năng Website
   - Tags: Performance, Web Vitals, Optimization
   - Date: 2024-05-20

2. Tương lai của AI trong Công nghệ phần mềm
   - Tags: AI, Machine Learning, Software Engineering
   - Date: 2024-05-10

3. Tìm hiểu về React Server Components
   - Tags: React, Next.js, Web Development
   - Date: 2024-05-01

4. TypeScript Best Practices cho Developer
   - Tags: TypeScript, Web Development, Software Engineering
   - Date: 2024-04-15

5. Next.js 14: Những tính năng mới đáng chú ý
   - Tags: Next.js, React, Web Development
   - Date: 2024-04-05

6. Machine Learning cơ bản cho Developer
   - Tags: Machine Learning, AI, Software Engineering
   - Date: 2024-03-25

7. Tối ưu Core Web Vitals để cải thiện SEO
   - Tags: Web Vitals, Performance, Optimization
   - Date: 2024-03-10

8. Software Architecture Patterns: Khi nào sử dụng gì?
   - Tags: Software Engineering, Architecture, Web Development
   - Date: 2024-02-20

9. React Hooks nâng cao: Custom Hooks và Best Practices
   - Tags: React, Web Development, Software Engineering
   - Date: 2024-02-05

10. AI Code Generation: Tương lai của lập trình?
    - Tags: AI, Software Engineering, Machine Learning
    - Date: 2024-01-15

 Tags phổ biến

- Web Development (4 bài)
- Software Engineering (5 bài)
- AI (3 bài)
- React (3 bài)
- Performance (2 bài)
- Machine Learning (2 bài)
- Next.js (2 bài)
- TypeScript (1 bài)
- Web Vitals (2 bài)
- Optimization (2 bài)



 🚀 Deployment

 GitHub Pages

Website được deploy lên GitHub Pages:

1. Build site:
   ```bash
   hugo
   ```

2. Push to GitHub:
   ```bash
   cd public
   git init
   git add .
   git commit -m "Deploy site"
   git branch -M main
   git remote add origin https://github.com/huytn593/huytn593.github.io.git
   git push -u origin main
   ```

3. Enable GitHub Pages:
   - Vào Settings > Pages
   - Chọn branch `main` và folder `/ (root)`
   - Website sẽ có tại: `https://huytn593.github.io/`

 Netlify (Alternative)

1. Connect repository với Netlify
2. Build command: `hugo`
3. Publish directory: `public`
4. Deploy tự động khi push code



 📊 Thống kê

- Tổng số bài viết: 10
- Tổng số tags: 10+
- Số sections trên homepage: 6
- Theme: Hugo Profile (customized)
- Build time: ~2-3 giây
- Site size: ~5MB (bao gồm images)



 🔧 Troubleshooting

 Lỗi thường gặp

1. Ảnh không hiển thị:
   - Kiểm tra đường dẫn ảnh trong frontmatter
   - Đảm bảo ảnh nằm trong `static/images/`
   - Sử dụng đường dẫn: `images/filename.png`

2. Theme không load:
   - Kiểm tra theme đã được clone: `git submodule update --init --recursive`
   - Đảm bảo `theme: "hugo-profile"` trong config.yaml

3. CSS không apply:
   - Clear cache browser
   - Kiểm tra đường dẫn CSS trong layouts
   - Rebuild site: `hugo --cleanDestinationDir`



 👤 Tác giả

Trần Phạm Gia Huy

- 🌐 Website: [https://huytn593.github.io/](https://huytn593.github.io/)
- 📧 Email: huytn593@gmail.com
- 💼 GitHub: [@huytn593](https://github.com/huytn593)
- 📱 Phone: (+84) 939 605 921
- 📍 Location: Thành phố Thủ Đức, Việt Nam

Học vấn:
- Sinh viên năm 4 ngành Công nghệ Phần mềm
- Đại học Công Nghệ TP.HCM (HUTECH)

Sở thích:
- Phát triển phần mềm
- Lập trình web
- Lập trình game
- Học hỏi công nghệ mới



 📄 License

Dự án này sử dụng theme [Hugo Profile](https://github.com/gurusabarish/hugo-profile) với license riêng.

Nội dung website (blog posts, images) thuộc bản quyền của Trần Phạm Gia Huy.



 🙏 Acknowledgments

- [Hugo](https://gohugo.io/) - Static site generator
- [Hugo Profile Theme](https://github.com/gurusabarish/hugo-profile) - Base theme
- [Bootstrap](https://getbootstrap.com/) - CSS framework
- [Font Awesome](https://fontawesome.com/) - Icons
- [GitHub Pages](https://pages.github.com/) - Hosting



 📝 Changelog

 Version 1.0.0 (2024)
- ✅ Initial release
- ✅ Blog system với 10 bài viết
- ✅ Dark/Light theme toggle
- ✅ Responsive design
- ✅ SEO optimization
- ✅ Custom layouts và styling
- ✅ Tags và categories support
- ✅ Image optimization



 🔮 Roadmap

- [ ] Thêm comment system (Disqus/Giscus)
- [ ] Thêm search functionality
- [ ] Thêm portfolio projects section
- [ ] Thêm analytics (Google Analytics)
- [ ] Thêm contact form
- [ ] Thêm RSS feed customization
- [ ] Thêm multi-language support
- [ ] Thêm reading progress indicator



 📞 Liên hệ

Nếu có bất kỳ câu hỏi hoặc đề xuất nào, vui lòng liên hệ:

- 📧 Email: huytn593@gmail.com
- 💬 GitHub Issues: [Create an issue](https://github.com/huytn593/Portfolio/issues)



⭐ Nếu bạn thấy dự án này hữu ích, hãy star repository này!



*Last updated: 2025*
