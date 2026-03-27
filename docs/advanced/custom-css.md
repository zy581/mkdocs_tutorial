# 自定义CSS

Material for MkDocs允许你通过自定义CSS来完全控制文档的外观和感觉。

## 启用自定义样式

### 1. 创建自定义CSS目录

```bash
mkdir -p docs/assets/css
mkdir -p docs/assets/js
mkdir -p docs/assets/images
```

### 2. 配置主题

在`mkdocs.yml`中启用自定义目录：

```yaml
theme:
  name: material
  custom_dir: docs/assets/css
```

### 3. 创建主样式文件

创建`docs/assets/css/main.css`：

```css
/* 自定义样式主文件 */

/* 导入Material基础样式 */
@import url('material/theme.css');

/* 你的自定义样式 */
:root {
  /* 颜色变量 */
  --md-primary-fg-color: #1976D2;
  --md-primary-fg-color--light: #42A5F5;
  --md-primary-fg-color--dark: #1565C0;
  --md-accent-fg-color: #FF4081;

  /* 字体变量 */
  --md-text-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --md-code-font-family: 'Fira Code', 'Courier New', monospace;

  /* 尺寸变量 */
  --md-content-max-width: 900px;
  --md-code-font-size: 14px;
}
```

## 基础样式覆盖

### 颜色定制

```css
/* docs/assets/css/custom.css */

/* 主色调 */
:root {
  --md-primary-fg-color: #2E7D32;
  --md-primary-fg-color--light: #4CAF50;
  --md-primary-fg-color--dark: #1B5E20;
  --md-accent-fg-color: #FF9800;
}

/* 深色模式颜色 */
[data-md-color-scheme="slate"] {
  --md-primary-fg-color: #4CAF50;
  --md-primary-fg-color--light: #81C784;
  --md-primary-fg-color--dark: #388E3C;
  --md-accent-fg-color: #FFB74D;
}

/* 背景颜色 */
:root {
  --md-background-color: #FFFFFF;
  --md-background-secondary-color: #F5F5F5;
  --md-code-background-color: #F5F5F5;
}

[data-md-color-scheme="slate"] {
  --md-background-color: #121212;
  --md-background-secondary-color: #1E1E1E;
  --md-code-background-color: #2D2D2D;
}
```

### 字体定制

```css
/* 自定义字体 */
:root {
  --md-text-font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --md-code-font-family: 'JetBrains Mono', 'Fira Code', monospace;
}

/* 字体大小 */
:root {
  --md-text-font-size: 16px;
  --md-text-font-size--large: 18px;
  --md-text-font-size--small: 14px;
  --md-code-font-size: 14px;
}

/* 移动端字体大小 */
@media (max-width: 768px) {
  :root {
    --md-text-font-size: 14px;
    --md-code-font-size: 12px;
  }
}
```

### 间距和布局

```css
/* 内容区域最大宽度 */
:root {
  --md-content-max-width: 900px;
}

/* 页面边距 */
.md-main {
  padding: 2rem 1rem;
}

/* 移动端边距 */
@media (max-width: 768px) {
  .md-main {
    padding: 1rem 0.5rem;
  }
}

/* 导航栏间距 */
.md-header {
  padding: 0 1rem;
}

/* 页脚间距 */
.md-footer {
  padding: 2rem 1rem;
}
```

## 组件样式

### 导航栏

```css
/* 导航栏样式 */
.md-header {
  background-color: var(--md-primary-fg-color);
  color: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* 导航链接 */
.md-header-nav__link {
  color: rgba(255, 255, 255, 0.87);
  font-weight: 500;
}

.md-header-nav__link:hover {
  color: white;
  text-decoration: underline;
}

/* 当前页面高亮 */
.md-header-nav__link--active {
  color: white;
  font-weight: 600;
}

/* 搜索框 */
.md-search__input {
  background-color: rgba(255, 255, 255, 0.1);
  color: white;
}

.md-search__input::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

/* 移动端导航 */
.md-header--shadow {
  box-shadow: 0 2px 8px rgba(0,0,0,0.15);
}
```

### 侧边栏

