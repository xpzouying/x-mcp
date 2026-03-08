# 小红书 MCP 技术规范

## 工具列表

| 工具 | 功能 | 适用场景 |
|------|------|----------|
| search_feeds | 搜索小红书内容 | 热门内容分析、竞品研究 |
| xhs_generate_cover | 生成封面图 | 自动化封面制作 |
| publish_content | 发布图文笔记 | 自动化内容发布 |
| list_feeds | 获取首页推荐 | 趋势分析 |
| get_feed_detail | 获取笔记详情 | 数据抓取、内容分析 |
| post_comment_to_feed | 发表评论 | 自动互动 |
| reply_comment_in_feed | 回复评论 | 精准互动 |
| like_feed | 点赞/取消点赞 | 互动操作 |
| favorite_feed | 收藏/取消收藏 | 互动操作 |
| check_login_status | 检查登录状态 | 前置检查 |
| publish_with_video | 发布视频笔记 | 视频内容发布 |

---

## 参数规范

### publish_content（发布图文）

**参数说明**

| 参数 | 类型 | 必填 | 限制 | 示例 |
|------|------|------|------|------|
| title | string | ✅ | ≤20字，emoji≤2个 | "早餐颜值天花板！草莓酸奶碗" |
| content | string | ✅ | 纯文本，**禁止含#标签** | 见下方示例 |
| images | array[string] | ✅ | 1-9张，支持URL/base64/本地路径 | ["https://...", "data:image/..."] |
| tags | array[string] | ❌ | **不加#前缀**，3-5个 | ["早餐", "健康饮食"] |
| schedule_at | string | ❌ | ISO 8601格式，1小时后～14天内 | "2025-02-28T14:30:00+08:00" |
| is_original | boolean | ❌ | 声明原创 | true |
| products | array[string] | ❌ | 商品关键字列表 | ["睫毛膏", "口红"] |
| visibility | string | ❌ | 公开可见/仅自己可见/仅互关好友可见 | "公开可见" |

**content 格式示例**
```
早餐真的太重要了！今天分享一个超简单的早餐搭配～

🥣 草莓酸奶燕麦碗
- 燕麦片 50g
- 原味酸奶 200ml
- 新鲜草莓 5-6 颗

做法超简单！燕麦片加热水泡软，倒入酸奶，摆上草莓就完成啦～

你们早餐都吃什么呀？～
```

**正确调用示例**
```json
{
  "title": "早餐颜值天花板！草莓酸奶碗太好吃了吧",
  "content": "早餐真的太重要了！今天分享一个超简单的早餐搭配～\n\n🥣 草莓酸奶燕麦碗\n- 燕麦片 50g\n- 原味酸奶 200ml\n- 新鲜草莓 5-6 颗\n\n做法超简单！燕麦片加热水泡软，倒入酸奶，摆上草莓就完成啦～\n\n你们早餐都吃什么呀？～",
  "images": ["https://example.com/cover.jpg"],
  "tags": ["早餐", "健康饮食", "草莓燕麦"],
  "is_original": true,
  "visibility": "公开可见"
}
```

**错误调用示例**
```json
{
  "title": "早餐颜值天花板！草莓酸奶碗太好吃了吧",
  "content": "早餐真的太重要了！\n\n#早餐 #健康饮食 #草莓燕麦",  // ❌ content 中不能包含 # 标签
  "images": ["https://example.com/cover.jpg"],
  "tags": ["#早餐", "#健康饮食", "#草莓燕麦"]  // ❌ tags 不需要 # 前缀
}
```

---

### publish_with_video（发布视频）

| 参数 | 类型 | 必填 | 说明 | 示例 |
|------|------|------|------|------|
| title | string | ✅ | 视频标题，≤20字 | "美食制作教程" |
| content | string | ✅ | 视频描述，**禁止含#标签** | "今天教大家做一道简单的..." |
| video | string | ❌ | 视频URL地址，不提供则使用之前上传的视频 | "https://..." |
| tags | array[string] | ❌ | 话题标签，**不加#前缀** | ["美食", "教程"] |
| schedule_at | string | ❌ | 定时发布时间（ISO格式），1小时后～14天内 | "2025-02-28T14:30:00+08:00" |
| products | array[string] | ❌ | 商品关键字列表 | ["美食材料"] |
| visibility | string | ❌ | 公开可见/仅自己可见/仅互关好友可见 | "公开可见" |

