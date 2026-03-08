---
name: x-mcp
description: "小红书全能助手：支持账号状态检查、搜索笔记、生成封面、获取详情、点赞收藏、评论互动及发布图文/视频。"
---

# 小红书自动化工具集

通过 mcporter 桥接 aredink.com 提供的 MCP 服务。

## check_login_status
检查当前小红书账号的登录状态。

### 运行
```bash
npx mcporter x-mcp.check_login_status
```

## search_feeds

搜索小红书内容。

### 参数

* `keyword`: (required) 搜索关键词。
* `filters`: (optional) 筛选选项。

### 运行

```bash
npx mcporter x-mcp.search_feeds --keyword "{{keyword}}" --filters "{{filters}}"
```

## list_feeds

获取小红书首页推荐内容流。

### 运行

```bash
npx mcporter x-mcp.list_feeds
```

## get_feed_detail

获取小红书笔记详情，返回笔记内容、图片、作者信息、互动数据及评论列表。

### 参数

* `feed_id`: (required) 小红书笔记ID，从Feed列表获取。
* `xsec_token`: (required) 访问令牌，从Feed列表的xsec_token字段获取。
* `load_all_comments`: (optional) 是否加载全部评论。false仅返回前10条一级评论（默认），true滚动加载更多评论。
* `limit`: (optional) 【仅当load_all_comments为true时生效】限制加载的一级评论数量。默认20。
* `click_more_replies`: (optional) 【仅当load_all_comments为true时生效】是否展开二级回复。true展开子评论，false不展开（默认）。
* `reply_limit`: (optional) 【仅当click_more_replies为true时生效】跳过回复数过多的评论。默认10。
* `scroll_speed`: (optional) 【仅当load_all_comments为true时生效】滚动速度slow慢速、normal正常、fast快速。

### 运行

```bash
npx mcporter x-mcp.get_feed_detail --feed_id "{{feed_id}}" --xsec_token "{{xsec_token}}"
```

## xhs_generate_cover

生成小红书封面图并上传到云存储，返回可访问的URL地址。

### 参数

* `title`: (required) 主标题文字。
* `subtitle`: (required) 副标题文字。
* `template`: (required) 模板样式：modern（现代）、minimal（极简）、pixel（像素）。
* `description`: (optional) 描述文字。
* `emoji`: (optional) 要显示的emoji表情。

### 运行

```bash
npx mcporter x-mcp.xhs_generate_cover --title "{{title}}" --subtitle "{{subtitle}}" --template "{{template}}" --description "{{description}}" --emoji "{{emoji}}"
```

## publish_content

发布小红书图文内容，可设置定时发布（1小时后～14天内）。

### 参数

* `title`: (required) 内容标题（小红书限制：最多20个中文字或英文单词）。
* `content`: (required) 正文内容，不包含以#开头的标签内容。
* `images`: (required) 图片列表（至少1张，最多9张），支持多种格式：1) base64 data URL 2) HTTP/HTTPS 网络地址 3) 本地文件路径。
* `tags`: (optional) 话题标签列表，如 ["美食", "旅行", "生活"]。
* `schedule_at`: (optional) 定时发布时间，格式示例：2025-01-20T14:30:00+08:00，需在1小时后～14天内。
* `is_original`: (optional) 是否声明原创，true为声明原创，false或不填则不声明。
* `products`: (optional) 要绑定的商品关键字列表，如 ["睫毛膏", "口红"]，系统会根据关键字搜索并选择第一个匹配商品。
* `visibility`: (optional) 可见范围，支持: 公开可见(默认)、仅自己可见、仅互关好友可见。

### 运行

```bash
npx mcporter x-mcp.publish_content --title "{{title}}" --content "{{content}}" --images "{{images}}" --tags "{{tags}}" --schedule_at "{{schedule_at}}" --is_original "{{is_original}}" --products "{{products}}" --visibility "{{visibility}}"
```

## publish_with_video

发布小红书视频内容，可设置定时发布（1小时后～14天内）。

### 参数

* `title`: (required) 视频标题（小红书限制：最多20个中文字或英文单词）。
* `content`: (required) 视频描述正文，不包含以#开头的标签内容。
* `video`: (optional) 视频文件的 URL 地址，支持 http/https 链接，系统会自动下载视频并上传到小红书。如果不提供，则使用之前通过 upload_video 上传的视频。
* `tags`: (optional) 话题标签列表。
* `schedule_at`: (optional) 定时发布时间，格式示例：2025-01-20T14:30:00+08:00，需在1小时后～14天内。
* `products`: (optional) 要绑定的商品关键字列表，如 ["睫毛膏", "口红"]。
* `visibility`: (optional) 可见范围，支持: 公开可见(默认)、仅自己可见、仅互关好友可见。

### 运行

```bash
npx mcporter x-mcp.publish_with_video --title "{{title}}" --content "{{content}}" --video "{{video}}" --tags "{{tags}}" --schedule_at "{{schedule_at}}" --products "{{products}}" --visibility "{{visibility}}"
```

## like_feed

为指定笔记点赞或取消点赞。

### 参数

* `feed_id`: (required) 小红书笔记ID，从Feed列表获取。
* `xsec_token`: (required) 访问令牌，从Feed列表的xsec_token字段获取。
* `unlike`: (optional) 是否取消点赞，true为取消点赞，false或未设置则为点赞。

### 运行

```bash
npx mcporter x-mcp.like_feed --feed_id "{{feed_id}}" --xsec_token "{{xsec_token}}" --unlike "{{unlike}}"
```

## favorite_feed

收藏指定笔记或取消收藏。

### 参数

* `feed_id`: (required) 小红书笔记ID，从Feed列表获取。
* `xsec_token`: (required) 访问令牌，从Feed列表的xsec_token字段获取。
* `unfavorite`: (optional) 是否取消收藏，true为取消收藏，false或未设置则为收藏。

### 运行

```bash
npx mcporter x-mcp.favorite_feed --feed_id "{{feed_id}}" --xsec_token "{{xsec_token}}" --unfavorite "{{unfavorite}}"
```

## post_comment_to_feed

发表评论到小红书笔记。

### 参数

* `feed_id`: (required) 小红书笔记ID，从Feed列表获取。
* `xsec_token`: (required) 访问令牌，从Feed列表的xsec_token字段获取。
* `content`: (required) 评论内容。

### 运行

```bash
npx mcporter x-mcp.post_comment_to_feed --feed_id "{{feed_id}}" --xsec_token "{{xsec_token}}" --content "{{content}}"
```

## reply_comment_in_feed

回复小红书笔记下的指定评论。

### 参数

* `feed_id`: (required) 小红书笔记ID，从Feed列表获取。
* `xsec_token`: (required) 访问令牌，从Feed列表的xsec_token字段获取。
* `content`: (required) 回复内容。
* `comment_id`: (optional) 目标评论ID，从评论列表获取（comment_id 或 user_id 至少提供一个）。
* `user_id`: (optional) 目标评论用户ID，从评论列表获取（comment_id 或 user_id 至少提供一个）。

### 运行

```bash
npx mcporter x-mcp.reply_comment_in_feed --feed_id "{{feed_id}}" --xsec_token "{{xsec_token}}" --content "{{content}}" --comment_id "{{comment_id}}" --user_id "{{user_id}}"
```