```css
/* 侧边栏样式 */
.md-sidebar {
  background-color: var(--md-background-secondary-color);
  border-right: 1px solid rgba(0,0,0,0.12);
}

/* 侧边栏标题 */
.md-sidebar__scrollwrap {
  padding: 1rem 0;
}

.md-sidebar__inner {
  padding: 0 1rem;
}

/* 侧边栏链接 */
.md-nav__link {
  color: var(--md-text-color);
  font-weight: 400;
  padding: 0.5rem 0;
  border-radius: 4px;
  transition: all 0.2s ease;
}

.md-nav__link:hover {
  background-color: rgba(0,0,0,0.04);
  padding-left: 0.5rem;
}

/* 当前章节高亮 */
.md-nav__link--active {
  color: var(--md-primary-fg-color);
  font-weight: 600;
  background-color: rgba(25, 118, 210, 0.1);
}

/* 子菜单缩进 */
.md-nav__item--nested > .md-nav__link {
  padding-left: 1rem;
}

.md-nav__item--nested .md-nav__link {
  padding-left: 2rem;
}
```

### 内容区域

```css
/* 内容区域 */
.md-content {
  background-color: var(--md-background-color);
  padding: 2rem;
}

/* 移动端内容区域 */
@media (max-width: 768px) {
  .md-content {
    padding: 1rem;
  }
}

/* 标题样式 */
.md-content h1 {
  color: var(--md-primary-fg-color);
  font-size: 2.25rem;
  font-weight: 700;
  margin: 2rem 0 1rem;
  border-bottom: 2px solid var(--md-primary-fg-color--light);
  padding-bottom: 0.5rem;
}

.md-content h2 {
  color: var(--md-primary-fg-color--dark);
  font-size: 1.75rem;
  font-weight: 600;
  margin: 1.5rem 0 0.75rem;
}

.md-content h3 {
  font-size: 1.5rem;
  font-weight: 600;
  margin: 1.25rem 0 0.5rem;
}

/* 段落样式 */
.md-content p {
  line-height: 1.7;
  margin: 0.75rem 0;
  color: var(--md-text-color);
}

/* 链接样式 */
.md-content a {
  color: var(--md-primary-fg-color);
  text-decoration: none;
  font-weight: 500;
}

.md-content a:hover {
  text-decoration: underline;
  color: var(--md-accent-fg-color);
}

/* 引用块样式 */
.md-content blockquote {
  background-color: var(--md-background-secondary-color);
  border-left: 4px solid var(--md-primary-fg-color);
  padding: 1rem 1.5rem;
  margin: 1rem 0;
  border-radius: 0 4px 4px 0;
}

.md-content blockquote p {
  margin: 0;
}
```

### 代码块样式

```css
/* 代码块容器 */
.md-content pre {
  background-color: var(--md-code-background-color);
  border-radius: 8px;
  padding: 1rem;
  margin: 1rem 0;
  overflow-x: auto;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* 内联代码 */
.md-content code {
  background-color: var(--md-code-background-color);
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
  font-size: 0.9em;
  font-family: var(--md-code-font-family);
}

/* 代码高亮 */
.highlight {
  background-color: var(--md-code-background-color);
}

.highlight .c { color: #6A9955; } /* 注释 */
.highlight .k { color: #569CD6; } /* 关键字 */
.highlight .n { color: #9CDCFE; } /* 标识符 */
.highlight .s { color: #CE9178; } /* 字符串 */
.highlight .o { color: #DCDCAA; } /* 操作符 */
.highlight .mi { color: #B5CEA8; } /* 数字 */

/* 行号 */
.linenos {
  color: #858585;
  background-color: #2D2D2D;
  padding-right: 1rem;
  border-right: 1px solid #404040;
}

/* 复制按钮 */
.md-clipboard {
  color: var(--md-primary-fg-color);
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 4px;
  padding: 0.25rem;
}

.md-clipboard:hover {
  background-color: rgba(255, 255, 255, 0.2);
}
```

### 表格样式