---

### xhs_generate_cover（生成封面）

| 参数 | 类型 | 必填 | 可选值/说明 | 示例 |
|------|------|------|-------------|------|
| title | string | ✅ | 主标题 | "早餐分享" |
| subtitle | string | ✅ | 副标题 | "5分钟搞定" |
| template | string | ✅ | modern / minimal / pixel | "modern" |
| description | string | ❌ | 描述文字 | "健康早餐推荐" |
| emoji | string | ❌ | emoji表情 | "🥣" |

**模板说明**
- `modern`：现代风格，渐变背景，适合生活方式类内容
- `minimal`：极简风格，留白多，适合高级感内容
- `pixel`：像素风格，复古感，适合游戏/科技类内容

---

### search_feeds（搜索内容）

| 参数 | 类型 | 必填 | 可选值/说明 | 示例 |
|------|------|------|-------------|------|
| keyword | string | ✅ | 搜索关键词 | "早餐" |
| filters | object | ❌ | 筛选选项 | {"sort": "popularity"} |

---

### get_feed_detail（获取笔记详情）

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| feed_id | string | ✅ | 笔记ID，必须从搜索结果中获取 |
| xsec_token | string | ✅ | 访问令牌，必须从搜索结果中获取 |
| load_all_comments | boolean | ❌ | 是否加载全部评论，默认false |
| limit | number | ❌ | 限制加载的一级评论数量，默认20 |
| click_more_replies | boolean | ❌ | 是否展开二级回复，默认false |
| reply_limit | number | ❌ | 跳过回复数过多的评论，默认10 |
| scroll_speed | string | ❌ | 滚动速度：slow/normal/fast |

⚠️ **注意**：`feed_id` 和 `xsec_token` 必须通过 `search_feeds` 或 `list_feeds` 的返回结果获取，不能自行构造。

---

### like_feed（点赞/取消点赞）

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| feed_id | string | ✅ | 笔记ID（从搜索结果获取） |
| xsec_token | string | ✅ | 访问令牌（从搜索结果获取） |
| unlike | boolean | ❌ | true为取消点赞，false为点赞（默认） |

---

### favorite_feed（收藏/取消收藏）

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| feed_id | string | ✅ | 笔记ID（从搜索结果获取） |
| xsec_token | string | ✅ | 访问令牌（从搜索结果获取） |
| unfavorite | boolean | ❌ | true为取消收藏，false为收藏（默认） |

---

### post_comment_to_feed（发表评论）

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| feed_id | string | ✅ | 笔记ID（从搜索结果获取） |
| xsec_token | string | ✅ | 访问令牌（从搜索结果获取） |
| content | string | ✅ | 评论内容 |

---

### reply_comment_in_feed（回复评论）

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| feed_id | string | ✅ | 笔记ID（从搜索结果获取） |
| xsec_token | string | ✅ | 访问令牌（从搜索结果获取） |
| content | string | ✅ | 回复内容 |
| comment_id | string | ❌ | 目标评论ID（comment_id 或 user_id 至少提供一个） |
| user_id | string | ❌ | 目标评论用户ID（comment_id 或 user_id 至少提供一个） |

---

## 内容规范

### 标题规范
- 长度：最多20个中文字或英文单词
- Emoji：建议使用，但不超过2个
- 技巧：使用数字、制造对比、引发好奇、直击痛点

### 正文规范
- 结构：3-5段，每段2-3句话
- 格式：支持换行和emoji
- 语言：生动有趣，避免过度营销感
- **重要**：content 中**禁止**包含以#开头的标签

### 标签规范
- 数量：3-5个
- 格式：纯文本，**不要加 # 前缀**
- 策略：热门标签+精准标签组合
- **重要**：通过 `tags` 参数单独传递，不要写在 content 中

### 图片规范
- 数量：1-9张
- 格式：支持URL、Base64 data URL、本地路径
- 推荐：封面图使用 `xhs_generate_cover` 生成

### 定时发布规范
- 时间格式：ISO 8601格式，如 "2025-02-28T14:30:00+08:00"
- 时间范围：必须在1小时后～14天内
- 时区：建议明确指定时区（如 +08:00）

