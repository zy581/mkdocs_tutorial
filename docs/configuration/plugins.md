# 插件使用

## 核心插件

### 搜索插件

搜索插件是Material主题的核心功能：

```yaml
plugins:
  - search:
      # 搜索分隔符
      separator: '[\s\-\.]+'

      # 支持的语言
      lang:
        - en
        - de
        - fr
        - es
        - it
        - nl
        - ru
        - pt
        - ja
        - ko
        - zh-CN

      # 搜索范围
      scope: '.md-content'

      # 是否包含标题
      include_title: true

      # 是否包含代码
      include_code: true
```

### 优化插件

#### HTML压缩

```yaml
plugins:
  - minify:
      minify_html: true
      minify_css: true
      minify_js: true
      htmlmin_opts:
        remove_comments: true
        remove_empty_elements: true
        remove_optional_tags: true
```

#### 图片优化

```yaml
plugins:
  - minify:
      minify_images: true
      images_ext:
        - .jpg
        - .jpeg
        - .png
        - .gif
```

### Git集成插件

#### 修订日期

```yaml
plugins:
  - git-revision-date-localized:
      type: timeago          # timeago, date, datetime
      timezone: Asia/Shanghai
      locale: zh_CN
      fallback_to_build_date: true
      enable_creation_date: true
```

#### Git历史

```yaml
plugins:
  - git-authors:
      show_contributors: true
      show_last_modified: true
```

## 功能增强插件

### 目录增强

```yaml
plugins:
  - toc:
      permalink: true        # 添加永久链接
      toc_depth: 3           # 目录深度
      title: '目录'          # 目录标题
```

### 页面优化

```yaml
plugins:
  - meta:
      enable: true
      description: true
      keywords: true
      author: true
      date: true
```

### SEO优化

```yaml
plugins:
  - seo:
      site_name: My Site
      twitter: '@your-username'
      image: assets/images/og-image.png
```

## 高级插件

### 多语言支持

```yaml
plugins:
  - i18n:
      default_language: zh-CN
      languages:
        zh-CN: 中文
        en: English
        ja: 日本語
        es: Español

      # 语言切换器
      lang_name: 语言
      lang_icon: material/translate

      # 自动生成翻译
      auto_translate: true
```

### 博客功能

```yaml
plugins:
  - blog:
      dir: blog              # 博客目录
      posts_dir: posts       # 文章目录
      page: 'index.md'       # 博客首页

      # 文章配置
      post_date_format: 'yyyy-MM-dd'
      post_url_format: '{category}/{slug}'

      # 分页
      paginate: true
      paginate_by: 10
```

### 代码文档

```yaml
plugins:
  - mkdocstrings:
      handlers:
        python:
          setup_commands:
            - import sys; sys.path.append('src')
          selection:
            docstring_style: google
            docstring_options:
              replace_admonitions: true
          rendering:
            show_root_heading: true
            show_source: true
            show_signature: true
            show_signature_annotations: true
            heading_level: 2
```

### 图表支持

```yaml
plugins:
  - mermaid:
      version: 10.6.1
      startOnLoad: true
      theme: default
      securityLevel: loose
      flowchart:
        useMaxWidth: true
        htmlLabels: true
        curve: basis
```

## 部署插件

### GitHub Pages

```yaml
plugins:
  - gh-deploy:
      repo: 'your-username/your-repo'
      branch: 'gh-pages'
      force: false
      delete_branch: false
```

### Netlify

```yaml
plugins:
  - netlify:
      config_file: netlify.toml
      context: production
```

## 性能优化插件

### 缓存

```yaml
plugins:
  - cache:
      dir: .cache
      cache_file: mkdocs.cache
      cache_expiry: 3600
```

### 资源优化

```yaml
plugins:
  - optimize:
      enabled: true
      css_minifier: true
      js_minifier: true
      image_optimizer: true
      webp_conversion: true
```

## 插件配置最佳实践

### 1. 按需加载

```yaml
# 只在生产环境启用某些插件
plugins:
  - search

  # 生产环境专用插件
  - minify:
      enabled: !!python/name:os.getenv('ENVIRONMENT') == 'production'
```

### 2. 插件顺序

```yaml
# 插件按特定顺序执行
plugins:
  - meta           # 先处理元数据
  - toc            # 再生成目录
  - minify         # 最后压缩
```

### 3. 错误处理

```yaml
plugins:
  - git-revision-date-localized:
      enabled: true
      on_error: continue  # 或 skip, fail
```

## 自定义插件开发

### 基础插件结构

```python
# docs/plugins/my_plugin.py
from mkdocs.plugins import BasePlugin

class MyPlugin(BasePlugin):
    config_scheme = (
        ('option1', config.Type(str, default='')),
        ('option2', config.Type(bool, default=False)),
    )

    def on_page_content(self, content, **kwargs):
        # 处理页面内容
        return content
```

### 注册插件

```yaml
plugins:
  - my_plugin:
      option1: 'value'
      option2: true
```

---

**下一步**: [Markdown扩展](writing/extensions.md)