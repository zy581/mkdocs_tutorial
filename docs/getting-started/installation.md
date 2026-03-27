# 安装MkDocs

在本教程中，我们将学习如何安装和配置MkDocs以及Material主题。

## 系统要求

- Python 3.6+
- pip (Python包管理器)

## 安装Python和pip

首先确保你的系统已经安装了Python 3.6或更高版本：

```bash
python --version
pip --version
```

如果没有安装，请从[Python官网](https://www.python.org/downloads/)下载并安装。

## 安装MkDocs

使用pip安装MkDocs：

```bash
pip install mkdocs
```

验证安装是否成功：

```bash
mkdocs --version
```

## 安装Material主题

安装Material for MkDocs主题：

```bash
pip install mkdocs-material
```

## 推荐插件

为了获得完整功能，建议安装以下插件：

```bash
pip install mkdocs-minify-plugin mkdocs-git-revision-date-localized-plugin
```

## 开发服务器要求

MkDocs内置开发服务器需要`livereload`库：

```bash
pip install livereload
```

## 验证安装

创建一个测试项目来验证所有组件是否正常工作：

```bash
mkdocs new test-project
cd test-project
mkdocs serve
```

如果一切正常，你可以在浏览器中访问`http://localhost:8000`查看测试站点。

---

**下一步**: [创建你的第一个项目](creating-project.md)