```css
/* 表格容器 */
.md-content table {
  border-collapse: collapse;
  width: 100%;
  margin: 1rem 0;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
  border-radius: 8px;
  overflow: hidden;
}

/* 表头 */
.md-content th {
  background-color: var(--md-primary-fg-color);
  color: white;
  font-weight: 600;
  padding: 0.75rem;
  text-align: left;
}

/* 表格单元格 */
.md-content td {
  padding: 0.75rem;
  border-bottom: 1px solid rgba(0,0,0,0.12);
}

/* 斑马纹效果 */
.md-content tr:nth-child(even) {
  background-color: var(--md-background-secondary-color);
}

/* 悬停效果 */
.md-content tr:hover {
  background-color: rgba(25, 118, 210, 0.04);
}
```

## 响应式设计

### 移动端优化

```css
/* 基础移动端样式 */
@media (max-width: 768px) {
  :root {
    --md-text-font-size: 14px;
    --md-code-font-size: 12px;
  }

  /* 导航栏 */
  .md-header {
    padding: 0 0.5rem;
  }

  .md-header-nav__link {
    font-size: 0.9rem;
    padding: 0.5rem 0.25rem;
  }

  /* 内容区域 */
  .md-content {
    padding: 1rem;
  }

  .md-content h1 {
    font-size: 1.75rem;
  }

  .md-content h2 {
    font-size: 1.5rem;
  }

  .md-content h3 {
    font-size: 1.25rem;
  }

  /* 侧边栏 */
  .md-sidebar {
    width: 250px;
  }

  /* 代码块 */
  .md-content pre {
    padding: 0.75rem;
    margin: 0.75rem 0;
  }

  /* 表格滚动 */
  .md-content table {
    display: block;
    overflow-x: auto;
    white-space: nowrap;
  }
}

/* 小屏幕手机 */
@media (max-width: 480px) {
  .md-content {
    padding: 0.75rem;
  }

  .md-content h1 {
    font-size: 1.5rem;
  }

  .md-content h2 {
    font-size: 1.25rem;
  }

  .md-content h3 {
    font-size: 1.1rem;
  }
}
```

### 平板优化

```css
@media (min-width: 769px) and (max-width: 1024px) {
  .md-content {
    padding: 1.5rem;
  }

  .md-sidebar {
    width: 280px;
  }

  .md-content h1 {
    font-size: 2rem;
  }
}
```

## 动画和交互

### 平滑滚动

```css
/* 平滑滚动 */
html {
  scroll-behavior: smooth;
}

/* 自定义滚动条 */
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: var(--md-background-secondary-color);
}

::-webkit-scrollbar-thumb {
  background: var(--md-primary-fg-color);
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: var(--md-primary-fg-color--dark);
}
```

### 悬停效果

```css
/* 卡片悬停效果 */
.md-content .admonition,
.md-content .md-typeset__table {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.md-content .admonition:hover,
.md-content .md-typeset__table:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

/* 链接悬停动画 */
.md-content a {
  transition: color 0.2s ease, text-decoration 0.2s ease;
}

/* 按钮悬停效果 */
.md-button {
  transition: all 0.2s ease;
}

.md-button:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}
```

## 主题切换

### 深色模式切换

```css
/* 切换按钮样式 */
.md-header__option {
  display: flex;
  align-items: center;
}

/* 深色模式切换动画 */
[data-md-color-scheme] {
  transition: background-color 0.3s ease, color 0.3s ease;
}

/* 深色模式特定样式 */
[data-md-color-scheme="slate"] {
  --md-text-color: #E0E0E0;
  --md-text-secondary-color: #9E9E9E;
  --md-background-color: #121212;
  --md-background-secondary-color: #1E1E1E;
}

/* 深色模式下的代码块 */
[data-md-color-scheme="slate"] .md-content pre {
  background-color: #2D2D2D;
}

[data-md-color-scheme="slate"] .highlight .c { color: #999999; }
[data-md-color-scheme="slate"] .highlight .k { color: #FF79C6; }
[data-md-color-scheme="slate"] .highlight .n { color: #F8F8F2; }
[data-md-color-scheme="slate"] .highlight .s { color: #F1FA8C; }
```

### 自动主题切换

```css
/* 根据系统偏好自动切换 */
@media (prefers-color-scheme: dark) {
  :root {
    --md-color-scheme: slate;
  }
}

@media (prefers-color-scheme: light) {
  :root {
    --md-color-scheme: default;
  }
}
```

