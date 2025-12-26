---
title: "React Hooks nâng cao: Custom Hooks và Best Practices"
date: 2024-02-05
image: "images/blog9.png"
tags: ["React", "Web Development", "Software Engineering"]
author: "Trần Phạm Gia Huy"
---

## Custom Hooks là gì?

Custom Hooks cho phép bạn tách logic tái sử dụng ra khỏi components. Một custom hook là một function bắt đầu với "use" và có thể gọi các hooks khác.

## Tại sao cần Custom Hooks?

- **Reusability**: Tái sử dụng logic giữa các components
- **Separation of concerns**: Tách business logic khỏi UI
- **Testability**: Dễ test logic độc lập
- **Readability**: Code component sạch và dễ đọc hơn

## Các Custom Hooks phổ biến

### 1. useFetch Hook

Hook để fetch data:

```javascript
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchData() {
      try {
        setLoading(true);
        const response = await fetch(url);
        const json = await response.json();
        setData(json);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    }

    fetchData();
  }, [url]);

  return { data, loading, error };
}

// Usage
function UserProfile({ userId }) {
  const { data, loading, error } = useFetch(`/api/users/${userId}`);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  return <div>{data.name}</div>;
}
```

### 2. useLocalStorage Hook

Lưu và đọc data từ localStorage:

```javascript
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      return initialValue;
    }
  });

  const setValue = (value) => {
    try {
      setStoredValue(value);
      window.localStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error(error);
    }
  };

  return [storedValue, setValue];
}

// Usage
function Settings() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  return (
    <select value={theme} onChange={(e) => setTheme(e.target.value)}>
      <option value="light">Light</option>
      <option value="dark">Dark</option>
    </select>
  );
}
```

### 3. useDebounce Hook

Debounce giá trị để tránh quá nhiều re-renders:

```javascript
import { useState, useEffect } from 'react';

function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);

  return debouncedValue;
}

// Usage
function SearchBox() {
  const [searchTerm, setSearchTerm] = useState('');
  const debouncedSearchTerm = useDebounce(searchTerm, 500);

  useEffect(() => {
    if (debouncedSearchTerm) {
      // Perform search
      performSearch(debouncedSearchTerm);
    }
  }, [debouncedSearchTerm]);

  return (
    <input
      value={searchTerm}
      onChange={(e) => setSearchTerm(e.target.value)}
      placeholder="Search..."
    />
  );
}
```

### 4. useClickOutside Hook

Detect click outside element:

```javascript
import { useEffect, useRef } from 'react';

function useClickOutside(callback) {
  const ref = useRef();

  useEffect(() => {
    function handleClickOutside(event) {
      if (ref.current && !ref.current.contains(event.target)) {
        callback();
      }
    }

    document.addEventListener('mousedown', handleClickOutside);
    return () => {
      document.removeEventListener('mousedown', handleClickOutside);
    };
  }, [callback]);

  return ref;
}

// Usage
function Dropdown() {
  const [isOpen, setIsOpen] = useState(false);
  const ref = useClickOutside(() => setIsOpen(false));

  return (
    <div ref={ref}>
      <button onClick={() => setIsOpen(!isOpen)}>Toggle</button>
      {isOpen && <div>Dropdown content</div>}
    </div>
  );
}
```

## Best Practices

### 1. Naming Convention

Luôn bắt đầu với "use":

```javascript
// ✅ Good
function useAuth() { }
function useWindowSize() { }

// ❌ Bad
function auth() { }
function getWindowSize() { }
```

### 2. Single Responsibility

Mỗi hook chỉ làm một việc:

```javascript
// ✅ Good
function useUser(userId) { }
function useUserPosts(userId) { }

// ❌ Bad
function useUserAndPosts(userId) { }
```

### 3. Return Consistent Structure

Luôn return cùng một structure:

```javascript
// ✅ Good - always returns { data, loading, error }
function useFetch(url) {
  return { data, loading, error };
}

// ❌ Bad - inconsistent returns
function useFetch(url) {
  if (loading) return loading;
  if (error) return error;
  return data;
}
```

## Kết luận

Custom Hooks là một trong những tính năng mạnh mẽ nhất của React. Chúng giúp bạn viết code sạch hơn, tái sử dụng được, và dễ test hơn. Hãy bắt đầu tạo custom hooks cho logic tái sử dụng trong dự án của bạn!

