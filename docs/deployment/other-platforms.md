# 其他部署平台

除了GitHub Pages，还可以将MkDocs部署到多种其他平台。

## Netlify

### 1. 准备工作

在项目根目录创建`netlify.toml`配置文件：

```toml
[build]
  command = "mkdocs build"
  publish = "site"

[build.environment]
  PYTHON_VERSION = "3.10"

[[plugins]]
  package = "netlify-plugin-cache"
  [plugins.inputs]
    paths = [".cache"]

[[plugins]]
  package = "netlify-plugin-submit-sitemap"
  [plugins.inputs]
    baseUrl = "https://your-site.netlify.app"
```

### 2. 部署步骤

#### 方法1：使用Netlify CLI

```bash
# 安装Netlify CLI
npm install -g netlify-cli

# 登录Netlify
netlify login

# 初始化项目
netlify init

# 部署
netlify deploy --prod
```

#### 方法2：使用GitHub集成

1. 登录Netlify
2. 点击 **New site from Git**
3. 选择GitHub仓库
4. 配置构建选项：
   - Build command: `mkdocs build`
   - Publish directory: `site`
5. 点击 **Deploy site**

### 3. 配置环境变量

在Netlify控制面板中：
1. 进入 **Site settings** > **Build & deploy** > **Environment**
2. 添加环境变量：
   - `PYTHON_VERSION`: `3.10`
   - `NODE_VERSION`: `18`

### 4. 自定义域名

1. 购买域名
2. 在Netlify中添加域名
3. 配置DNS记录
4. 启用HTTPS

## Vercel

### 1. 准备工作

创建`vercel.json`配置：

```json
{
  "buildCommand": "mkdocs build",
  "outputDirectory": "site",
  "devCommand": "mkdocs serve",
  "installCommand": "pip install mkdocs mkdocs-material"
}
```

### 2. 部署步骤

#### 方法1：使用Vercel CLI

```bash
# 安装Vercel CLI
npm install -g vercel

# 部署
vercel
```

#### 方法2：使用GitHub集成

1. 登录Vercel
2. 导入GitHub仓库
3. 配置项目设置
4. 部署

## GitLab Pages

### 1. 配置`.gitlab-ci.yml`

```yaml
image: python:3.10

pages:
  stage: deploy
  script:
    - pip install mkdocs mkdocs-material mkdocs-minify-plugin
    - mkdocs build
  artifacts:
    paths:
      - public
  only:
    - main
```

### 2. 部署

```bash
git add .gitlab-ci.yml
git commit -m "Add GitLab CI configuration"
git push origin main
```

## Docker部署

### 1. 创建Dockerfile

```dockerfile
FROM python:3.10-slim

WORKDIR /app

# 安装系统依赖
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# 安装MkDocs
RUN pip install --no-cache-dir \
    mkdocs \
    mkdocs-material \
    mkdocs-minify-plugin \
    mkdocs-git-revision-date-localized-plugin

# 复制项目文件
COPY . .

# 暴露端口
EXPOSE 8000

# 启动命令
CMD ["mkdocs", "serve", "--dev-addr", "0.0.0.0:8000"]
```

### 2. 构建和运行

```bash
# 构建镜像
docker build -t mkdocs-tutorial .

# 运行容器
docker run -p 8000:8000 mkdocs-tutorial

# 后台运行
docker run -d -p 8000:8000 --name mkdocs-server mkdocs-tutorial
```

### 3. Docker Compose

创建`docker-compose.yml`：

```yaml
version: '3.8'

services:
  mkdocs:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - ./docs:/app/docs
      - ./mkdocs.yml:/app/mkdocs.yml
    restart: unless-stopped
```

运行：
```bash
docker-compose up -d
```

## AWS S3 + CloudFront

### 1. 配置AWS CLI

```bash
aws configure
```

### 2. 创建S3存储桶

```bash
aws s3 mb s3://your-bucket-name --region us-east-1
```

### 3. 配置静态网站

```bash
aws s3 website s3://your-bucket-name/ --index-document index.html
```

