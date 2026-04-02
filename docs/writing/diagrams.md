# 图表和图示功能

MkDocs Material通过Mermaid.js支持创建专业的图表和图示，让文档更加直观易懂。

## ✨ 核心功能

### 1. 流程图
创建清晰的工作流程和数据流程图

### 2. 序列图
展示系统间的交互流程和调用关系

### 3. 甘特图
项目计划和进度管理的可视化

### 4. 其他图表
支持类图、状态图、饼图等多种图表类型

---

## 🚀 快速开始

### Mermaid配置

在`mkdocs.yml`中启用Mermaid支持：

```yaml
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format

plugins:
  - mermaid:
      version: 10.6.1
      startOnLoad: true
      theme: default
```

---

## 📊 流程图

### 基本流程图

展示工作流程或数据处理流程：

```mermaid
graph TD
    A[开始] --> B{判断}
    B -->|是| C[执行1]
    B -->|否| D[执行2]
    C --> E[结束]
    D --> E
```

### 横向流程图

适合展示线性流程：

```mermaid
graph LR
    A[开始] --> B[步骤1]
    B --> C[步骤2]
    C --> D[结束]
```

### 复杂流程图

展示包含条件判断的完整流程：

```mermaid
graph TD
    A[用户登录] --> B{验证}
    B -->|成功| C[加载主页]
    B -->|失败| D[显示错误]
    D --> E[重新输入]
    E --> B
    C --> F[获取用户数据]
    F --> G[显示内容]
```

---

## 🔄 序列图

### 基本序列图

展示系统间的交互流程：

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Server

    User->>Browser: 输入URL
    Browser->>Server: 发送请求
    Server-->>Browser: 返回HTML
    Browser-->>User: 显示页面
```

### 复杂序列图

展示包含条件判断的业务流程：

```mermaid
sequenceDiagram
    participant User
    participant UI as UI层
    participant API as API层
    participant DB as 数据库

    User->>UI: 点击登录
    UI->>API: POST /login
    API->>DB: 查询用户
    DB-->>API: 返回结果
    alt 成功
        API-->>UI: 200 OK + token
        UI-->>User: 跳转到主页
    else 失败
        API-->>UI: 401 Unauthorized
        UI-->>User: 显示错误信息
    end
```

---

## 📅 甘特图

### 项目计划

展示项目的时间安排和任务依赖：

```mermaid
gantt
    title 项目开发计划
    dateFormat  YYYY-MM-DD
    section 需求分析
    需求收集       :a1, 2024-01-01, 10d
    需求分析       :a2, after a1, 5d
    section 开发阶段
    前端开发       :b1, 2024-01-15, 20d
    后端开发       :b2, 2024-01-15, 25d
    section 测试阶段
    单元测试       :c1, after b1, 10d
    集成测试       :c2, after b2, 15d
    section 部署上线
    部署发布       :d1, after c1 c2, 5d
```

### 里程碑计划

展示项目关键节点和时间安排：

```mermaid
gantt
    title 项目里程碑计划
    dateFormat  YYYY-MM-DD
    section 第一阶段
    需求完成       :crit, done, m1, 2024-01-15, 1d
    设计完成       :crit, active, m2, after m1, 1d
    section 第二阶段
    开发完成       :active, m3, 2024-02-20, 1d
    测试完成       :m4, after m3, 1d
    section 第三阶段
    上线发布       :crit, m5, after m4, 1d
```

---

## 🎯 饼图

### 数据分布

展示数据的占比情况：

```mermaid
pie title 编程语言使用率
    "JavaScript" : 35
    "Python" : 25
    "Java" : 20
    "C#" : 10
    "其他" : 10
```

---

## 🏗️ 类图

### 面向对象设计

展示类之间的关系：

```mermaid
classDiagram
    class Animal {
        +name: string
        +age: int
        +eat()
        +sleep()
    }

    class Dog {
        +breed: string
        +bark()
    }

    class Cat {
        +color: string
        +meow()
    }

    Animal <|-- Dog
    Animal <|-- Cat
```

---

## 🔄 状态图

### 状态转换

展示对象的状态变化：

```mermaid
stateDiagram-v2
    [*] --> 待机
    待机 --> 运行: 启动
    运行 --> 暂停: 暂停
    暂停 --> 运行: 恢复
    运行 --> 停止: 停止
    停止 --> [*]

    state 运行 {
        [*] --> 初始化
        初始化 --> 处理中
        处理中 --> 完成
        完成 --> [*]
    }
```

---

## 🎨 图表样式

### 自定义样式

创建自定义CSS文件：

```css
/* docs/assets/css/custom.css */
.mermaid {
    background-color: #f8f9fa;
    border: 1px solid #dee2e6;
    border-radius: 8px;
    padding: 1rem;
    margin: 1rem 0;
}

.mermaid .node rect,
.mermaid .node circle,
.mermaid .node ellipse {
    fill: #e3f2fd !important;
    stroke: #1976d2 !important;
}

.mermaid .edgePath path {
    stroke: #424242 !important;
}
```

### 响应式设计

移动端适配：

```css
@media (max-width: 768px) {
    .mermaid {
        font-size: 12px;
        overflow-x: auto;
    }
}
```

---

## 💡 使用技巧

### 1. 保持简洁

**✅ 推荐：**
```mermaid
graph TD
    A[用户] --> B[系统]
    B --> C[数据库]
```

**❌ 不推荐：**
过于复杂的图表，难以理解

### 2. 使用合适的布局

```mermaid
graph TD
    A[开始] --> B[步骤1]
    B --> C[步骤2]
    C --> D[结束]
```

根据内容选择合适的布局：TD（从上到下）、LR（从左到右）

### 3. 添加描述

```mermaid
graph TD
    A[用户登录] --> B{验证成功?}
    B -->|是| C[进入主页]
    B -->|否| D[显示错误]
```

图1：用户登录流程图

---

## 📋 实际应用场景

### 1. 系统设计文档

```mermaid
graph TD
    A[用户请求] --> B[负载均衡]
    B --> C[Web服务器]
    C --> D[应用服务器]
    D --> E[数据库]
    D --> F[缓存]
```

### 2. API文档

```mermaid
sequenceDiagram
    participant Client
    participant API
    participant Database

    Client->>API: 请求数据
    API->>Database: 查询
    Database-->>API: 返回结果
    API-->>Client: 响应数据
```

### 3. 项目计划

```mermaid
gantt
    title 开发计划
    dateFormat  YYYY-MM-DD
    section 前端
    UI设计 :a1, 2024-01-01, 15d
    前端开发 :a2, after a1, 20d
    section 后端
    数据库设计 :b1, 2024-01-01, 10d
    后端开发 :b2, after b1, 25d
```

---

## 🎯 教学建议

1. **循序渐进**：从简单流程图开始，逐步介绍复杂图表
2. **结合实际**：使用实际项目中的图表案例
3. **动手实践**：让学生创建自己的图表
4. **对比学习**：比较不同图表类型的适用场景

---

**图表功能让复杂信息变得更加直观易懂！** 📊

**下一步**: [GitHub Pages部署](deployment/github-pages.md)