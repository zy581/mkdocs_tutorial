# GitHub Pages部署

GitHub Pages是GitHub提供的免费静态网站托管服务，非常适合托管MkDocs文档。

## 准备工作

### 1. 创建GitHub仓库

首先，在GitHub上创建一个新的仓库：

```bash
# 使用GitHub CLI
gh repo create mkdocs-tutorial --public --source=. --remote=origin

# 或者手动创建后添加远程仓库
git remote add origin https://github.com/your-username/mkdocs-tutorial.git
```

### 2. 配置Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 3. 更新配置文件

在`mkdocs.yml`中添加仓库信息：

```yaml
site_name: MkDocs Material 教程
site_url: https://your-username.github.io/mkdocs-tutorial/
repo_name: your-username/mkdocs-tutorial
repo_url: https://github.com/your-username/mkdocs-tutorial
edit_uri: edit/main/docs/
```

## 手动部署

### 1. 构建文档

```bash
mkdocs build
```

### 2. 部署到GitHub Pages

```bash
mkdocs gh-deploy
```

这会自动：
- 构建文档
- 创建`gh-pages`分支
- 推送到GitHub

### 3. 验证部署

部署完成后，访问：
`https://your-username.github.io/mkdocs-tutorial/`

## GitHub Actions自动化部署

### 1. 创建部署工作流

在项目根目录创建`.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Install dependencies
        run: |
          pip install mkdocs
          pip install mkdocs-material
          pip install mkdocs-minify-plugin
          pip install mkdocs-git-revision-date-localized-plugin

      - name: Deploy to GitHub Pages
        run: mkdocs gh-deploy --force
```

### 2. 配置GitHub Pages

在GitHub仓库设置中：
1. 进入 **Settings** > **Pages**
2. 选择 **Source**: `Deploy from a branch`
3. 选择 **Branch**: `gh-pages` / `(root)`
4. 保存设置

### 3. 触发部署

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

## 自定义域名

### 1. 购买域名

在域名注册商购买域名，如`example.com`。

### 2. 配置DNS

添加CNAME记录：
```
Type: CNAME
Name: docs
Value: your-username.github.io
TTL: 3600
```

### 3. 创建CNAME文件

在`docs/`目录创建`CNAME`文件：

```bash
echo "docs.example.com" > docs/CNAME
```

### 4. 更新配置

```yaml
site_url: https://docs.example.com
```

### 5. 配置GitHub Pages

在GitHub仓库设置中：
1. 进入 **Settings** > **Pages**
2. 在 **Custom domain** 中输入`docs.example.com`
3. 勾选 **Enforce HTTPS**

## 部署配置选项

### 强制部署

```bash
mkdocs gh-deploy --force
```

### 不使用gh-pages分支

```bash
mkdocs gh-deploy --remote-branch main
```

### 指定远程仓库

```bash
mkdocs gh-deploy --remote-name upstream
```

### 本地构建后部署

```bash
mkdocs build
mkdocs gh-deploy --clean
```

## 高级配置

### 使用Personal Access Token

```yaml
# .github/workflows/deploy.yml
env:
  GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  # 或自定义Token
  # GH_TOKEN: ${{ secrets.MY_GH_TOKEN }}
```

### 自定义部署脚本

```yaml
- name: Custom deploy
  run: |
    mkdocs build
    echo "Custom deployment script"
    # 添加额外的部署逻辑
```

### 多环境部署

```yaml
# 开发环境部署到dev分支
- name: Deploy dev
  if: github.ref == 'refs/heads/develop'
  run: mkdocs gh-deploy --remote-branch gh-pages-dev

# 生产环境部署到main分支
- name: Deploy prod
  if: github.ref == 'refs/heads/main'
  run: mkdocs gh-deploy
```

## 常见问题

### 1. 部署后页面空白

**原因**: 可能缺少依赖
**解决**:
```yaml
# 确保在工作流中安装所有依赖
- name: Install dependencies
  run: |
    pip install mkdocs
    pip install mkdocs-material
    pip install mkdocs-minify-plugin
    pip install mkdocs-git-revision-date-localized-plugin
```

### 2. 自定义域名不生效

**原因**: DNS配置或CNAME文件问题
**解决**:
1. 检查DNS解析是否正确
2. 确保CNAME文件在`docs/`目录
3. 等待DNS传播（可能需要几小时）

### 3. HTTPS不生效

**原因**: 可能需要等待GitHub配置
**解决**:
1. 等待几分钟
2. 检查GitHub Pages设置中的HTTPS选项
3. 重新保存设置

### 4. 404错误

**原因**: 路径配置问题
**解决**:
1. 检查`site_url`配置
2. 确保使用正确的仓库名称
3. 验证base URL设置

## 最佳实践

### 1. 使用版本控制

```bash
# 忽略site目录
echo "site/" >> .gitignore

# 确保包含所有必要文件
git add mkdocs.yml docs/ .github/
git commit -m "Update documentation"
git push
```

### 2. 定期更新依赖

```bash
# 更新MkDocs和相关插件
pip install --upgrade mkdocs mkdocs-material mkdocs-minify-plugin
```

### 3. 本地测试

```bash
# 在部署前本地测试
mkdocs serve
# 访问 http://localhost:8000
```

### 4. 自动化测试

```yaml
# 添加测试步骤
- name: Test build
  run: mkdocs build --dry-run
```

### 5. 备份配置

```bash
# 备份重要配置文件
cp mkdocs.yml mkdocs.yml.backup
```

## 监控和统计

### 启用Google Analytics

```yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX
```

### GitHub Pages统计

在GitHub仓库中查看访问统计：
1. 进入 **Insights** > **Traffic**
2. 查看访客数据
3. 分析热门页面

---

**下一步**: [其他部署平台](other-platforms.md)