### 4. 部署脚本

创建`deploy.sh`：

```bash
#!/bin/bash

# 构建文档
mkdocs build

# 同步到S3
aws s3 sync site/ s3://your-bucket-name/ --delete

# 设置缓存策略
aws s3 cp s3://your-bucket-name/ s3://your-bucket-name/ --recursive \
  --cache-control "max-age=300"

# 使文件公开
aws s3api put-object-acl --bucket your-bucket-name --key index.html --acl public-read
```

### 5. 配置CloudFront

1. 创建CloudFront分发
2. 选择S3存储桶作为源
3. 配置缓存行为
4. 启用HTTPS

## Azure Static Web Apps

### 1. 创建Azure资源

```bash
# 安装Azure CLI
az login

# 创建资源组
az group create --name rg-mkdocs --location eastus

# 创建静态Web应用
az staticwebapp create \
    --name mkdocs-tutorial \
    --resource-group rg-mkdocs \
    --source https://github.com/your-username/mkdocs-tutorial \
    --location eastus \
    --branch main \
    --app-location "/" \
    --output-location "site" \
    --build-action "MkDocs Build"
```

### 2. 配置构建

在Azure门户中：
1. 进入 **Configuration** > **Application settings**
2. 添加构建命令：`mkdocs build`

## 自建服务器

### 1. Nginx配置

```nginx
server {
    listen 80;
    server_name your-domain.com;

    root /path/to/mkdocs/site;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # 缓存静态资源
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # Gzip压缩
    gzip on;
    gzip_vary on;
    gzip_types
        text/plain
        text/css
        text/xml
        text/javascript
        application/javascript
        application/xml+rss
        application/json;
}
```

### 2. Apache配置

```apache
<VirtualHost *:80>
    ServerName your-domain.com
    DocumentRoot /path/to/mkdocs/site

    <Directory /path/to/mkdocs/site>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    # 缓存配置
    <FilesMatch "\.(js|css|png|jpg|jpeg|gif|ico|svg)$">
        Header set Cache-Control "max-age=31536000, public"
    </FilesMatch>

    # Gzip压缩
    <IfModule mod_deflate.c>
        AddOutputFilterByType DEFLATE text/plain text/css text/xml text/javascript
        AddOutputFilterByType DEFLATE application/javascript application/xml+rss application/json
    </IfModule>
</VirtualHost>
```

## 部署比较

| 平台 | 优点 | 缺点 | 适合场景 |
|------|------|------|----------|
| GitHub Pages | 免费、集成Git、自动部署 | 构建时间限制、功能限制 | 个人项目、开源项目 |
| Netlify | 免费额度、全球CDN、预览部署 | 构建时间限制 | 个人项目、小型团队 |
| Vercel | 快速、现代、预览部署 | 构建时间限制 | 前端项目、个人站点 |
| GitLab Pages | 集成GitLab、免费 | 需要GitLab账户 | GitLab用户 |
| AWS S3 | 可扩展、低成本、高度可控 | 配置复杂、费用可能较高 | 企业级应用 |
| Docker | 一致环境、可移植 | 需要容器知识 | 开发团队、微服务 |

## 多平台部署策略

### 1. 主备部署

```yaml
# GitHub Actions工作流
name: Multi-platform Deploy

on:
  push:
    branches:
      - main

jobs:
  deploy-github:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to GitHub Pages
        run: mkdocs gh-deploy --force

  deploy-netlify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Netlify
        run: |
          npm install -g netlify-cli
          netlify deploy --prod --site-id=${{ secrets.NETLIFY_SITE_ID }}
```

### 2. 环境特定配置

```yaml
# 根据分支部署到不同环境
- name: Deploy based on branch
  if: github.ref == 'refs/heads/main'
  run: mkdocs gh-deploy --force

- name: Deploy preview to Netlify
  if: github.event_name == 'pull_request'
  run: netlify deploy --branch=${{ github.head_ref }}
```

---

**下一步**: [自定义CSS](advanced/custom-css.md)