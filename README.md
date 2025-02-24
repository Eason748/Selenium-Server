# Selenium MCP Server

A Model Context Protocol (MCP) server that provides Selenium-based browser automation capabilities. This server enables automated browser testing and web scraping functionality through a standardized MCP interface.

## Features

- Browser automation with Selenium WebDriver
- Support for Chrome, Firefox, and Edge browsers
- Session management and browser pooling
- Comprehensive error handling and logging
- Screenshot capture capabilities
- JavaScript execution support

## Tools

### navigate
Navigate to a URL in a browser session.
```typescript
{
  url: string;          // URL to navigate to
  browserType?: string; // 'chrome' | 'firefox' | 'edge'
}
```

### click
Click on an element in the page.
```typescript
{
  selector: {
    type: string;   // 'css' | 'xpath' | 'id' | 'name' | 'class'
    value: string;  // Selector value
  };
  options?: {
    waitForElement?: boolean; // Wait for element to be present
    timeout?: number;         // Timeout in milliseconds
  };
  sessionId: string;
}
```

### type
Type text into an element.
```typescript
{
  selector: {
    type: string;   // 'css' | 'xpath' | 'id' | 'name' | 'class'
    value: string;  // Selector value
  };
  text: string;     // Text to type
  options?: {
    clearFirst?: boolean;  // Clear field before typing
    submitAfter?: boolean; // Submit form after typing
  };
  sessionId: string;
}
```

### wait
Wait for an element to be visible.
```typescript
{
  selector: {
    type: string;   // 'css' | 'xpath' | 'id' | 'name' | 'class'
    value: string;  // Selector value
  };
  options?: {
    timeout?: number;      // Timeout in milliseconds
    pollInterval?: number; // Poll interval in milliseconds
  };
  sessionId: string;
}
```

### execute_script
Execute JavaScript in the browser context.
```typescript
{
  script: string;   // JavaScript code to execute
  args?: any[];     // Arguments to pass to the script
  sessionId: string;
}
```

### screenshot
Take a screenshot of the current page.
```typescript
{
  sessionId: string;
}
```

### get_content
Get page content (URL, title, or source).
```typescript
{
  type: string;     // 'url' | 'title' | 'source'
  sessionId: string;
}
```

## 快速开始

### 通过 npx 使用

无需安装，直接通过 npx 运行：

```bash
npx @thinkai/selenium-mcp-server
```

### MCP 客户端配置

#### Claude Desktop

在 Claude Desktop 配置文件中添加以下配置（通常位于 `~/Library/Application Support/Claude/claude_desktop_config.json`）：

```json
{
  "mcpServers": {
    "selenium": {
      "command": "npx",
      "args": [
        "-y",
        "@thinkai/selenium-mcp-server"
      ],
      "disabled": false,
      "autoApprove": [
        "navigate",
        "click",
        "type",
        "wait",
        "screenshot",
        "get_content"
      ]
    }
  }
}
```

#### Cline

在 Cline 配置文件中添加以下配置（通常位于 `~/Library/Application Support/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json`）：

```json
{
  "mcpServers": {
    "selenium": {
      "command": "npx",
      "args": [
        "-y",
        "@thinkai/selenium-mcp-server"
      ],
      "disabled": false,
      "autoApprove": [
        "navigate",
        "click",
        "type",
        "wait",
        "screenshot",
        "get_content"
      ]
    }
  }
}
```

### 本地开发

1. 安装依赖:
```bash
pnpm install
```

2. 构建项目:
```bash
pnpm build
```

## Configuration

The server can be configured through environment variables or a configuration file:

```typescript
interface Config {
  port?: number;                 // Server port (default: 3000)
  logLevel?: string;            // Winston log level
  maxSessions?: number;         // Max concurrent browser sessions
  timeout?: number;             // Default operation timeout (ms)
  retries?: number;             // Operation retry count
  browsers?: {                  // Browser-specific configs
    chrome?: BrowserConfig;
    firefox?: BrowserConfig;
    edge?: BrowserConfig;
  };
}

interface BrowserConfig {
  binary?: string;              // Browser binary path
  args?: string[];             // Browser launch arguments
  defaultCapabilities?: object; // Default capabilities
}
```

## Usage

1. Start the server:
```bash
pnpm start
```

2. Use with an MCP client:
```typescript
const result = await client.useTool('navigate', {
  url: 'https://example.com',
  browserType: 'chrome'
});

const sessionId = JSON.parse(result.content[0].text).sessionId;

await client.useTool('click', {
  selector: {
    type: 'css',
    value: '#submit-button'
  },
  sessionId
});
```

## Development

1. Run in development mode:
```bash
pnpm dev
```

2. Run tests:
```bash
pnpm test
```

3. Lint code:
```bash
pnpm lint
```

## License

MIT
