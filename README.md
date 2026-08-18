# 我们的家 · 前端

一个手机上用的伴侣型聊天应用**前端**。粉色、毛玻璃、启动动画、可拖动的桌宠、
首页小组件（天气 / 纪念日 / 热力日历）、聊天气泡与输入区。

**直接用浏览器打开 `index.html` 就能看**，不需要装任何东西、不需要服务器。

![纯前端 · 无依赖](https://img.shields.io/badge/%E7%BA%AF%E5%89%8D%E7%AB%AF-%E6%97%A0%E4%BE%9D%E8%B5%96-c96f87)

## 这是什么，不是什么

- ✅ **是**：一整套做好的界面，拿去改配色、改布局、改文案
- ❌ **不是**：一个能真的聊天的产品。对话内容是**演示数据**

页面里的对话、天气、额度都来自内置的演示层（`<script id="oss-demo">`）。
它把发往 `/home-api/*` 的请求拦下来返回假数据，所以离线也能完整显示。

## 接自己的后端

删掉 `index.html` 末尾那块 `<script id="oss-demo">`，然后实现下面这些接口
（同源、返回 JSON、带 cookie 鉴权）：

| 接口 | 作用 |
|---|---|
| `GET /home-api/auth/status` | 是否已登录 |
| `GET /home-api/chat/list` | 对话列表 |
| `GET /home-api/chat/messages?chat_id=` | 某个对话的消息 |
| `POST /home-api/chat/send` | 发消息（流式） |
| `GET /home-api/chat/profile` | 昵称、头像 |
| `GET /home-api/chat/weather` | 首页天气 |
| `GET /home-api/chat/status` | 连接状态、额度 |

返回结构照着演示层里的 `DEMO` 对象写就行，那里每个接口都有一份样例。

## 设置里有什么

公开版只保留三样：**主题（浅色 / 深色 / 跟随系统）**、**天气城市**、**玻璃质感**。

其余设置块（聊天连接、开发引擎、主动消息、人格设定等）都是接自建服务的，
在 `<style id="oss-trim">` 里用 CSS 隐藏了 —— 没有删代码，因为页面脚本到处
引用那些元素的 id，直接删会报错。想彻底清掉，连相关 JS 一起删才安全。

## 结构

单文件。HTML、CSS、JS 全在 `index.html` 里（约 20000 行），
配图在 `assets/`。没有构建步骤、没有 npm、没有框架。

改配色从 `:root` 那几个变量入手；毛玻璃相关的类名是 `hg-clear` / `hg-frost` /
`home-liquid-on`；深色主题走 `body[data-nh-theme="dark"]`。

## 说明

- 界面里的人名都是占位（阿念 / 小满），随便改
- 毛玻璃（`backdrop-filter`）在 iPhone 上比较吃性能，页面里有 100 多处，
  介意的话可以按需关掉
- 图标、启动画面等资源版权归原作者

## 许可

MIT，见 [LICENSE](LICENSE)。
