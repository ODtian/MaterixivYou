# 实施票据索引

母规格：[Spec #1](https://github.com/ODtian/MaterixivYou/issues/1)。
共 26 张已批准的实施票据，分诊标签为 ready-for-agent。每票覆盖完整交付路径与场景验收。

| 代号 | Issue | 交付行为 | 直接阻塞 |
| --- | --- | --- | --- |
| APP-01 | [#2 — Android 宿主从安装到启动及恢复](https://github.com/ODtian/MaterixivYou/issues/2) | 可安装的 Android 宿主显示一个可操作页面，用户切到后台再返回时恢复页面状态，并形成可重复验证的构建路径。 | 可立即开始 |
| APP-02 | [#3 — Native AOT 安装包消费 M3 组件](https://github.com/ODtian/MaterixivYou/issues/3) | Android Native AOT 安装包消费版本化 M3 包，启动后执行主题按钮场景并完成前后台恢复。 | [APP-01](https://github.com/ODtian/MaterixivYou/issues/2), [M3-01](https://github.com/ODtian/Avalonia.Material3/issues/2) |
| APP-03 | [#12 — Satori 与基准运行时完成同场景对照](https://github.com/ODtian/MaterixivYou/issues/12) | 同一 Native AOT 客户端场景分别运行于基准和 Satori 配置，给出可重复的启动、帧时间、内存及稳定性对照，并据此确定交付配置。 | [APP-08](https://github.com/ODtian/MaterixivYou/issues/9) |
| APP-04 | [#5 — 正式详情页呈现常驻信息与悬浮入口](https://github.com/ODtian/MaterixivYou/issues/5) | 可控数据源返回作品后，正式详情页展示图片、常驻标题作者、可展开信息和独立收藏入口，模式配置进入次级设置。 | [APP-01](https://github.com/ODtian/MaterixivYou/issues/2), [M3-04](https://github.com/ODtian/Avalonia.Material3/issues/9), [M3-09](https://github.com/ODtian/Avalonia.Material3/issues/7), [M3-14](https://github.com/ODtian/Avalonia.Material3/issues/16) |
| APP-05 | [#4 — 账号授权后查看资料并恢复会话](https://github.com/ODtian/MaterixivYou/issues/4) | 用户完成 Pixiv 授权，客户端显示账号资料并建立安全持久会话，再次启动可继续访问账号页面。 | [APP-01](https://github.com/ODtian/MaterixivYou/issues/2), [M3-03](https://github.com/ODtian/Avalonia.Material3/issues/4) |
| APP-06 | [#6 — 作品列表进入真实详情并返回原位置](https://github.com/ODtian/MaterixivYou/issues/6) | 用户浏览推荐作品、继续加载，进入真实作品详情后返回列表，内容与位置保持连续。 | [APP-05](https://github.com/ODtian/MaterixivYou/issues/4), [APP-04](https://github.com/ODtian/MaterixivYou/issues/5) |
| APP-07 | [#8 — 关注排行趋势与作者路径可持续浏览](https://github.com/ODtian/MaterixivYou/issues/8) | 用户切换关注、排行、趋势和作者作品，逐页浏览并进入详情，各来源保留自己的条件和位置。 | [APP-06](https://github.com/ODtian/MaterixivYou/issues/6), [M3-16](https://github.com/ODtian/Avalonia.Material3/issues/17) |
| APP-08 | [#9 — 图片流在目标设备满足帧与内存预算](https://github.com/ODtian/MaterixivYou/issues/9) | 用户快速滚动图片流、切作品并缩放，按目标设备的刷新率验证帧时间和缓存预算，并持续恢复界面。 | [APP-06](https://github.com/ODtian/MaterixivYou/issues/6), [APP-02](https://github.com/ODtian/MaterixivYou/issues/3) |
| APP-09 | [#10 — Token 刷新后并发原请求自动恢复](https://github.com/ODtian/MaterixivYou/issues/10) | 列表和详情遇到鉴权过期时共享一次刷新，随后自动恢复各自请求，保留位置并连续呈现加载结果。 | [APP-06](https://github.com/ODtian/MaterixivYou/issues/6), [M3-13](https://github.com/ODtian/Avalonia.Material3/issues/15) |
| APP-10 | [#13 — 插画与小说评论入口分页展示回复](https://github.com/ODtian/MaterixivYou/issues/13) | 用户从作品详情或小说入口查看评论、加载下一页并阅读回复关系，失败后继续恢复当前列表。 | [APP-09](https://github.com/ODtian/MaterixivYou/issues/10) |
| APP-11 | [#14 — 收藏处理中与结果在各页面同步](https://github.com/ODtian/MaterixivYou/issues/14) | 用户添加或取消收藏时立即看到处理中，服务确认后列表与详情同步结果，切换作品也能正确归属操作。 | [APP-09](https://github.com/ODtian/MaterixivYou/issues/10), [M3-11](https://github.com/ODtian/Avalonia.Material3/issues/12) |
| APP-12 | [#15 — 多关键词编辑后显式提交模糊搜索](https://github.com/ODtian/MaterixivYou/issues/15) | 用户编辑多个词条、选择建议并显式提交模糊查询，查看分页结果并返回继续编辑当前搜索。 | [APP-09](https://github.com/ODtian/MaterixivYou/issues/10), [M3-08](https://github.com/ODtian/Avalonia.Material3/issues/11) |
| APP-13 | [#17 — 单词条历史从提交到管理和重启恢复](https://github.com/ODtian/MaterixivYou/issues/17) | 组合搜索提交后分别记录各词条；用户点击历史追加当前搜索，删除、清空或固定记录，再次启动保留管理结果。 | [APP-12](https://github.com/ODtian/MaterixivYou/issues/15) |
| APP-14 | [#18 — 既有译名数据与中文文案贯通主要页面](https://github.com/ODtian/MaterixivYou/issues/18) | 客户端通过现有中文译名路径和缓存，在详情、搜索、趋势及作者页面统一显示标签；界面与操作反馈使用维护的中文文案。 | [APP-07](https://github.com/ODtian/MaterixivYou/issues/8), [APP-12](https://github.com/ODtian/MaterixivYou/issues/15) |
| APP-15 | [#19 — 小说入口到结构化正文阅读](https://github.com/ODtian/MaterixivYou/issues/19) | 用户从小说推荐、关注、排行或搜索进入正文，阅读段落、章节和插图，并恢复请求异常后的内容。 | [APP-12](https://github.com/ODtian/MaterixivYou/issues/15) |
| APP-16 | [#22 — 小说系列收藏书签与阅读位置恢复](https://github.com/ODtian/MaterixivYou/issues/22) | 用户切换系列相邻作品、收藏和设置书签，调整阅读偏好，重开后继续正确的阅读位置。 | [APP-15](https://github.com/ODtian/MaterixivYou/issues/19), [APP-11](https://github.com/ODtian/MaterixivYou/issues/14), [M3-10](https://github.com/ODtian/Avalonia.Material3/issues/8) |
| APP-17 | [#16 — 单文件从入队到保存打开和分享](https://github.com/ODtian/MaterixivYou/issues/16) | 用户将作品图片加入队列，看到文件进度，完成后在选定目录打开或分享保存结果。 | [APP-09](https://github.com/ODtian/MaterixivYou/issues/10), [M3-11](https://github.com/ODtian/Avalonia.Material3/issues/12) |
| APP-18 | [#20 — 暂停续传网络恢复与重启继续下载](https://github.com/ODtian/MaterixivYou/issues/20) | 用户暂停再继续下载，网络恢复或应用重启后按资源版本恢复进度，完成的文件保持正确内容。 | [APP-17](https://github.com/ODtian/MaterixivYou/issues/16) |
| APP-19 | [#23 — 批量作品队列归组并发去重与重试](https://github.com/ODtian/MaterixivYou/issues/23) | 用户批量加入和管理作品任务，调整并发、暂停或重试，单项失败时其他可运行任务继续下载。 | [APP-18](https://github.com/ODtian/MaterixivYou/issues/20), [M3-06](https://github.com/ODtian/Avalonia.Material3/issues/5), [M3-10](https://github.com/ODtian/Avalonia.Material3/issues/8) |
| APP-20 | [#24 — 后台下载与通知持续恢复队列](https://github.com/ODtian/MaterixivYou/issues/24) | 用户切到其他应用后，在系统允许的执行条件下继续下载，通知展示当前进度并可控制任务，返回后恢复队列视图。 | [APP-19](https://github.com/ODtian/MaterixivYou/issues/23) |
| APP-21 | [#25 — 目录命名与记录文件管理保持一致](https://github.com/ODtian/MaterixivYou/issues/25) | 用户调整保存目录和命名方式，定位完成作品并清理任务记录或独立管理文件，数据与操作范围一致。 | [APP-19](https://github.com/ODtian/MaterixivYou/issues/23) |
| APP-22 | [#26 — 动图资源包与小说 TXT 完成下载导出](https://github.com/ODtian/MaterixivYou/issues/26) | 用户保存动图原始资源与帧信息，或将小说导出为 TXT，队列和文件管理展示对应的完整结果。 | [APP-19](https://github.com/ODtian/MaterixivYou/issues/23), [APP-16](https://github.com/ODtian/MaterixivYou/issues/22) |
| APP-23 | [#11 — 两种图片区模式与区域手势正确分工](https://github.com/ODtian/MaterixivYou/issues/11) | 用户在设置切换横向分页与纵向浏览；图片区按所选模式浏览内容，信息区横向直接切作品，缩放和抽屉操作连续可用。 | [APP-06](https://github.com/ODtian/MaterixivYou/issues/6), [M3-18](https://github.com/ODtian/Avalonia.Material3/issues/19) |
| APP-24 | [#21 — 收藏按钮重力换边服务单手操作](https://github.com/ODtian/MaterixivYou/issues/21) | 用户启用重力换边，倾斜设备将悬浮收藏按钮吸附到另一侧，回正后保留位置并继续收藏。 | [APP-23](https://github.com/ODtian/MaterixivYou/issues/11), [APP-11](https://github.com/ODtian/MaterixivYou/issues/14), [M3-06](https://github.com/ODtian/Avalonia.Material3/issues/5), [M3-10](https://github.com/ODtian/Avalonia.Material3/issues/8) |
| APP-25 | [#7 — 全局主题与阅读偏好在正式设置中生效](https://github.com/ODtian/MaterixivYou/issues/7) | 用户在正式设置调整主题、动态配色及字体尺度，主要页面立即生效，重开后继续使用自己的偏好。 | [APP-04](https://github.com/ODtian/MaterixivYou/issues/5), [M3-02](https://github.com/ODtian/Avalonia.Material3/issues/3), [M3-06](https://github.com/ODtian/Avalonia.Material3/issues/5), [M3-10](https://github.com/ODtian/Avalonia.Material3/issues/8) |
| APP-26 | [#27 — 正式客户端从冷启动到主要场景发布验收](https://github.com/ODtian/MaterixivYou/issues/27) | 用户安装正式 Native AOT 客户端，从冷启动、登录和主要功能到前后台恢复完成使用，获得统一的 M3 Expressive 体验与可维护发布版本。 | [APP-03](https://github.com/ODtian/MaterixivYou/issues/12), [APP-10](https://github.com/ODtian/MaterixivYou/issues/13), [APP-13](https://github.com/ODtian/MaterixivYou/issues/17), [APP-14](https://github.com/ODtian/MaterixivYou/issues/18), [APP-20](https://github.com/ODtian/MaterixivYou/issues/24), [APP-21](https://github.com/ODtian/MaterixivYou/issues/25), [APP-22](https://github.com/ODtian/MaterixivYou/issues/26), [APP-24](https://github.com/ODtian/MaterixivYou/issues/21), [APP-25](https://github.com/ODtian/MaterixivYou/issues/7), [M3-19](https://github.com/ODtian/Avalonia.Material3/issues/20) |

## 当前起始前沿

- [APP-01 — Android 宿主从安装到启动及恢复](https://github.com/ODtian/MaterixivYou/issues/2)

## 推进规则

后续根据 GitHub 原生 blocked-by 关系和实际完成状态选择可开始任务。App 消费对应能力的 M3 版本化包，跨仓库依赖使用完整 Issue 链接。
当前阶段由主代理直接推进，各任务结果与验收记录写入对应仓库和 Issue。
