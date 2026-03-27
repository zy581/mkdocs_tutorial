# 基本配置

## 站点信息配置

### 站点名称和描述

```yaml
site_name: My Documentation Site
site_url: https://example.com/docs
site_author: Your Name
site_description: Professional documentation for your project
```

### 版权信息

```yaml
copyright: © 2024 Your Company. All rights reserved.
```

## 仓库集成

### GitHub集成

```yaml
repo_name: your-username/your-repo
repo_url: https://github.com/your-username/your-repo
```

### 编辑链接

```yaml
edit_uri: edit/main/docs/
```

这会在每个页面添加"编辑此页面"的链接。

## 目录结构配置

### 自定义文档目录

```yaml
docs_dir: documentation
```

### 自定义输出目录

```yaml
site_dir: public
```

### 排除文件

```yaml
exclude_docs: |
  /drafts/*
  /private/*
```

## 主题配置

### 基本主题设置

```yaml
theme:
  name: material
  language: zh-CN
  palette:
    - scheme: default
      primary: 'blue'
      accent: 'blue'
      toggle:
        icon: material/weather-night
        name: 切换到深色模式
```

### 字体配置

```yaml
theme:
  font:
    text: Roboto
    code: Roboto Mono
```

## 导航配置

### 基本导航结构

```yaml
nav:
  - 首页: index.md
  - 快速开始: quickstart.md
  - 用户指南:
    - 安装: guide/installation.md
    - 配置: guide/configuration.md
    - 使用: guide/usage.md
  - API参考: api/
  - 常见问题: faq.md
  - 关于: about.md
```

### 嵌套导航

```yaml
nav:
  - 首页: index.md
  - 用户指南:
    - 入门:
      - 安装: guide/getting-started/installation.md
      - 快速开始: guide/getting-started/quickstart.md
    - 进阶:
      - 配置详解: guide/advanced/configuration.md
      - 最佳实践: guide/advanced/best-practices.md
  - 开发者:
    - API文档: api/index.md
    - 贡献指南: contributing.md
```

### 导航选项

```yaml
theme:
  features:
    - navigation.tabs        # 顶部标签导航
    - navigation.sections    # 侧边栏分组
    - navigation.expand      # 自动展开所有章节
    - navigation.indexes     # 自动生成索引页面
```

## 插件配置

### 搜索插件

```yaml
plugins:
  - search:
      separator: '[\s\-\.]+'
      lang:
        - en
        - de
```

### Git修订日期

```yaml
plugins:
  - git-revision-date-localized:
      type: timeago
      timezone: Asia/Shanghai
      locale: zh_CN
```

### 压缩插件

```yaml
plugins:
  - minify:
      minify_html: true
      minify_css: true
      minify_js: true
```

## Markdown扩展配置

### 启用扩展

```yaml
markdown_extensions:
  - attr_list              # 属性列表
  - def_list               # 定义列表
  - footnotes              # 脚注
  - meta                   # 元数据
  - toc:                   # 目录
      permalink: true
```

### 高级扩展配置

```yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
```

## 额外配置

### 社交媒体链接

```yaml
extra:
  social:
    - icon: fontawesome/brands/github
      link: https://github.com/your-username
      name: GitHub
    - icon: fontawesome/brands/twitter
      link: https://twitter.com/your-username
      name: Twitter
```

### Google Analytics

```yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX
```

### 自定义变量

```yaml
extra:
  version: '1.0.0'
  project_name: 'My Project'
  company_name: 'My Company'
```

## 环境配置

### 开发环境

```yaml
# 开发环境配置
dev_addr: 127.0.0.1:8000
strict: false
```

### 生产环境

```yaml
# 生产环境配置
strict: true
```

---

**下一步**: [主题定制](theming.md)