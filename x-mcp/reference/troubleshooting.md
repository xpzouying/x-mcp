# x-mcp 问题排查指南

## 快速索引

| 问题 | 解决方案 |
|------|----------|
| 工具不存在 | 配置 ~/.mcporter/mcporter.json（见下方配置示例） |
| 未登录 | 在浏览器登录 xiaohongshu.com |
| 发布失败 | 检查 content 不含 #，tags 不加 #，标题 ≤20 字 |
| 详情获取失败 | 确认 feed_id 和 xsec_token 来自同一笔记 |

## 详细错误说明

### NOT_LOGGED_IN
用户未在小红书网站登录。需要在浏览器访问 xiaohongshu.com 并登录。

### INVALID_PARAMS
参数格式错误，常见原因：
- `content` 包含 `#` 开头的标签 → 将标签移到 `tags` 参数
- `tags` 包含 `#` 前缀 → 移除 #，如 `["美食"]` 而非 `["#美食"]`
- `images` 为空或超过 9 张 → 确保 1-9 张图片

### TITLE_TOO_LONG
标题超过 20 个中文字或英文单词。需要精简标题。

### INVALID_SCHEDULE_TIME
定时发布时间不符合要求（需在 1 小时后～14 天内）。

## mcporter 配置示例

创建 `~/.mcporter/mcporter.json`：

```json
{
  "mcpServers": {
    "x-mcp": {
      "description": "x-mcp 小红书助手",
      "url": "https://mcp.aredink.com/mcp",
      "headers": {
        "X-API-Key": "你的API密钥"
      }
    }
  }
}
```

## 参数规范参考

### publish_content
```json
{
  "title": "标题（≤20字）",
  "content": "正文内容，不含#标签",
  "images": ["url1", "url2"],
  "tags": ["标签1", "标签2"],
  "schedule_at": "2025-03-10T14:00:00+08:00",
  "is_original": true,
  "visibility": "公开可见"
}
```

### get_feed_detail
```json
{
  "feed_id": "从搜索结果获取",
  "xsec_token": "从同一笔记获取",
  "load_all_comments": true
}
```
