# SearchEngineJumpPlus 搜索引擎快捷跳转+

<div align="center">

<a href="https://github.com/mexiaow/SearchEngineJumpPlus/raw/main/searchEngineJump.user.js" target="_blank">
<img src="https://img.shields.io/badge/%E5%AE%89%E8%A3%85-%E7%82%B9%E5%87%BB%E5%AE%89%E8%A3%85%E8%84%9A%E6%9C%AC-2ea44f?logo=tampermonkey&style=for-the-badge" alt="安装"></a>
<a href="https://github.com/mexiaow/SearchEngineJumpPlus" target="_blank">
<img src="https://img.shields.io/badge/GitHub-%E4%BB%93%E5%BA%93-181717?logo=github&style=for-the-badge" alt="GitHub"></a>
<a href="https://github.com/mexiaow/SearchEngineJumpPlus/issues" target="_blank">
<img src="https://img.shields.io/badge/%E5%8F%8D%E9%A6%88-Issues-d73a4a?logo=github&style=for-the-badge" alt="Issues"></a>

</div>

## 安装

需要先安装 [Tampermonkey](https://www.tampermonkey.net/) 或 [Violentmonkey](https://violentmonkey.github.io/) 等用户脚本管理器，然后点击下面的链接安装：

**➡️ [点此安装 / 更新脚本](https://github.com/mexiaow/SearchEngineJumpPlus/raw/main/searchEngineJump.user.js)**

脚本头部的 `@updateURL` 已指向本仓库，之后本仓库递增版本号后，脚本管理器会自动检查并提示更新。

## 项目说明

本项目的前身是 [iqxin 维护的搜索引擎跳转脚本](https://github.com/qxinGitHub/searchEngineJump)，随后由 [MUTED64](https://github.com/MUTED64/SearchEngineJumpPlus) Fork 出来并做了大规模重构（Shadow DOM 样式隔离、严格 CSP 页面适配等）。

本仓库自 **5.32.8** 起从上游 Fork 出来独立维护：

- 脚本的 `@require`（GBK 编码函数、搜索引擎列表、网站规则）、`@resource`（全局样式）全部改为从本仓库加载，不再依赖上游的 GreasyFork 发布；
- `@namespace` / `@homepage` / `@supportURL` / `@updateURL` / `@downloadURL` 以及脚本内的反馈入口均指向本仓库；
- 后续的新功能、网站适配与问题修复都在本仓库进行。

原始脚本自 2011 年起由多位作者接力维护，具体见 [致谢](#致谢)。

## 使用说明

### 搜索页跳转

在脚本管理器中启用脚本后，当访问支持的搜索页时，页面中会显示脚本的跳转小横条，你可以点击其中的按钮跳转到相应的搜索引擎，并自动按照当前搜索框中的内容进行快捷的一键搜索。

<!-- 截图待补充：![SearchEngineJump](SearchEngineJump.png) -->

### 划词搜索

访问不支持搜索框的其它页面时，脚本默认开启划词搜索功能，在页面中使用鼠标划动取词，页面上方会弹出跳转小横条，此时可以点击其中的按钮跳转到相应的搜索引擎，并自动按照当前划词内容进行快捷的一键搜索。

<!-- 截图待补充：![SelectSearch](SelectSearch.png) -->

### 深色模式

脚本支持深色模式，但不同的页面对深色模式的适配不同，导致部分不支持深色模式的网站与操作系统或浏览器的默认设置冲突，因此建议与 [Dark Reader 拓展](https://darkreader.org/) 共同使用，自动根据操作系统设置渲染深色页面。

<!-- 截图待补充：![Dark](Dark.png) -->

### 设置菜单

跳转小横条的最后有设置按钮，点击后进入设置菜单，或者从脚本管理器的选项中也可以进入设置菜单。在设置菜单中可以对脚本的搜索引擎进行配置，例如拖拽调整位置、点击切换启用状态、添加或删除搜索引擎等。

「更多设置」中还可以调整固定到顶端、划词搜索、动画、隐藏同站链接、设置按钮透明度等选项。注意其中的部分开关需要刷新页面才会生效。

<!-- 截图待补充：![Settings](Settings.png) -->

## 目录结构

| 文件 | 说明 | 加载方式 |
| --- | --- | --- |
| `searchEngineJump.user.js` | 主脚本 | 由脚本管理器安装 |
| `rules.js` | 各搜索网站的匹配规则与插入样式 | `@require` |
| `engineList.js` | 默认搜索引擎列表（分类 + 各站点链接、图标） | `@require` |
| `GlobalStyle.css` | 跳转条与设置面板的全局样式 | `@resource GLOBAL_STYLE` |
| `toGBK.user.js` | 搜索词 GBK 编码函数（1688、樱花动漫等 GBK 站点需要） | `@require` |

## 维护与发布

- 想新增 / 修改某个网站的适配：改 `rules.js`；
- 想增删默认搜索引擎：改 `engineList.js`；
- 改样式：改 `GlobalStyle.css`。

**上述依赖文件改动后，必须同时递增主脚本头部的 `@version`。** 脚本管理器只在检测到脚本新版本时才会重新拉取 `@require` / `@resource`，否则用户端拿到的仍然是缓存的旧文件。

发布流程：

1. 修改依赖文件或主脚本，同步更新 `@version` 与 `@lastUpdated`，并在下面的「更新历史」补一条记录；
2. 提交并推送到 `main` 分支；
3. 用户端由脚本管理器自动检查更新，也可以用上面的安装链接手动覆盖安装。

> 提示：`@require` 目前使用 `main` 分支地址，由脚本管理器按 `@version` 缓存。如果希望某个版本永久固定，可改用 jsDelivr 的带版本地址，例如
> `https://cdn.jsdelivr.net/gh/mexiaow/SearchEngineJumpPlus@5.32.8/rules.js`。

## 更新历史

- version 5.32.8 2026-09-18
  - 调整：本仓库转为独立维护，`@author`、`@namespace`、`@homepage`、`@supportURL`、`@updateURL`、`@downloadURL` 以及脚本内的反馈与说明链接全部改为本仓库
  - 修复：设置面板 7 个开关（固定到顶端 / 仅上拉显示 / 折叠当前搜索分类 / 动画 / 划词搜索 / 隐藏同站链接 / 一键搜索）的复选框无法回显已保存状态，导致每次在面板中点「保存并关闭」都会把它们按「未勾选」写回，刷新后用户设置被清空
  - 修复：规则匹配成功但找不到输入框或插入位置时抛异常，导致整个脚本初始化中断的问题
  - 修复：第一个分类（网页）无法被禁用的问题

- version 5.32.7 2026-02-24
  - 修复：在 sandboxed frame 页面点击搜索引擎时，`target="_blank"` 被浏览器拦截（allow-popups 缺失）的问题
  - 调整：新标签打开优先使用 `GM_openInTab`，避免页面沙箱弹窗限制
  - 修复：点击图标子元素时目标识别不稳定导致跳转异常的问题

- version 5.32.6 2026-02-24
  - 修复：严格 CSP 页面中内联样式被拦截导致脚本样式失效、加载异常的问题
  - 调整：Shadow DOM 样式注入优先使用 Constructable Stylesheets
  - 调整：移除主要模板中的 inline style，严格 CSP 页面自动降级部分依赖内联样式的功能

- version 5.32.5 2026-01-16
  - 修复：Google 搜索框 z-index 遮挡问题

- version 5.32.4 2026-01-16
  - 修复：深色模式检测逻辑

- version 5.32.3 2026-01-16
  - 调整：Bilibili、Google 搜索框适配
  - 修复：深色模式检测逻辑
  - 修复：Bilibili 打开设置时跳转条重建的问题

- version 5.32.2 2026-01-16
  - 修复：淘宝、京东搜索框适配

- version 5.32.1 2026-01-16
  - 修复：深色模式检测逻辑
  - 修复：深色模式样式

- version 5.32.0 2026-01-14
  - 重构：使用 Shadow DOM 隔离样式，避免与网站样式冲突，避免 Obsidian Web Clipper 等插件冲突
  - 调整：部分网站适配

- version 5.31.17 2025-05-11
  - 修复：图标更新逻辑
  - 调整：更新贴吧图标

上面未列出的更早版本（4.1.0.0 ~ 5.31.16）见上游仓库的 [README 更新历史](https://github.com/MUTED64/SearchEngineJumpPlus#更新历史)。

## 致谢

- 原始作者：NLF（2011 年起）
- 修改与维护：锐经、[iqxin](https://github.com/qxinGitHub/searchEngineJump)
- Fork 重构与长期维护：[MUTED64](https://github.com/MUTED64/SearchEngineJumpPlus)
- 5.32.8 起的独立维护：[mexiaow](https://github.com/mexiaow)

## 许可证

本项目沿用 **MIT 许可证**，原始版权归原作者所有，详见 [LICENSE](LICENSE)。

原始脚本由 NLF 于 2011 年创建，后经 锐经、iqxin、MUTED64 等人接力修改与重构。MIT 许可证允许自由使用、修改与再分发，条件是保留原作者的署名与许可证声明，因此本仓库保留了完整的作者信息（脚本头部的 `@author` 与上面的[致谢](#致谢)）。
