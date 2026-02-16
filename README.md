# X-MCP

这里是项目 [x.zouying.work](https://x.zouying.work/) 的示例和反馈的地方。

因为有很多非技术同学在使用 [xiaohongshu-mcp](https://github.com/xpzouying/xiaohongshu-mcp) 的时候，都遇到了各种各样的部署的问题，所以在此开发了一套浏览器插件版本的 MCP。

目前处于内测环节，可能会遇到各种问题，欢迎反馈。

使用该插件：

- 不需要复杂的部署流程
- 自动化操作可见
- 账号和浏览器的账号复用

【一键发布 DEMO】

https://github.com/user-attachments/assets/57916170-ef39-43b3-92d8-f7555b32a795


## 1. 使用指南

### 1.1. 安装插件

**方式一：Chrome 应用商店安装（推荐）**

1. 访问 [Chrome 应用商店 - 小红书MCP助手](https://chromewebstore.google.com/detail/%E5%B0%8F%E7%BA%A2%E4%B9%A6mcp%E5%8A%A9%E6%89%8B/dklmcgbmpnmkndhapabinagmmdmjhjgl)
2. 点击"添加到 Chrome"按钮
3. 确认安装即可

> 推荐使用 Chrome 应用商店安装：简单快捷，自动更新。

**方式二：下载安装包**（适合无法访问 Chrome 应用商店的情况）

1. 打开 [x.zouying.work](https://x.zouying.work/) 页面，点击 "下载安装包" 链接，下载插件。

2. 下载并在本地解压。

3. 打开 Chrome 浏览器扩展管理（地址栏输入 `chrome://extensions/`），开启 "开发者模式"，选择 "加载已解压的扩展程序"。

<img width="2604" height="1006" alt="image" src="https://github.com/user-attachments/assets/5e646991-bbcd-4020-9ab0-12cbdc5cddcd" />


### 1.2. 注册并且登录

打开 [x.zouying.work](https://x.zouying.work/) 进行注册并且登录。

点击【创建连接】，会获取一个 API Token，保存好，只会展示一次。这个 API Token 需要填入小红书 MCP 的浏览器插件中，

<img width="2496" height="1490" alt="image" src="https://github.com/user-attachments/assets/171da49c-a0b3-4f26-b7d3-fd0f090187f5" />

浏览器插件填入 API Token 后，就能从控制台看到对应的浏览器插件的连接状态。

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/92e21798-79d9-45fe-9909-009b1fde53b6" />


<img width="2528" height="1330" alt="image" src="https://github.com/user-attachments/assets/856304aa-ce72-4ded-a154-3a42261e06ac" />

### 1.3. 测试

首先，填入跟小红书 MCP 绑定的 API Token，

<img width="2496" height="1712" alt="image" src="https://github.com/user-attachments/assets/3ee1abc1-d5c2-4ce6-a4b3-2a4ff0f12d19" />

测试一下小红书 MCP 是否正常，以测试检查登录状态为例。

https://github.com/user-attachments/assets/4e1d4348-d268-4fc4-8563-a24a84e309e9

### 2. 客户端接入

以 Claude Code 为例，

```
claude mcp add --transport http x-mcp https://mcp.zouying.work/mcp --header "X-API-Key: <你的API-TOKEN>"
```

视频演示：

https://github.com/user-attachments/assets/aef73b85-fd8b-4cdb-b156-fd3005a33bbd



支持通用的 MCP 协议的客户端接入，

1. 选择 HTTP 协议
2. 连接地址：`https://mcp.zouying.work/mcp`
3. 设置认证：Header 中增加字段： `X-API-Key`，值为 <你的API-TOKEN>。

更多客户端进行补充。

### 示例 - 发布

依然是我们的发布示例，

```
帮我写一篇帖子发布到小红书上，
配图为：https://cn.bing.com/th?id=OHR.MaoriRock_EN-US6499689741_UHD.jpg&w=3840
图片是："纽西兰陶波湖的Ngātoroirangi矿湾毛利岩雕（© Joppi/Getty Images）"

使用 x-mcp 进行发布。
```

https://github.com/user-attachments/assets/cce5d21c-94e0-4dd0-ba4c-5cfd2c65946a

### 示例 - 发布视频

依然是使用我们的发布视频示例，

```帮我 2 个小时后，发布一篇视频文章，内容随意，视频已上传给了插件，不要询问，直接操作。
视频为：创作中心上传视频

使用 x-mcp 进行视频发布。
```
https://github.com/user-attachments/assets/ef68dd72-8b8b-425b-ad22-7ede050bf125


### 示例 - 生成封面图片

https://github.com/user-attachments/assets/a41faf51-0d0f-48ca-bde5-0a92efac4bde

### 微信群聊

![x-mcp](https://github.com/user-attachments/assets/38c5bdd9-fced-4c2b-8307-ba3a1cc4662a)


