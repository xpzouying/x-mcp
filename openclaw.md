# OpenClaw 接入 x-mcp (小红书) 完整指南

本指南介绍如何通过 **mcporter** 桥接器，将 **x-mcp** (aredink.com) 的小红书自动化能力集成到 **OpenClaw** 中。

## 1. 环境配置 (mcporter)

首先，你需要配置 `mcporter` 来访问远程的 MCP 服务。

1. 打开或创建配置文件：`~/.mcporter/mcporter.json`
2. 填入以下内容（**请务必将 `sk_xxx` 替换为您自己的 API Key**）：

```json
{
  "mcpServers": {
    "x-mcp": {
      "description": "x-mcp aredink.com 小红书助手",
      "url": "https://mcp.aredink.com/mcp",
      "headers": {
        "X-API-Key": "sk_请在此处替换您的实际密钥"
      }
    }
  },
  "imports": []
}
```

**验证配置：**
在终端运行 `npx mcporter x-mcp list`。如果能列出 `xhs_` 开头的 8 个函数，则配置正确。

---

## 2. OpenClaw Skill 定义 (SKILL.md)

将本仓库提供的 `x-mcp/SKILL.md` 文件复制到 OpenClaw 项目的 skills 目录下（`<openclaw-project>/skills/x-mcp/`）。

**目录结构：**
```
<openclaw-project>/
└── skills/
    └── x-mcp/
        ├── SKILL.md              # 工具定义
        └── reference/
            └── troubleshooting.md # 故障排除参考
```

---

## 3. 在 OpenClaw 中激活

1.  **加载 Skill**：在 OpenClaw 的 `openclaw.json` 配置中，将 `x-mcp` 的 `enabled` 设为 `true`。
2.  **环境变量**：确保 OpenClaw 的执行环境能够找到 `node` 和 `npx`。
3.  **开始对话**：直接在对话框输入指令即可触发。

### 典型应用场景示例

* **指令**："看看现在小红书上关于'DeepSeek'的热门笔记有哪些？"
    * *AI 会自动调用 `search_feeds`*
* **指令**："帮我写一篇关于'极简主义穿搭'的小红书笔记，并用 modern 模板生成一个封面。"
    * *AI 会先生成文案，随后连续调用 `xhs_generate_cover` 和 `publish_content`*
