# 代码展示功能

MkDocs Material提供了专业的代码展示功能，让技术文档更加清晰易读。

## ✨ 核心功能

### 1. 代码高亮
自动识别和突出显示多种编程语言的语法

### 2. 行号显示
显示代码行号，便于代码审查和教学演示

### 3. 复制功能
一键复制代码到剪贴板

### 4. 代码标注
在代码中添加注释，解释关键代码段

---

## 🚀 快速开始

### 基本代码块

在Markdown中使用三个反引号创建代码块，系统会自动识别并高亮显示：

```python
def hello():
    print("Hello, World!")
```

### 指定语言

在反引号后指定编程语言，获得更准确的语法高亮：

```javascript
function add(a, b) {
    return a + b;
}
```

---

## 📚 支持的语言

Material for MkDocs支持所有主流编程语言：

### Python 示例
```python
def calculate_sum(numbers):
    total = 0
    for num in numbers:
        total += num
    return total
```

### JavaScript 示例
```javascript
function calculateSum(numbers) {
    return numbers.reduce((a, b) => a + b, 0);
}
```

### HTML 示例
```html
<!DOCTYPE html>
<html>
<head>
    <title>示例页面</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```

### CSS 示例
```css
.container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}
```

### YAML 示例
```yaml
site_name: My Site
theme:
  name: material
  primary: 'blue'
```

### JSON 示例
```json
{
  "name": "My Project",
  "version": "1.0.0",
  "author": "Your Name"
}
```

---

## 🎯 高级功能

### 代码标注

在代码行末使用 `# (数字)` 添加标注，然后在下方解释：

```python
def process_data(items):     # (1)
    result = []              # (2)
    for item in items:       # (3)
        result.append(item)  # (4)
    return result           # (5)
```

1. 函数定义，接收列表参数
2. 初始化结果列表
3. 遍历输入列表
4. 添加元素到结果列表
5. 返回处理后的列表

### 行号显示

在配置中启用行号显示功能：

```python
def example():
    x = 1
    y = 2
    z = x + y
    return z
```

### 代码标题

为代码块添加标题，便于理解：

```python title="计算总价"
def calculate_total(price, quantity):
    return price * quantity
```

## 💡 使用技巧

### 1. 选择合适的语言标识符

使用正确的语言标识符确保准确的语法高亮：
- `python` 或 `py` - Python
- `javascript` 或 `js` - JavaScript  
- `html` - HTML
- `css` - CSS
- `yaml` - YAML
- `json` - JSON
- `bash` 或 `sh` - Shell脚本
- `sql` - SQL

### 2. 保持代码简洁

**✅ 推荐：**
```python
# 简洁明了的示例
def add(a, b):
    return a + b
```

**❌ 不推荐：**
```python
# 过于复杂的示例
def complex_calculation(a, b, c, d, e, f, g, h):
    # 大量复杂逻辑...
    pass
```

### 3. 安全最佳实践

**✅ 推荐：**
```python
import os

# 使用环境变量存储敏感信息
api_key = os.getenv('API_KEY')
```

**❌ 不推荐：**
```python
# 永远不要硬编码敏感信息
api_key = "sk-1234567890abcdef"  # 不安全！
```

---

## 🎨 样式配置

### 启用复制按钮

在`mkdocs.yml`中启用代码复制功能：

```yaml
theme:
  features:
    - content.code.copy
```

### 自定义代码样式

创建自定义CSS文件：

```css
/* docs/assets/css/custom.css */
:root {
  --md-code-background-color: #f6f8fa;
  --md-code-font-size: 14px;
  --md-code-line-height: 1.5;
}
```

---

## 📋 实际应用场景

### API文档示例
```python
import requests

def get_user_data(user_id):
    """获取用户数据"""
    response = requests.get(f'/api/users/{user_id}')
    return response.json()
```

### 配置示例
```yaml
database:
  host: localhost
  port: 5432
  name: mydb
  user: admin
```

### 命令行工具
```bash
# 安装依赖
pip install -r requirements.txt

# 启动服务
python app.py --port 8080
```

---

## 🎯 教学建议

1. **循序渐进**：从简单代码块开始，逐步介绍高级功能
2. **实践为主**：让学生动手编写和展示代码
3. **对比学习**：使用代码组功能比较不同语言实现
4. **安全第一**：强调敏感信息处理的重要性

---

**代码展示功能大大提升了技术文档的专业性和可读性！** 🚀

**下一步**: [图表和图示](diagrams.md)