# Steam 状态监控插件V2

## 访问统计
![:shell](https://count.getloli.com/@github_monitor_shell?name=github_monitor_shell&theme=minecraft&padding=7&offset=0&align=top&scale=1&pixelated=1&darkmode=auto)

本插件是专为AstrBot设计的插件，用于定时轮询 Steam Web API，监控指定玩家的在线/离线/游戏状态变更，并在状态变化时推送通知。支持多 SteamID 监控，自动记录游玩日志，支持群聊分组，数据持久化，支持丰富指令。

## 功能特性
- 支持定时轮询多个 SteamID 的状态，分群管理，每个群聊可独立配置监控玩家
- 检测玩家上线、下线、开始/切换/退出游戏等状态变更，自动推送游戏启动/关闭提醒
- 成就变动自动推送提醒
- 已配置自动轮询频率，默认为1-30分钟查询一次状态，取决于steam的上次在线时间
- 持久化记录玩家游玩日志，重启bot后状态不会丢失

## 默认轮询间隔说明
| 玩家最近在线时间 | 轮询间隔 |
| ---------------- | -------- |
| 12分钟内         | 1分钟    |
| 12分钟~3小时     | 5分钟    |
| 3小时~24小时     | 10分钟   |
| 24~48小时        | 20分钟   |
| 超过48小时       | 30分钟   |

## 快速上手
1. 在AstrBot网页后台的配置中配置 Steam_Web_API_Key：[点击获取](https://steamcommunity.com/dev/apikey)
2. 在AstrBot网页后台的配置中配置 SGDB_API_KEY（用于获取封面图，可选）：[点击获取](https://www.steamgriddb.com/profile/preferences/api)
3. （可选）在AstrBot网页后台配置中添加 `steam_group_mapping` 配置项，格式为 `SteamID|群号`，例如：`76561198888888888|123456789`
4. 在需要进行提醒的群聊输入指令：
   `/steam addid [Steam64位ID]`  （如：/steam addid 7656119xxxxxxxxxx）
5. 启动轮询：
   `/steam on`  启动本群 Steam 状态监控，后续状态变更会自动推送。

注意：通过 `steam_group_mapping` 配置的 SteamID 与群号映射关系会自动应用于对应的群组，无需手动执行 `/steam addid` 命令。



## 注意事项
- 获取速度与是否成功获取 Steam 数据取决于网络环境。建议通过加速或魔法手段来保证稳定的查询状态。

- 遇到升级后，如果出现未知的轮询错误可以使用 `/steam clear_allids` 来清除所有群聊的轮询id，并重新添加
- 修改插件参数后，如果出现重复通知的情况，请不要重载插件，而是重启astrbot。
- 如果出现未知的无法提醒，但轮询显示正常的情况，请使用 /steam on/off 进行修复
- 部分设备会出现2.1.7或以上版本无法正常进行信息推送的情况，需降级为2.1.6或以下版本使用。
## 演示截图
![开始游戏示例](https://raw.githubusercontent.com/Maoer233/astrbot_plugin_steam_status_monitor/main/str.png)
![结束游戏示例](https://raw.githubusercontent.com/Maoer233/astrbot_plugin_steam_status_monitor/main/stop.png)
![成就推送示例](https://raw.githubusercontent.com/Maoer233/astrbot_plugin_steam_status_monitor/main/achievement.png)


## 指令列表
- `/steam on` 启动本群Steam状态监控
- `/steam off` 停止本群Steam状态监控
- `/steam list` 列出本群所有玩家当前状态
- `/steam check` 立即手动检测本群并推送变更
- `/steam alllist` 列出所有群聊分组及玩家状态
- `/steam config` 查看当前插件配置
- `/steam set [参数] [值]` 设置配置参数（如 `/steam set poll_interval_sec 30`）
- `/steam addid [SteamID] [QQ号]` 添加监控，可绑定QQ号以显示群名片（如 `/steam addid 76561198xxxxxxxxx 123456789`）
- `/steam bind [SteamID] [QQ号]` 为已添加的SteamID绑定或更新QQ号
- `/steam delid [SteamID]` 从本群监控列表删除SteamID
- `/steam openbox [SteamID]` 查看指定SteamID的全部详细信息
- `/steam rs` 清除所有状态并初始化（可能不生效）
- `/steam clear_allids` 初始化清空所有群聊监控id
- `/steam achievement_on` 开启本群Steam成就推送
- `/steam achievement_off` 关闭本群Steam成就推送
- `/steam test_achievement_render [steamid] [gameid] [数量]` 测试成就图片渲染
- `/steam test_game_start_render [steamid] [gameid]` 测试开始游戏图片渲染
- `/steam清除缓存` 清除所有头像、封面图等图片缓存
- `/steam help` 显示所有指令帮助

## 依赖
- Python 3.7+
- httpx
- Pillow
- AstrBot 框架

### 依赖安装方法
如果显示缺少依赖，你可以尝试下载以下工具来进行修复
pip install httpx pillow

### 新增配置项
- `card_update_interval_sec`: 群名片自动更新间隔，默认 86400 秒（24小时）。

可以添加QQ：1912584909 来反馈功能和建议 闲聊也欢迎喵~

## ⭐ Stars

> 如果本项目对您的生活 / 工作产生了帮助，或者您关注本项目的未来发展，请给项目 Star，这是我维护这个开源项目的动力 ❤️。

## 更新日志

### v2.2.6
- 新增群名片显示功能：支持绑定 QQ 号，优先显示群名片。
- 新增指令 `/steam bind`：用于绑定或更新 SteamID 对应的 QQ 号。
- 优化 `/steam addid`：支持直接在添加时指定 QQ 号。
- 优化图片渲染：游戏开始/结束图片将只显示群名片（如有），界面更清爽。
- 性能优化：`/steam list` 列表查询改为并发执行，响应速度大幅提升。

### v2.1.9
- 新增 `steam_group_mapping` 配置项，支持通过配置文件预设 SteamID 与群号的映射关系
- 修复配置项与命令数据不互通的问题


## 🐔 联系作者

- **反馈**：欢迎在 [GitHub Issues](https://github.com/1592363624/astrbot_plugin_zanwo_shell/issues) 提交问题或建议
QQ群:91219736
telegram:[巅峰阁](https://t.me/ShellDFG)