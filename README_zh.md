# Selenium MCP 服务器

一个基于 Model Context Protocol (MCP) 的服务器，提供 Selenium 浏览器自动化功能。通过标准化的 MCP 接口，实现自动化浏览器测试和网页抓取功能。

```bash
npx @thinkai/selenium-mcp-server
```

## 功能特点

- 🌐 基于 Selenium WebDriver 的浏览器自动化
- 🔄 支持 Chrome、Firefox 和 Edge 浏览器
- 📦 会话管理和浏览器池
- 📝 完善的错误处理和日志记录
- 📸 截图功能
- 🔧 JavaScript 执行支持
- 🐳 Docker 容器化支持

## 可用工具

本 MCP 服务器通过自然语言交互提供以下浏览器自动化工具：

### 浏览器导航
- **navigate**: 在浏览器中打开网页（支持 Chrome、Firefox 或 Edge）
  - 示例："在 Chrome 中打开 example.com"

### 页面交互
- **click**: 点击页面元素
  - 示例："点击登录按钮"
  - 示例："点击 ID 为 'submit' 的元素"

- **type**: 在表单字段中输入文本
  - 示例："在搜索框中输入 'hello'"
  - 示例："在用户名字段中填写 'admin'"

- **wait**: 等待元素出现
  - 示例："等待加载动画消失"
  - 示例："等待搜索结果加载完成"

### 页面分析
- **get_content**: 获取页面信息
  - 示例："获取页面标题"
  - 示例："获取当前 URL"
  - 示例："获取页面源代码"

### 视觉验证
- **screenshot**: 捕获当前页面状态
  - 示例："截取页面截图"

### 高级功能
- **execute_script**: 执行 JavaScript 代码（用于高级自动化）
  - 注意：这通常由 AI 助手根据任务需求自动处理

AI 助手会自动管理浏览器会话和技术细节，让用户可以专注于用自然语言描述自动化目标。

## 使用示例

```
用户："能帮我测试一下 example.com 的登录表单吗？"

AI：我来帮你测试登录表单：
1. 打开网站
2. 填写表单
3. 提交并验证

[AI 自动通过自然语言处理浏览器自动化]
```


## 工具集

| 工具 | 描述 | 输入参数 |
| --- | --- | --- |
| navigate | 在浏览器中打开网页 | url*<br>string<br>要访问的 URL<br>browserType<br>string<br>'chrome' \| 'firefox' \| 'edge'<br>sessionId<br>string<br>浏览器会话 ID |
| click | 点击页面元素 | selector*<br>object<br>元素选择器 {type, value}<br>options<br>object<br>{waitForElement, timeout}<br>sessionId*<br>string<br>浏览器会话 ID |
| type | 在表单字段中输入文本 | selector*<br>object<br>元素选择器 {type, value}<br>text*<br>string<br>要输入的文本<br>options<br>object<br>{clearFirst, submitAfter}<br>sessionId*<br>string<br>浏览器会话 ID |
| wait | 等待元素出现 | selector*<br>object<br>元素选择器 {type, value}<br>options<br>object<br>{timeout, pollInterval}<br>sessionId*<br>string<br>浏览器会话 ID |
| screenshot | 捕获当前页面状态 | sessionId*<br>string<br>浏览器会话 ID |
| get_content | 获取页面信息 | type*<br>string<br>'url' \| 'title' \| 'source'<br>sessionId*<br>string<br>浏览器会话 ID |
| execute_script | 执行 JavaScript 代码 | script*<br>string<br>要执行的 JavaScript 代码<br>args<br>array<br>传递的参数<br>sessionId*<br>string<br>浏览器会话 ID |

## 安装方式

### 使用 NPX

无需安装，直接运行：

```bash
npx @thinkai/selenium-mcp-server
```

### 使用 Docker

1. 构建镜像：
```bash
docker build -t selenium-mcp-server .
```

2. 运行容器：
```bash
docker run -d \
  --name selenium-mcp \
  -p 3000:3000 \
  selenium-mcp-server
```

3. 自定义配置（可选）：
```bash
docker run -d \
  --name selenium-mcp \
  -p 3000:3000 \
  -e PORT=3000 \
  -e LOG_LEVEL=info \
  -e MAX_SESSIONS=5 \
  selenium-mcp-server
```

或使用我们的预构建镜像：
```bash
docker run -d \
  --name selenium-mcp \
  -p 3000:3000 \
  thinkai/selenium-mcp-server
```

Docker 镜像包含：
- Node.js 18 LTS
- Chrome 和 Firefox 浏览器
- 所有必要的浏览器依赖
- 预配置环境

## 参数配置

### Docker 配置

| 参数 | 描述 |
| --- | --- |
| PORT | 服务器端口（默认：3000） |
| LOG_LEVEL | Winston 日志级别 |
| MAX_SESSIONS | 最大并发浏览器会话数 |
| TIMEOUT | 默认操作超时时间（毫秒） |
| RETRIES | 操作重试次数 |

### NPX 配置

| 参数 | 描述 |
| --- | --- |
| PORT | 服务器端口（默认：3000） |
| LOG_LEVEL | Winston 日志级别 |
| MAX_SESSIONS | 最大并发浏览器会话数 |
| TIMEOUT | 默认操作超时时间（毫秒） |
| RETRIES | 操作重试次数 |


## 配置说明

> Claude Desktop ｜ Vscode Cline

在 `config.json` 中添加：

```json
{
  "mcpServers": {
    "github.com/thinkai/selenium-mcp-server": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "PORT=3000",
        "-e",
        "MAX_SESSIONS=5",
        "thinkai/selenium-mcp-server"
      ]
    }
  }
}
```

### NPX 配置

```json
{
  "mcpServers": {
    "github.com/thinkai/selenium-mcp-server": {
      "command": "npx",
      "args": [
        "-y",
        "@thinkai/selenium-mcp-server"
      ]
    }
  }
}
```

## 构建

Docker 构建：

```bash
docker build -t thinkai/selenium-mcp-server:latest .
```

## 开发

1. 安装依赖：
```bash
pnpm install
```

2. 开发模式运行：
```bash
pnpm dev
```

3. 运行测试：
```bash
pnpm test
```

## 许可证

本 MCP 服务器基于 MIT 许可证。这意味着您可以自由使用、修改和分发本软件，但需要遵守 MIT 许可证的条款和条件。详细信息请参见项目仓库中的 LICENSE 文件。