## 自定义组件

### 提示框自定义

```css
/* 自定义提示框样式 */
.admonition {
  border-radius: 8px;
  border-left: 4px solid;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

/* 不同提示类型 */
.admonition.note {
  border-left-color: #2196F3;
  background-color: rgba(33, 150, 243, 0.1);
}

.admonition.warning {
  border-left-color: #FF9800;
  background-color: rgba(255, 152, 0, 0.1);
}

.admonition.error {
  border-left-color: #F44336;
  background-color: rgba(244, 67, 54, 0.1);
}

.admonition.success {
  border-left-color: #4CAF50;
  background-color: rgba(76, 175, 80, 0.1);
}

/* 提示框标题 */
.admonition-title {
  font-weight: 600;
  padding: 0.75rem 1rem;
  margin: 0;
  border-bottom: 1px solid rgba(0,0,0,0.1);
}

.admonition-title::before {
  display: none; /* 隐藏默认图标 */
}

/* 提示框内容 */
.admonition-content {
  padding: 1rem;
  margin: 0;
}
```

### 按钮样式

```css
/* 自定义按钮 */
.md-button {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  background-color: var(--md-primary-fg-color);
  color: white;
  text-decoration: none;
  border-radius: 6px;
  font-weight: 500;
  transition: all 0.2s ease;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.md-button:hover {
  background-color: var(--md-primary-fg-color--dark);
  color: white;
  text-decoration: none;
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}

/* 次要按钮 */
.md-button--secondary {
  background-color: transparent;
  color: var(--md-primary-fg-color);
  border: 2px solid var(--md-primary-fg-color);
}

.md-button--secondary:hover {
  background-color: var(--md-primary-fg-color);
  color: white;
}

/* 成功按钮 */
.md-button--success {
  background-color: #4CAF50;
}

.md-button--success:hover {
  background-color: #45a049;
}

/* 警告按钮 */
.md-button--warning {
  background-color: #FF9800;
}

.md-button--warning:hover {
  background-color: #e68900;
}

/* 危险按钮 */
.md-button--danger {
  background-color: #F44336;
}

.md-button--danger:hover {
  background-color: #da190b;
}

/* 按钮大小 */
.md-button--small {
  padding: 0.5rem 1rem;
  font-size: 0.9rem;
}

.md-button--large {
  padding: 1rem 2rem;
  font-size: 1.1rem;
}

/* 按钮组 */
.button-group {
  display: flex;
  gap: 0.5rem;
  margin: 1rem 0;
}

@media (max-width: 768px) {
  .button-group {
    flex-direction: column;
  }
}
```

### 卡片组件

```css
/* 卡片组件 */
.card {
  background-color: var(--md-background-color);
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  padding: 1.5rem;
  margin: 1rem 0;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 16px rgba(0,0,0,0.15);
}

/* 卡片标题 */
.card-title {
  color: var(--md-primary-fg-color);
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0 0 0.75rem 0;
}

/* 卡片内容 */
.card-content {
  color: var(--md-text-color);
  line-height: 1.6;
}

/* 卡片页脚 */
.card-footer {
  border-top: 1px solid rgba(0,0,0,0.1);
  padding-top: 1rem;
  margin-top: 1rem;
}

/* 卡片网格 */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin: 1.5rem 0;
}

@media (max-width: 768px) {
  .card-grid {
    grid-template-columns: 1fr;
  }
}
```

## 性能优化

### 关键CSS内联

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
  }
</style>
```

### 异步加载CSS

```javascript
// docs/assets/js/load-css.js
function loadCSS(href) {
  const link = document.createElement('link');
  link.rel = 'stylesheet';
  link.href = href;
  document.head.appendChild(link);
}

// 延迟加载非关键CSS
window.addEventListener('load', () => {
  loadCSS('assets/css/non-critical.css');
});
```

### CSS压缩

```bash
# 使用CSSNano压缩
npm install cssnano-cli --save-dev
npx cssnano docs/assets/css/main.css docs/assets/css/main.min.css
```

---

**下一步**: [多语言支持](i18n.md)