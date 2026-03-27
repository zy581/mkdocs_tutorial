# 主题定制

## 颜色方案

### 基本颜色配置

Material主题提供了丰富的颜色方案配置选项：

```yaml
theme:
  palette:
    # 浅色模式
    - scheme: default
      primary: 'blue'
      accent: 'blue'
      toggle:
        icon: material/weather-night
        name: 切换到深色模式

    # 深色模式
    - scheme: slate
      primary: 'blue'
      accent: 'blue'
      toggle:
        icon: material/weather-sunny
        name: 切换到浅色模式
```

### 预定义颜色选项

Material主题支持以下预定义颜色：

**主要颜色(primary):**
- `red` - 红色
- `pink` - 粉色
- `purple` - 紫色
- `deep purple` - 深紫色
- `indigo` - 靛蓝色
- `blue` - 蓝色
- `light blue` - 浅蓝色
- `cyan` - 青色
- `teal` - 水鸭色
- `green` - 绿色
- `light green` - 浅绿色
- `lime` - 酸橙色
- `yellow` - 黄色
- `amber` - 琥珀色
- `orange` - 橙色
- `deep orange` - 深橙色
- `brown` - 棕色
- `grey` - 灰色
- `blue grey` - 蓝灰色

**强调颜色(accent):**
- 使用`'dark'`或`'light'`前缀
- 例如: `'blue darken-3'`, `'pink lighten-1'`

### 自定义颜色

如果你想使用自定义颜色，可以在CSS中覆盖默认变量：

```css
/* docs/assets/css/custom.css */
:root {
  --md-primary-fg-color: #1976D2;
  --md-primary-fg-color--light: #42A5F5;
  --md-primary-fg-color--dark: #1565C0;
  --md-accent-fg-color: #FF4081;
}
```

然后在配置中启用：

```yaml
theme:
  custom_dir: docs/assets/css
```

## 字体配置

### 谷歌字体

```yaml
theme:
  font:
    text: Roboto
    code: Roboto Mono
```

### 禁用谷歌字体

```yaml
theme:
  font: false
```

### 自定义字体

```css
/* docs/assets/css/custom.css */
:root {
  --md-text-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --md-code-font-family: 'Fira Code', 'Courier New', monospace;
}
```

## 主题功能

### 导航功能

```yaml
theme:
  features:
    - navigation.tabs           # 顶部标签导航
    - navigation.sections       # 侧边栏分组显示
    - navigation.expand         # 自动展开所有章节
    - navigation.indexes        # 自动生成索引页面
    - navigation.top            # 返回顶部按钮
    - navigation.footer         # 页脚导航
    - navigation.instant        # 即时加载
    - navigation.tracking       # URL自动跟踪
```

### 搜索功能

```yaml
theme:
  features:
    - search.suggest            # 搜索建议
    - search.highlight          # 搜索结果高亮
    - search.share              # 搜索结果分享
```

### 内容功能

```yaml
theme:
  features:
    - content.code.annotate     # 代码注释
    - content.code.copy         # 复制代码按钮
    - content.action.edit       # 编辑按钮
    - content.action.view       # 查看源文件
```

## 语言配置

### 支持的语言

```yaml
theme:
  language: zh-CN
```

### 多语言支持

```yaml
plugins:
  - i18n:
      default_language: zh-CN
      languages:
        zh-CN: 中文
        en: English
```

## 图标和Logo

### Logo配置

```yaml
theme:
  logo: assets/images/logo.png
```

### Favicon配置

```yaml
theme:
  favicon: assets/images/favicon.png
```

### 自定义图标

```yaml
extra:
  icons:
    - icon: fontawesome/brands/github
      link: https://github.com/your-username
```

## 深色模式配置

### 自动切换

```yaml
theme:
  palette:
    - media: '(prefers-color-scheme: light)'
      scheme: default
      primary: 'blue'
      accent: 'blue'
      toggle:
        icon: material/weather-night
        name: 切换到深色模式

    - media: '(prefers-color-scheme: dark)'
      scheme: slate
      primary: 'blue'
      accent: 'blue'
      toggle:
        icon: material/weather-sunny
        name: 切换到浅色模式
```

### 强制默认模式

```yaml
theme:
  palette:
    scheme: default  # 强制使用浅色模式
    # 或
    scheme: slate    # 强制使用深色模式
```

## 主题变量覆盖

### 使用CSS变量

```css
/* docs/assets/css/custom.css */
:root {
  --md-primary-fg-color: #1976D2;
  --md-primary-fg-color--light: #42A5F5;
  -md-primary-fg-color--dark: #1565C0;
  --md-accent-fg-color: #FF4081;

  /* 文字颜色 */
  --md-text-color: #212121;
  --md-text-secondary-color: #757575;

  /* 背景颜色 */
  --md-background-color: #FFFFFF;
  --md-background-secondary-color: #F5F5F5;

  /* 代码块样式 */
  --md-code-background-color: #F5F5F5;
  --md-code-text-color: #212121;
}
```

### 响应式设计

```css
/* docs/assets/css/custom.css */
@media (max-width: 768px) {
  :root {
    --md-text-font-size: 14px;
  }
}

@media (min-width: 769px) {
  :root {
    --md-text-font-size: 16px;
  }
}
```

## 主题继承

### 创建自定义主题

```yaml
theme:
  name: material
  custom_dir: docs/theme
```

### 继承基础主题

在你的自定义主题中，可以继承Material的基础样式：

```css
/* docs/theme/main.css */
@import url('material/theme.css');

/* 你的自定义样式 */
.custom-style {
  /* ... */
}
```

---

**下一步**: [插件使用](plugins.md)