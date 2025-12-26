---
title: "Software Architecture Patterns: Khi nào sử dụng gì?"
date: 2024-02-20
image: "images/blog8.png"
tags: ["Software Engineering", "Architecture", "Web Development"]
author: "Trần Phạm Gia Huy"
---

## Tại sao Architecture Patterns quan trọng?

Software Architecture Patterns là các giải pháp đã được chứng minh cho các vấn đề thiết kế phổ biến. Hiểu và áp dụng đúng pattern giúp code dễ maintain, scale, và test hơn.

## MVC (Model-View-Controller)

MVC là pattern phổ biến nhất, tách ứng dụng thành 3 phần:

- **Model**: Business logic và data
- **View**: UI presentation
- **Controller**: Xử lý user input

### Khi nào sử dụng?

- Web applications với server-side rendering
- Desktop applications
- Frameworks: Ruby on Rails, Django, ASP.NET MVC

```javascript
// Model
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }
}

// View
function renderUser(user) {
  return `<div>${user.name} - ${user.email}</div>`;
}

// Controller
function handleUserSubmit(name, email) {
  const user = new User(name, email);
  return renderUser(user);
}
```

## MVVM (Model-View-ViewModel)

MVVM phổ biến trong frontend frameworks:

- **Model**: Data và business logic
- **View**: UI
- **ViewModel**: Bridge giữa Model và View

### Khi nào sử dụng?

- Single Page Applications (SPA)
- Frameworks: Angular, Vue.js, WPF

## Microservices Architecture

Chia ứng dụng thành nhiều services độc lập, mỗi service có database riêng.

### Ưu điểm:

- **Scalability**: Scale từng service độc lập
- **Technology diversity**: Mỗi service có thể dùng tech stack khác
- **Fault isolation**: Lỗi ở một service không ảnh hưởng toàn bộ

### Nhược điểm:

- **Complexity**: Phức tạp hơn monolithic
- **Network latency**: Communication giữa services
- **Data consistency**: Khó đảm bảo consistency

### Khi nào sử dụng?

- Large applications với nhiều teams
- Cần scale độc lập các components
- Các services có different requirements

## Serverless Architecture

Chạy code mà không cần quản lý servers:

- **Functions as a Service (FaaS)**: AWS Lambda, Azure Functions
- **Backend as a Service (BaaS)**: Firebase, Supabase

### Ưu điểm:

- **No server management**: Không cần quản lý infrastructure
- **Auto-scaling**: Tự động scale theo demand
- **Cost-effective**: Chỉ trả tiền khi sử dụng

### Nhược điểm:

- **Cold starts**: Delay khi function chưa được invoke
- **Vendor lock-in**: Phụ thuộc vào platform
- **Debugging**: Khó debug hơn traditional apps

## Event-Driven Architecture

Components communicate thông qua events:

- **Event Producer**: Tạo events
- **Event Consumer**: Xử lý events
- **Event Bus**: Message broker

### Khi nào sử dụng?

- Real-time applications
- Microservices communication
- Decoupled systems

## Clean Architecture

Tổ chức code thành layers với dependencies hướng vào trong:

```
┌─────────────────────┐
│   Frameworks & UI   │
├─────────────────────┤
│   Interface Adapters│
├─────────────────────┤
│   Use Cases         │
├─────────────────────┤
│   Entities          │
└─────────────────────┘
```

### Principles:

- **Dependency Rule**: Dependencies chỉ hướng vào trong
- **Independence**: Business logic độc lập với frameworks
- **Testability**: Dễ test vì business logic tách biệt

## Kết luận

Không có pattern nào là "best" cho mọi trường hợp. Việc chọn pattern phụ thuộc vào:
- **Project size**: Small projects có thể dùng MVC đơn giản
- **Team size**: Large teams có thể cần microservices
- **Requirements**: Real-time apps có thể cần event-driven

Quan trọng là hiểu trade-offs của mỗi pattern và chọn phù hợp với context của bạn!

