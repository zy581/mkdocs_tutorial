# 本地预览和开发

## 启动开发服务器

MkDocs内置了一个开发服务器，支持实时重新加载：

```bash
mkdocs serve
```

这将启动一个本地服务器，默认地址为`http://localhost:8000`。

## 常用命令选项

```bash
# 指定端口
mkdocs serve --dev-addr 8080:8000

# 启用HTTPS
mkdocs serve --dev-addr 8080:8000 --use-commit-on-save

# 自动重新加载
mkdocs serve --livereload

# 不使用 livereload
mkdocs serve --no-livereload
```

## 开发工作流程

### 1. 启动服务器
```bash
mkdocs serve
```

### 2. 编辑文档
在编辑器中修改Markdown文件，浏览器会自动刷新。

### 3. 查看变更
所有变更会立即在浏览器中反映出来。

### 4. 停止服务器
按`Ctrl+C`停止开发服务器。

## 配置文件热更新

修改`mkdocs.yml`配置文件后，需要重启服务器才能生效：

```bash
# 停止服务器
Ctrl+C

# 重新启动
mkdocs serve
```

## 调试技巧

### 查看日志输出
```bash
mkdocs serve --verbose
```

### 检查配置
```bash
mkdocs build --dry-run
```

### 验证链接
```bash
mkdocs build
mkdocs gh-deploy --force
```

## 开发服务器限制

1. **仅限本地访问**：默认只监听`127.0.0.1`
2. **不适用于生产**：内置服务器性能有限
3. **配置变更需要重启**：修改`mkdocs.yml`需要手动重启

## 多项目开发

如果你有多个MkDocs项目，可以为每个项目使用不同的端口：

```bash
# 项目1
mkdocs serve --dev-addr 127.0.0.1:8000

# 项目2
mkdocs serve --dev-addr 127.0.0.1:8001
```

## 集成开发环境配置

### VS Code集成
在VS Code中，你可以创建一个任务来启动开发服务器：

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Start MkDocs Server",
      "type": "shell",
      "command": "mkdocs",
      "args": ["serve"],
      "isBackground": true
    }
  ]
}
```

### PyCharm集成
在PyCharm中，创建一个新的Python运行配置：
- Script path: `mkdocs`
- Parameters: `serve`

---

**下一步**: [基本配置](configuration/basic.md)