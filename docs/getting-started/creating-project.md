# 创建你的第一个MkDocs项目

## 基本项目结构

使用MkDocs创建新项目非常简单：

```bash
mkdocs new my-project
cd my-project
```

这会生成以下目录结构：

```
my-project/
├── mkdocs.yml    # 配置文件
└── docs/
    └── index.md  # 首页内容
```

## 配置文件详解

打开`mkdocs.yml`文件，这是项目的核心配置文件：

```yaml
site_name: My Project  # 网站名称
docs_dir: docs         # 文档目录
site_dir: site         # 构建输出目录
```

## 添加Material主题

修改配置文件以使用Material主题：

```yaml
theme:
  name: material
  palette:
    - scheme: default
      primary: 'blue'
      accent: 'blue'
```

## 添加导航结构

扩展导航结构以包含多个页面：

```yaml
nav:
  - 首页: index.md
  - 关于: about.md
  - 指南:
    - 入门: guide/getting-started.md
    - 进阶: guide/advanced.md
```

## 创建额外页面

手动创建导航中引用的页面：

```bash
# 创建about页面
echo "# 关于" > docs/about.md

# 创建指南子目录
mkdir -p docs/guide

# 创建指南页面
echo "# 入门指南" > docs/guide/getting-started.md
echo "# 进阶指南" > docs/guide/advanced.md
```

## 项目组织最佳实践

### 1. 目录结构
```
docs/
├── index.md
├── about.md
├── guide/
│   ├── index.md
│   ├── getting-started.md
│   └── advanced.md
├── api/
│   └── index.md
└── assets/
    ├── css/
    ├── images/
    └── js/
```

### 2. 文件命名规范
- 使用小写字母
- 用连字符分隔单词
- 保持简洁但有意义

### 3. 配置管理
- 将大型配置拆分为多个文件
- 使用环境变量管理敏感信息
- 保持配置版本控制

## 验证项目结构

运行以下命令验证项目结构是否正确：

```bash
mkdocs serve
```

访问`http://localhost:8000`查看效果。

---

**下一步**: [本地预览和开发](serving.md)