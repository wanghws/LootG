# Changelog

## v1.3.1

- Fixed the settings window rendering blank — tab contents never drew due to a callback signature mismatch.
- Unified the display settings between Loot Notification and Combat State: both now use Scroll Speed (multiplier of 100 px/s) and Fade Time (seconds); old loot `scrollTime` / `fadeSpeed` values are auto-converted per profile.
- The enter/leave combat text boxes now show the effective localized default instead of appearing empty; clearing them restores the follow-client-locale behavior.
- Fixed long combat state text (e.g. "Leave Combat") being truncated with an ellipsis.
- Fixed a Lua error when looting caged battle pets and other non-item links.
- Switching / copying / resetting profiles now applies anchors and lock state immediately.
- Tuned defaults: loot font size 14, display time 1.5s, fade 0.1s, Y offset 250; combat display time 1s.
- zhCN / zhTW leave-combat wording changed to "离开战斗" / "離開戰鬥".
- 修复设置窗口空白：回调参数不匹配导致 Tab 内容从未绘制。
- 统一拾取通知与战斗状态的显示参数：均使用"滚动速度"（100 px/s 的倍率）和"渐隐时间"（秒）；旧的拾取 `scrollTime` / `fadeSpeed` 存档按 profile 自动换算迁移。
- 进入/离开战斗文本输入框现在显示生效的本地化默认值，不再显示为空；清空即恢复跟随客户端语言。
- 修复战斗状态长文本（如 "Leave Combat"）被截断为省略号的问题。
- 修复拾取笼装战斗宠物等非物品链接时的 Lua 报错。
- 切换/复制/重置配置文件后锚点位置和锁定状态立即生效。
- 默认值调整：拾取字号 14、显示 1.5 秒、渐隐 0.1 秒、Y 偏移 250；战斗状态显示 1 秒。
- 简体/繁体"脱离战斗"文案更名为"离开战斗"/"離開戰鬥"。

## v1.3.0

- Rewrote settings UI on Ace3 (AceGUI/AceConfig/AceDB/LibSharedMedia). Standalone floating window with Loot / Combat State / Profiles tabs.
- Added profile support (Profiles tab) so multiple characters can share or diverge on settings.
- Added LibSharedMedia font list — any user-installed font from an LSM-aware addon is available in the font dropdown.
- Fixed enter/leave combat default text sometimes freezing at whatever locale seeded the SavedVariables on first install. Defaults are now empty strings and the runtime falls back to the localized default text each call.
- Existing LootGDB SavedVariables are auto-migrated into the new LootGAceDB shape on first launch.
- Interface bumped to 12.0.5 / 12.0.7.
- Rolled up the taint-error and dedup fixes shipped in 1.2.2 / 1.2.3.
- 基于 Ace3 (AceGUI/AceConfig/AceDB/LibSharedMedia) 重写设置界面：独立浮动窗口，拾取通知 / 战斗状态 / 配置文件 三个 Tab。
- 新增配置文件（Profiles）支持，多角色可共用或独立设置。
- 新增 LibSharedMedia 字体池：任何 LSM 兼容插件安装的字体都可在字体下拉中选择。
- 修复某些情况下"进入/脱离战斗"默认文本被首次安装时的客户端语言锁定的问题。默认值改为空串，运行时每次读取当前语言的本地化字符串。
- 首次启动自动迁移旧 LootGDB 中的设置到新 LootGAceDB。
- Interface 升级至 12.0.5 / 12.0.7。
- 汇总合并 1.2.2 / 1.2.3 的 taint 与去重修复。

## v1.2.3

- Bug fixes.
- 修复若干问题。

## v1.2.2

- Bug fixes.
- 修复若干问题。

## v1.2.1

- Added loot, currency, and gold notifications from opened containers, and restored missing chest and quest reward messages.
- Fixed duplicate or mixed notifications for personal currency, dungeon loot, and chest gold rewards.
- Fixed gold amount scaling, currency link fallback parsing, and duplicate gold icon display issues.
- Improved scrolling message updates with one shared animation loop, overlap avoidance, and smoother fading.
- Fixed profession skill notifications to use stable fileID icons and more reliable profession name matching.
- Fixed errors caused by secret values.
- 新增容器开启后的物品、通货与金币通知，并恢复遗漏的宝箱与任务奖励提示。
- 修复个人货币、地下城掉落与宝箱金币提示重复或数值串入的问题。
- 修复金币倍率、通货链接回退解析以及金币图标重复显示问题。
- 优化滚动消息更新逻辑，统一动画循环，避免消息重叠并让渐隐更平滑。
- 修复商业技能提升提示的图标来源与专业名称匹配稳定性。
- 修复秘密值报错。

## v1.2.0

- Gold display now shows all sources (vendor, quest, loot, mail, etc.).
- Added reputation change notifications with matching chat color.
- Added profession skill up notifications.
- 金币显示不再限于拾取，支持所有来源（商人、任务、邮件等）。
- 新增声望变化通知，颜色与聊天窗口一致。
- 新增商业技能提升通知。

## v1.1.0

- Added Combat State flash text module with Scroll/Static modes and 4-direction scrolling.
- Subcategory settings, independent anchors and font settings per module.
- Merged into single LootG.lua, continuous scrolling, localized UI labels.
- 新增战斗状态闪烁文字模块，支持滚动/静态模式和四方向滚动。
- 分类设置面板，每个模块独立锚点和字体设置。
- 多语言界面标签，UI 布局优化。

## v1.0.0

- Initial release: scrolling loot display with animation, item quality colors, customizable fonts and positioning, settings panel integration.
- 首次发布：带动画的滚动拾取显示，物品品质颜色、可自定义字体和位置。