### 可见范围规范
- `公开可见`：所有人可见（默认）
- `仅自己可见`：仅发布者可见
- `仅互关好友可见`：仅互相关注的好友可见

---

## 违禁词清单

以下内容不允许出现在小红书笔记中：

| 类型 | 违禁词示例 |
|------|-----------|
| 引流类 | 评论、关注、私信、加微信、加群 |
| 广告类 | 推广、合作、招商、加盟、代理 |
| 诱导类 | 点击链接、扫码、下载APP |

---

## 常见错误

### 错误1：content 中包含 # 标签
```json
// ❌ 错误
{
  "content": "早餐真的太重要了！\n\n#早餐 #健康饮食"
}

// ✅ 正确
{
  "content": "早餐真的太重要了！",
  "tags": ["早餐", "健康饮食"]
}
```

### 错误2：tags 包含 # 前缀
```json
// ❌ 错误
{
  "tags": ["#早餐", "#美食"]
}

// ✅ 正确
{
  "tags": ["早餐", "美食"]
}
```

### 错误3：标题超过长度限制
```json
// ❌ 错误（超过20字）
{
  "title": "这是一个非常非常非常长的标题超过了二十个中文字的长度限制会导致发布失败"
}

// ✅ 正确
{
  "title": "早餐分享｜5分钟搞定高颜值燕麦碗"
}
```

### 错误4：图片数量不符合要求
```json
// ❌ 错误（缺少图片）
{
  "images": []
}

// ❌ 错误（超过9张）
{
  "images": ["1.jpg", "2.jpg", ..., "10.jpg"]
}

// ✅ 正确
{
  "images": ["cover.jpg"]
}
```

### 错误5：feed_id 和 xsec_token 不匹配
```json
// ❌ 错误（必须同时使用同一篇笔记的 feed_id 和 xsec_token）
{
  "feed_id": "笔记A的ID",
  "xsec_token": "笔记B的token"
}

// ✅ 正确
{
  "feed_id": "从搜索结果获取的笔记ID",
  "xsec_token": "从同一笔记获取的xsec_token"
}
```

---

## 自动化流程示例

### 场景1：自动发布带封面的图文笔记

```
1. 准备内容（标题、正文、图片列表）
2. 如需要封面 → 调用 xhs_generate_cover
3. 组装参数（注意 content 和 tags 分开）
4. 调用 publish_content 发布
```

### 场景2：搜索热门内容并分析

```
1. 调用 search_feeds（keyword=目标关键词）
2. 获取返回结果的 feed_id 和 xsec_token
3. 调用 get_feed_detail 获取详情
4. 分析标题、内容结构、标签策略
```

### 场景3：批量互动（点赞+收藏+评论）

```
1. 调用 search_feeds 或 list_feeds 获取笔记列表
2. 提取 feed_id 和 xsec_token
3. 调用 like_feed 点赞
4. 调用 favorite_feed 收藏
5. 调用 post_comment_to_feed 发表评论
```

### 场景4：定时发布视频

```
1. 准备视频内容和元数据
2. 调用 publish_with_video，传入 schedule_at 参数
3. 系统将在指定时间自动发布
```

---

## 返回值说明

### 成功响应
```json
{
  "success": true,
  "data": {
    "noteId": "1234567890",
    "url": "https://www.xiaohongshu.com/explore/xxxxx"
  }
}
```

### 错误响应
```json
{
  "success": false,
  "error": {
    "code": "INVALID_PARAMS",
    "message": "标题长度超过限制"
  }
}
```

**常见错误码**
| 错误码 | 说明 |
|--------|------|
| INVALID_PARAMS | 参数格式错误 |
| TITLE_TOO_LONG | 标题超过20字限制 |
| INVALID_TAGS | tags格式错误（含#前缀或位置错误） |
| IMAGES_EMPTY | 图片列表为空 |
| TOO_MANY_IMAGES | 图片超过9张 |
| NOT_LOGGED_IN | 用户未登录 |
| PUBLISH_FAILED | 发布失败（小红书服务端错误） |
| INVALID_SCHEDULE_TIME | 定时发布时间不符合要求（1小时后～14天内） |

---

## 环境要求

- Node.js ≥ 16
- mcporter 已配置且可访问 x-mcp 服务
- 小红书账号已登录且状态正常
