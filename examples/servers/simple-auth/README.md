# Simple MCP Server with GitHub OAuth Authentication

# 简单的 MCP 服务器（集成 GitHub OAuth 认证）

This is a simple example of an MCP server with GitHub OAuth authentication. It demonstrates the essential components needed for OAuth integration with just a single tool.

这是一个集成了 GitHub OAuth 认证的 MCP 服务器示例。它展示了实现 OAuth 集成所需的基本组件，仅包含一个工具。

This is just an example of a server that uses auth, an official GitHub mcp server is [here](https://github.com/github/github-mcp-server)

这只是一个使用认证的服务器示例，官方的 GitHub MCP 服务器在 [这里](https://github.com/github/github-mcp-server)

## Overview

## 概述

This simple demo to show to set up a server with:
- GitHub OAuth2 authorization flow
- Single tool: `get_user_profile` to retrieve GitHub user information

本示例演示如何搭建一个服务器，包含：
- GitHub OAuth2 授权流程
- 单一工具：`get_user_profile` 用于获取 GitHub 用户信息

## Prerequisites

## 前置条件

1. Create a GitHub OAuth App:
   - Go to GitHub Settings > Developer settings > OAuth Apps > New OAuth App
   - Application name: Any name (e.g., "Simple MCP Auth Demo")
   - Homepage URL: `http://localhost:8000`
   - Authorization callback URL: `http://localhost:8000/github/callback`
   - Click "Register application"
   - Note down your Client ID and Client Secret

1. 创建一个 GitHub OAuth 应用：
   - 进入 GitHub 设置 > 开发者设置 > OAuth 应用 > 新建 OAuth 应用
   - 应用名称：任意（如 "Simple MCP Auth Demo"）
   - 主页 URL：`http://localhost:8000`
   - 授权回调 URL：`http://localhost:8000/github/callback`
   - 点击“注册应用”
   - 记下你的 Client ID 和 Client Secret

## Required Environment Variables

## 必需的环境变量

You MUST set these environment variables before running the server:

在运行服务器前，必须设置以下环境变量：

```bash
export MCP_GITHUB_GITHUB_CLIENT_ID="your_client_id_here"
export MCP_GITHUB_GITHUB_CLIENT_SECRET="your_client_secret_here"
```

The server will not start without these environment variables properly set.

如果没有正确设置这些环境变量，服务器将无法启动。


## Running the Server

## 运行服务器

```bash
# Set environment variables first (see above)

# Run the server
uv run mcp-simple-auth
```

The server will start on `http://localhost:8000`.

服务器将启动在 `http://localhost:8000`。

### Transport Options

### 传输选项

This server supports multiple transport protocols that can run on the same port:

该服务器支持多种传输协议，可以在同一端口上运行：

#### SSE (Server-Sent Events) - Default
```bash
uv run mcp-simple-auth
# or explicitly:
uv run mcp-simple-auth --transport sse
```

SSE transport provides endpoint:
- `/sse`

SSE 传输提供端点：
- `/sse`

#### Streamable HTTP
```bash
uv run mcp-simple-auth --transport streamable-http
```

Streamable HTTP transport provides endpoint:
- `/mcp`

Streamable HTTP 传输提供端点：
- `/mcp`


This ensures backward compatibility without needing multiple server instances. When using SSE transport (`--transport sse`), only the `/sse` endpoint is available.

这确保了向后兼容性，无需多个服务器实例。当使用 SSE 传输（`--transport sse`）时，仅 `/sse` 端点可用。

## Available Tool

## 可用工具

### get_user_profile

The only tool in this simple example. Returns the authenticated user's GitHub profile information.

**Required scope**: `user`

**Returns**: GitHub user profile data including username, email, bio, etc.

本示例中唯一的工具。返回经过身份验证的用户的 GitHub 个人资料信息。

**所需权限范围**：`user`

**返回**：GitHub 用户个人资料数据，包括用户名、电子邮件、个人简介等。


## Troubleshooting

## 故障排除

If the server fails to start, check:
1. Environment variables `MCP_GITHUB_GITHUB_CLIENT_ID` and `MCP_GITHUB_GITHUB_CLIENT_SECRET` are set
2. The GitHub OAuth app callback URL matches `http://localhost:8000/github/callback`
3. No other service is using port 8000
4. The transport specified is valid (`sse` or `streamable-http`)

如果服务器无法启动，请检查：
1. 环境变量 `MCP_GITHUB_GITHUB_CLIENT_ID` 和 `MCP_GITHUB_GITHUB_CLIENT_SECRET` 是否已设置
2. GitHub OAuth 应用的回调 URL 是否与 `http://localhost:8000/github/callback` 匹配
3. 没有其他服务占用 8000 端口
4. 指定的传输方式是否有效（`sse` 或 `streamable-http`）

You can use [Inspector](https://github.com/modelcontextprotocol/inspector) to test Auth