# 性能优化

优化MkDocs站点的性能可以提供更好的用户体验并改善SEO排名。

## 加载性能优化

### 1. 资源压缩

```yaml
plugins:
  - minify:
      minify_html: true
      minify_css: true
      minify_js: true
      minify_images: true
      htmlmin_opts:
        remove_comments: true
        remove_empty_elements: true
        remove_optional_tags: true
      cssmin_opts:
        compatibility: '*'
      jsmin_opts:
        mangle: true
        compress:
          drop_console: true
          drop_debugger: true
```

### 2. 图片优化

```bash
# 安装图片优化工具
pip install pillow
pip install imageoptim

# 优化PNG图片
imageoptim --quality=medium docs/assets/images/*.png

# 优化JPEG图片
imageoptim --quality=medium --format=jpeg docs/assets/images/*.jpg
```

### 3. 使用WebP格式

```yaml
plugins:
  - minify:
      webp_conversion: true
      webp_quality: 80
      webp_args:
        - -q 80
        - -m 6
        - -af
        - -f 0.1
```

### 4. 资源预加载

```yaml
extra:
  preload:
    - href: /assets/css/main.css
      as: style
      crossorigin: anonymous
    - href: /assets/js/main.js
      as: script
      crossorigin: anonymous
    - href: /assets/images/logo.png
      as: image
      crossorigin: anonymous
```

## 缓存策略

### 1. 浏览器缓存

```nginx
# Nginx配置
location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
  expires 1y;
  add_header Cache-Control "public, immutable";
  add_header ETag "";
}

location / {
  expires -1;
  add_header Cache-Control "no-cache, no-store, must-revalidate";
}
```

### 2. Service Worker缓存

```javascript
// docs/assets/js/sw.js
const CACHE_NAME = 'mkdocs-v1';
const urlsToCache = [
  '/',
  '/assets/css/main.css',
  '/assets/js/main.js',
  '/assets/images/logo.png'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(urlsToCache))
  );
});

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        if (response) {
          return response;
        }
        return fetch(event.request);
      })
  );
});
```

```html
<!-- 注册Service Worker -->
<script>
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/assets/js/sw.js');
  });
}
</script>
```

### 3. CDN缓存

```yaml
# Cloudflare配置
extra:
  cdn:
    provider: cloudflare
    zone_id: YOUR_ZONE_ID
    api_token: YOUR_API_TOKEN

# 缓存规则
cache_rules:
  - url: /*.js
    cache_ttl: 86400
  - url: /*.css
    cache_ttl: 86400
  - url: /*.png
    cache_ttl: 604800
  - url: /api/*
    cache_ttl: 0
```

## 代码优化

### 1. 减少HTTP请求

```css
/* 合并CSS文件 */
/* 不推荐 */
@import url('reset.css');
@import url('typography.css');
@import url('layout.css');
@import url('components.css');

/* 推荐 - 合并为一个文件 */
/* main.css */
/* 包含所有CSS */
```

### 2. 延迟加载

```javascript
// docs/assets/js/lazy-load.js
document.addEventListener('DOMContentLoaded', function() {
  const images = document.querySelectorAll('img[loading="lazy"]');
  const imageObserver = new IntersectionObserver((entries, observer) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const img = entry.target;
        img.src = img.dataset.src;
        img.classList.remove('lazy');
        imageObserver.unobserve(img);
      }
    });
  });

  images.forEach(img => imageObserver.observe(img));
});
```

```html
<!-- 使用延迟加载的图片 -->
<img data-src="image.jpg" class="lazy" alt="描述文本" loading="lazy">
```

### 3. 关键CSS内联

```html
<!-- 在<head>中内联关键CSS -->
<style>
  /* 关键路径CSS */
  .md-header {
    background-color: #1976D2;
    color: white;
  }

  .md-content {
    padding: 2rem;
    max-width: 900px;
    margin: 0 auto;
  }

  .md-main {
    min-height: 100vh;
  }
</style>
```

## 构建优化

### 1. 增量构建

```bash
# 启用增量构建
mkdocs build --incremental

# 使用缓存
mkdocs build --cache
mkdocs build --cache-dir .cache
```

### 2. 并行构建

```yaml
# 使用多进程构建
plugins:
  - parallel:
      workers: 4
      enabled: true
```

### 3. 构建时间优化

```yaml
# 禁用不必要的插件
plugins:
  - search:
      enabled: true
  - git-revision-date-localized:
      enabled: true
  - minify:
      enabled: true
  # - 其他可能影响构建时间的插件: false
```

## SEO性能优化

### 1. 核心Web指标

```css
/* 优化CLS（累积布局偏移） */
img {
  width: 100%;
  height: auto;
}

video {
  width: 100%;
  height: auto;
}

/* 优化LCP（最大内容绘制） */
.md-content h1 {
  content-visibility: auto;
  contain-intrinsic-size: 0 5rem;
}

.md-content p {
  content-visibility: auto;
  contain-intrinsic-size: 0 3rem;
}
```

### 2. 预连接和预加载

