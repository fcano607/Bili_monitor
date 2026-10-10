# B站动态钉钉监控

一个在 Windows 系统托盘中运行的本地工具，定时检查指定 UP 主的动态，并通过钉钉机器人推送新动态。通过浏览器控制台管理配置，使用 SQLite 保存去重状态。

当前提供 Windows x64 可执行文件和技术说明文档，尚未包含原始源码及依赖文件。

## 快速使用

1. 下载并双击运行 [BiliDingTalkMonitor.exe](BiliDingTalkMonitor.exe)，浏览器会打开本地控制台。
2. 填写钉钉机器人 Webhook；按机器人的安全设置填写加签密钥、匹配的关键词。需要登录权限时，填写自己的 B站 Cookie。
3. 添加需要监控的 UP 主，支持输入 UID 或个人空间链接。
4. 保存配置，点击测试钉钉推送，确认可以收到测试消息。
5. 点击“启动后台监控”。建议轮询间隔设置为 60 秒或更长。

关闭浏览器后，后台监控继续运行。可以通过右下角托盘图标重新打开控制台，或选择“退出”结束程序。

## 使用说明

- 默认首次检查只记录已有动态，之后发现的新动态才会推送。
- 当前每次重新打开程序后，需要手动启动后台监控；托盘图标存在不代表监控已启动。
- “推送 0 条”不能单独证明没有新动态或检查成功，请结合错误日志判断。
- 动态是否可获取，取决于账号权限和 B站接口返回内容；接口或平台规则变化可能影响使用。
- 钉钉 Webhook 的获取方式和适用条件，请参考[钉钉官方开发者说明](https://open-dingtalk.github.io/developerpedia/docs/learn/bot/webhook/overview/)。

## 配置与数据

运行数据保存在 `%APPDATA%\BiliDingTalkMonitor`：

| 文件 | 用途 |
| --- | --- |
| `config.yaml` | UP 列表、轮询间隔及推送配置 |
| `state.sqlite3` | 动态去重状态 |
| `monitor.log` | 运行日志（如生成） |

不要上传真实 Cookie、Webhook、加签密钥及运行数据；分享界面截图前请遮盖这些内容。

## 技术文档

模块设计、数据流、打包思路和问题排查见 [项目技术说明](B站UP主动态钉钉监控项目落地文档.md)。文档中的打包示例需在补齐源码和依赖后使用。

发布版本时，可将 EXE 放到 [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)，并附上版本说明。
