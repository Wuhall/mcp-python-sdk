# Simple Auth Client Example  
# 简单认证客户端示例

A demonstration of how to use the MCP Python SDK with OAuth authentication over streamable HTTP or SSE transport.  
演示如何通过可流式HTTP或SSE传输，使用MCP Python SDK进行OAuth认证。

## Features  
## 功能特性

- OAuth 2.0 authentication with PKCE  
- 支持带PKCE的OAuth 2.0认证
- Support for both StreamableHTTP and SSE transports  
- 支持StreamableHTTP和SSE两种传输方式
- Interactive command-line interface  
- 交互式命令行界面

## Installation  
## 安装

```bash
cd examples/clients/simple-auth-client
uv sync --reinstall 
```

## Usage  
## 用法

### 1. Start an MCP server with OAuth support  
### 1. 启动支持OAuth的MCP服务器

```bash
# Example with mcp-simple-auth
# 使用mcp-simple-auth示例
cd path/to/mcp-simple-auth
uv run mcp-simple-auth --transport streamable-http --port 3001
```

### 2. Run the client  
### 2. 运行客户端

```bash
uv run mcp-simple-auth-client

# Or with custom server URL
# 或自定义服务器URL
MCP_SERVER_PORT=3001 uv run mcp-simple-auth-client

# Use SSE transport
# 使用SSE传输
MCP_TRANSPORT_TYPE=sse uv run mcp-simple-auth-client
```

### 3. Complete OAuth flow  
### 3. 完成OAuth流程

The client will open your browser for authentication. After completing OAuth, you can use commands:  
客户端会自动打开浏览器进行认证。完成OAuth后，你可以使用如下命令：

- `list` - List available tools  
- `list` - 列出可用工具
- `call <tool_name> [args]` - Call a tool with optional JSON arguments    
- `call <tool_name> [args]` - 调用工具并可选传递JSON参数
- `quit` - Exit  
- `quit` - 退出

## Example  
## 示例

```
🔐 Simple MCP Auth Client
🔐 简单MCP认证客户端
Connecting to: http://localhost:3001
正在连接：http://localhost:3001

Please visit the following URL to authorize the application:
请访问以下URL以授权应用：
http://localhost:3001/authorize?response_type=code&client_id=...

✅ Connected to MCP server at http://localhost:3001
✅ 已连接到MCP服务器：http://localhost:3001

mcp> list
mcp> list
📋 Available tools:
📋 可用工具：
1. echo - Echo back the input text
1. echo - 回显输入文本

mcp> call echo {"text": "Hello, world!"}
mcp> call echo {"text": "Hello, world!"}
🔧 Tool 'echo' result:
🔧 工具'echo'结果：
Hello, world!
Hello, world!

mcp> quit
mcp> quit
👋 Goodbye!
👋 再见！
```

## Configuration  
## 配置

- `MCP_SERVER_PORT` - Server URL (default: 8000)  
- `MCP_SERVER_PORT` - 服务器URL（默认：8000）
- `MCP_TRANSPORT_TYPE` - Transport type: `streamable_http` (default) or `sse`  
- `MCP_TRANSPORT_TYPE` - 传输类型：`streamable_http`（默认）或`sse`
