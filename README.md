# Selenium MCP Server

A Model Context Protocol (MCP) server that provides Selenium-based browser automation capabilities. This server enables automated browser testing and web scraping functionality through a standardized MCP interface.

```bash
npx @thinkai/selenium-mcp-server
```

## Features

- 🌐 Browser automation with Selenium WebDriver
- 🔄 Support for Chrome, Firefox, and Edge browsers
- 📦 Session management and browser pooling
- 📝 Comprehensive error handling and logging
- 📸 Screenshot capture capabilities
- 🔧 JavaScript execution support
- 🐳 Docker support for containerized execution

## Available Tools

This MCP server provides several tools for browser automation through natural language interaction:

### Browser Navigation
- **navigate**: Open a webpage in a browser (Chrome, Firefox, or Edge)
  - Example: "Open example.com in Chrome"

### Page Interaction
- **click**: Click on elements in the page
  - Example: "Click the login button"
  - Example: "Click the element with id 'submit'"

- **type**: Enter text into form fields
  - Example: "Type 'hello' into the search box"
  - Example: "Fill the username field with 'admin'"

- **wait**: Wait for elements to appear
  - Example: "Wait for the loading spinner to disappear"
  - Example: "Wait for the search results to load"

### Page Analysis
- **get_content**: Retrieve page information
  - Example: "Get the page title"
  - Example: "Get the current URL"
  - Example: "Get the page source"

### Visual Verification
- **screenshot**: Capture the current page state
  - Example: "Take a screenshot of the page"

### Advanced Features
- **execute_script**: Run JavaScript code (for advanced automation)
  - Note: This is typically handled automatically by the AI assistant based on the task requirements

The AI assistant automatically manages browser sessions and technical details, allowing users to focus on describing their automation goals in natural language.

## Usage Example

```
User: "Can you test the login form on example.com?"

AI: I'll help you test the login form:
1. Navigate to the website
2. Fill in the form
3. Submit and verify

[AI automatically handles browser automation through natural language]
```

## Toolset

| Tool | Description | Inputs |
| --- | --- | --- |
| navigate | Open a webpage in a browser | url*<br>string<br>URL to navigate to<br>browserType<br>string<br>'chrome' \| 'firefox' \| 'edge'<br>sessionId<br>string<br>Browser session ID |
| click | Click on an element in the page | selector*<br>object<br>Element selector {type, value}<br>options<br>object<br>{waitForElement, timeout}<br>sessionId*<br>string<br>Browser session ID |
| type | Enter text into form fields | selector*<br>object<br>Element selector {type, value}<br>text*<br>string<br>Text to type<br>options<br>object<br>{clearFirst, submitAfter}<br>sessionId*<br>string<br>Browser session ID |
| wait | Wait for elements to appear | selector*<br>object<br>Element selector {type, value}<br>options<br>object<br>{timeout, pollInterval}<br>sessionId*<br>string<br>Browser session ID |
| screenshot | Capture the current page state | sessionId*<br>string<br>Browser session ID |
| get_content | Get page information | type*<br>string<br>'url' \| 'title' \| 'source'<br>sessionId*<br>string<br>Browser session ID |
| execute_script | Run JavaScript code | script*<br>string<br>JavaScript code to execute<br>args<br>array<br>Arguments to pass<br>sessionId*<br>string<br>Browser session ID |

## Installation

### Using NPX

Run directly without installation:

```bash
npx @thinkai/selenium-mcp-server
```

### Using Docker

1. Build the image:
```bash
docker build -t selenium-mcp-server .
```

2. Run the container:
```bash
docker run -d \
  --name selenium-mcp \
  -p 3000:3000 \
  selenium-mcp-server
```

3. With custom configuration (optional):
```bash
docker run -d \
  --name selenium-mcp \
  -p 3000:3000 \
  -e PORT=3000 \
  -e LOG_LEVEL=info \
  -e MAX_SESSIONS=5 \
  selenium-mcp-server
```

Or use our pre-built image:
```bash
docker run -d \
  --name selenium-mcp \
  -p 3000:3000 \
  thinkai/selenium-mcp-server
```

The Docker image includes:
- Node.js 18 LTS
- Chrome and Firefox browsers
- All necessary browser dependencies
- Pre-configured environment

## Parameters

### Docker Configuration

| Parameter | Description |
| --- | --- |
| PORT | Server port (default: 3000) |
| LOG_LEVEL | Winston log level |
| MAX_SESSIONS | Max concurrent browser sessions |
| TIMEOUT | Default operation timeout (ms) |
| RETRIES | Operation retry count |

### NPX Configuration

| Parameter | Description |
| --- | --- |
| PORT | Server port (default: 3000) |
| LOG_LEVEL | Winston log level |
| MAX_SESSIONS | Max concurrent browser sessions |
| TIMEOUT | Default operation timeout (ms) |
| RETRIES | Operation retry count |

## Configuration

> Claude Desktop ｜ Vscode Cline

Add this to your `config.json`:

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

### NPX Configuration

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

## Build

Docker build:

```bash
docker build -t thinkai/selenium-mcp-server:latest .
```

## Development

1. Install dependencies:
```bash
pnpm install
```

2. Run in development mode:
```bash
pnpm dev
```

3. Run tests:
```bash
pnpm test
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