```yaml
extra:
  preload:
    - href: https://fonts.googleapis.com
      rel: preconnect
      crossorigin: true
    - href: https://fonts.gstatic.com
      rel: preconnect
      crossorigin: true
    - href: /assets/css/main.css
      rel: preload
      as: style
    - href: /assets/js/main.js
      rel: preload
      as: script
```

### 3. 服务器响应优化

```nginx
# 启用Gzip压缩
gzip on;
gzip_vary on;
gzip_types
  text/plain
  text/css
  text/xml
  text/javascript
  application/javascript
  application/xml+rss
  application/json
  application/vnd.ms-fontobject
  font/truetype
  font/opentype
  image/svg+xml;

# 启用Brotli压缩
brotli on;
brotli_comp_level 6;
brotli_types
  text/plain
  text/css
  text/xml
  text/javascript
  application/javascript
  application/xml+rss
  application/json;

# HTTP/2服务器推送
http2_push /assets/css/main.css;
http2_push /assets/js/main.js;
```

## 监控和分析

### 1. 性能监控

```yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX

    # 核心Web指标监控
    web_vitals: true

    # 性能监控
    performance:
      timing:
        - 'navigationStart'
        - 'loadEventEnd'
        - 'domContentLoadedEventEnd'
        - 'firstContentfulPaint'
        - 'firstInputDelay'
        - 'largestContentfulPaint'
        - 'cumulativeLayoutShift'
        - 'layoutShift'
```

### 2. Lighthouse CI

```yaml
# .github/workflows/lighthouse.yml
name: Lighthouse CI

on: [push]

jobs:
  lighthouse:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Lighthouse on production
        uses: treosh/lighthouse-ci-action@v9
        with:
          urls: |
            https://your-site.com
            https://your-site.com/docs/
          budgetPath: ./budget.json
          uploadArtifacts: true
          temporaryPublicStorage: true
```

```json
// budget.json
[
  {
    "path": "/*",
    "resourceSizes": [
      {
        "resourceType": "document",
        "budget": 80
      },
      {
        "resourceType": "stylesheet",
        "budget": 50
      },
      {
        "resourceType": "image",
        "budget": 200
      },
      {
        "resourceType": "media",
        "budget": 200
      },
      {
        "resourceType": "font",
        "budget": 80
      },
      {
        "resourceType": "total",
        "budget": 500
      }
    ],
    "resourceCounts": [
      {
        "resourceType": "third-party",
        "budget": 5
      }
    ]
  }
]
```

### 3. 实时监控

```javascript
// docs/assets/js/performance.js
// 监控页面加载性能
window.addEventListener('load', function() {
  const perfData = window.performance.timing;
  const pageLoadTime = perfData.loadEventEnd - perfData.navigationStart;
  const domReadyTime = perfData.domContentLoadedEventEnd - perfData.navigationStart;

  // 发送性能数据到分析服务
  if (pageLoadTime > 3000) {
    console.warn('Page load time exceeded 3 seconds:', pageLoadTime);
  }

  // 监控Core Web Vitals
  if ('web-vital' in window) {
    const { getCLS, getFID, getLCP } = window.webVital;

    getCLS(console.log);
    getFID(console.log);
    getLCP(console.log);
  }
});
```

## 移动端优化

### 1. 响应式图片

```markdown
<!-- 使用srcset和sizes属性 -->
![响应式图片](image.jpg){: srcset="image-480.jpg 480w, image-800.jpg 800w, image-1200.jpg 1200w" sizes="(max-width: 600px) 480px, (max-width: 900px) 800px, 1200px" }
```

### 2. 触摸优化

```css
/* 优化触摸交互 */
@media (touch-enabled) {
  .md-content a {
    min-height: 44px;
    min-width: 44px;
  }

  .md-button {
    padding: 12px 20px;
    min-height: 44px;
  }

  .md-nav__link {
    padding: 12px 0;
  }
}
```

### 3. 省电模式优化

```javascript
// 检测设备电量
if ('getBattery' in navigator) {
  navigator.getBattery().then(battery => {
    battery.addEventListener('levelchange', () => {
      if (battery.level < 0.2 && !battery.charging) {
        // 低电量模式，减少动画
        document.documentElement.style.scrollBehavior = 'auto';
        document.querySelectorAll('*').forEach(el => {
          el.style.animation = 'none';
          el.style.transition = 'none';
        });
      }
    });
  });
}
```

## 部署优化

### 1. 边缘计算

```yaml
# Vercel边缘函数配置
{
  "functions": {
    "api/performance.js": {
      "maxDuration": 10
    }
  },
  "rewrites": [
    { "source": "/performance", "destination": "/api/performance.js" }
  ]
}
```

### 2. 智能缓存

```yaml
# Netlify智能缓存
[[plugins]]
  package = "netlify-plugin-cache"
  [plugins.inputs]
    paths = [".cache", "site/.cache"]

# 基于内容哈希的缓存
plugins:
  - cache_bust:
      enabled: true
      method: hash
      extensions: ['.css', '.js', '.png', '.jpg']
```

---

**最后一步**: 更新首页内容并运行测试