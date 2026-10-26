# 猿媒BOT MCP · DeepSeek Harness 插件

> 产品文档与完整接入说明：https://github.com/CN-Jayden/yuanmei-bot-docs
>
> 这个仓库只负责 DeepSeek Harness 插件安装，不包含猿媒BOT 账号、知识库或业务数据。

在 DeepSeek Harness（DSH）里预置猿媒BOT MCP，安装后即可让 Agent 使用：

- `whoami`：验证令牌
- `list_robots`
- `list_conversations`
- `read_messages`
- `search_messages`
- `send_text`
- `send_image`
- `send_link`
- `schedule_message`

## 前置条件

1. 已安装 DeepSeek Harness（`dsh web` 可正常启动）
2. 在猿媒BOT「个人中心 → API 接入 → MCP 接入」签发长期令牌
3. 令牌只保存到本机环境变量，不要写进仓库

## 安装

### 从 npm 安装（发布后）

```bash
dsh plugin --profile web add yuanmei-bot-dsh-mcp
```

### 从本仓库安装

```bash
git clone https://github.com/CN-Jayden/yuanmei-bot-dsh-mcp.git
cd yuanmei-bot-dsh-mcp
dsh plugin --profile web add link:$(pwd)
```

### 设置令牌

```bash
export YUANMEI_MCP_TOKEN='你的猿媒BOT MCP 令牌'
```

Windows PowerShell：

```powershell
$env:YUANMEI_MCP_TOKEN = '你的猿媒BOT MCP 令牌'
```

建议把环境变量写入 DSH 的 profile 环境或系统环境变量，而不是写进仓库。

### 重启

```bash
dsh web
```

重启后，DSH 会加载 `@deepseek-ai/dsh-mcp-client`，工具名形如：

```text
mcp__yuanmei__whoami
mcp__yuanmei__list_robots
mcp__yuanmei__send_text
```

## 验证

在 DSH 中执行：

```text
调用 mcp__yuanmei__whoami
```

确认返回工作空间和工具范围后，再调用 `tools/list` 或发送类工具。

## 注意

- MCP 令牌等同密码，不要提交到 Git、不要发到群里
- 发送类工具风险为 medium，发送前确认目标和内容
- 如果已安装 `@hyzyn/dsh-mcp` 并手工配置过 `yuanmei`，不要再安装本插件，避免 `serverName` 冲突
- 需要固定出口 IP 时，在猿媒BOT MCP 接入页配置 IP 白名单
- 本插件只负责注册 MCP 客户端，不包含猿媒BOT 账号或令牌

## 发布

```bash
npm publish
```

发布前请确认 npm 包名可用，并更新 `package.json` 的 version。
