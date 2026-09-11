# dsh webUI CSS 颜色变量（`--dsw-*`）引用审计

> 审计对象：DeepSeek Harness webUI 前端中所有以 `dsw-` 开头的 **颜色** CSS 变量，查明每个变量被哪些 UI 元素直接引用。
> 产物：本文件。按 **static → specific → alias** 顺序排列（变量分组），即"变量被什么元素引用"视角。
> 配套插件 `dsh-customization-settings` 通过覆盖这些变量实现主题定制，本文件为其提供完整的引用面参考。

<!-- GENERATED-DOC: 由 .work-css-vars/ 下的脚本与子代理审计结果合并生成，勿手改主体 -->

## 1. 范围与方法

- **变量全集**：162 个颜色变量 = **73 static + 11 specific + 78 alias**，全部定义于 `@deepseek-ai/dsh-client-ui-theme` 包的 `design_platform_css_default` 样式表（`body` / `body[data-ds-dark-theme]` 两套作用域）。
- **非颜色变量排除**：`--dsw-font-*`（字体）、`--dsw-shadow-*`（阴影）、`--dsw-mask-blur`（滤镜）、`--dsw-linear-*`（渐变）、`--dsh-*` 等不属于"颜色变量"，不在此文档；仅当它们被颜色变量链引用时在相应位置注明。
- **浅色 / 深色**：所有变量在 `body`（浅色）与 `body[data-ds-dark-theme]`（深色，由 `html { color-scheme }` + `data-ds-dark-theme` 属性切换）下各有一份定义。本文每个变量均列出两套值；两套相同的注明"浅深相同"。
- **"直接引用"口径**：UI 元素样式/内联样式中出现 `var(--dsw-X)`（含 `var(--dsw-X, <fallback>)` 形式）或内联样式键 `"--dsw-X"`，记为"直接引用"，归入该变量标题下（需求 ①）。若变量定义指向另一变量（如 `--dsw-alias-x: var(--dsw-static-y)`），在该变量标题下注明指向（需求 ②）；static 变量标题下反向注明"被哪些 alias/specific 指向"。
- **证据来源**：webUI 前端无源码，审计基于构建产物：
  - 变量定义：`@deepseek-ai/dsh-client-ui-theme/lib/client.js`（5 个内嵌样式表）；
  - 使用面：33 个 `@deepseek-ai/dsh-client-*` 包的 `lib/client.js`（未压缩）+ `@deepseek-ai/dsh-web-frontend/dist/assets/` 的 `index-C6eRlFa6.css`、`vendor-CjyC-hUb.css`、`index-ClqxG24t.js`（压缩产物，含 shell 独有组件）。
  - 引用计数基准：dist 中 184 处命中 / 全部使用面 1358 处命中（含 fallback 形式）。
- **包 → UI 领域对照**：conversation=聊天主界面、sidebar=左侧边栏、layout=布局框架、settings*=设置面板、theme=主题设置面板、tool=工具调用卡片、trajectory=运行轨迹、goal=目标面板、jobs=任务列表、deliverables=交付物、attachment=附件、input-trigger=输入触发条、commands=命令面板、model-selection=模型选择器、message-feedback=消息反馈、permission-presets=权限预设、skill=技能、cordis=插件面板、user-questions=用户提问、workspace=工作区、agent-preset=代理预设、plan=计划、directory-picker=目录选择、connection=连接状态、locale=本地化、session-log-export=会话导出、subagent=子代理界面、workflow-run=工作流执行界面、agent-preset=代理预设。

## 2. 统计概览

- 变量总数：163（体系内 static 73 / specific 11 / alias 78 = 162，另体系外局部变量 --dsw-hovercard-bg 1 个）
- 有直接 UI 引用的变量：77（体系内 76 + 体系外 1；详见附录 C）
- 无直接 UI 引用（仅被其他变量定义引用或完全未被引用）的变量：86（均为体系内变量）
- dist 产物命中总数：184 处；全部使用面命中总数：1358 处

## 3. 分类体系说明

```
static（73）  基础色板，值全部为颜色字面量（如 #4176e6），浅深两套值几乎一致
  ▲ 被 specific / alias 的 var() 定义引用
specific（11） 面向具体界面部位的语义色（气泡、输入框、侧边栏等），值多为 var(--dsw-static-*)
  ▲ 被 alias 定义引用（--dsw-specific-menu → --dsw-alias-bg-layer-3）
alias（78）   全局语义层，值多为 var(--dsw-static-*) 或颜色字面量；--dsw-alias-button-primary-fill → var(--dsw-alias-brand-primary)（alias 指向 alias）
```

## 一、static 变量（73 个）

> static 为基础色板，值全部为颜色字面量。UI 元素极少直接引用它们（绝大多数经 alias/specific 间接生效），因此本节重点在于"被哪些 alias/specific 指向"，即修改该 static 会影响哪些语义层。

### `--dsw-static-amber-100`
- 值（浅色 / 深色）：`#fef5e7` / `#fef5e7`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-warn-tertiary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-amber-400`
- 值（浅色 / 深色）：`#f7ad31` / `#f7ad31`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-warn-secondary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-amber-500`
- 值（浅色 / 深色）：`#f59e0b` / `#f59e0b`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-warn-primary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-amber-600`
- 值（浅色 / 深色）：`#dd8629` / `#dd8629`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-warn-label`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-amber-900`
- 值（浅色 / 深色）：`#27241f` / `#27241f`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-warn-tertiary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-100`
- 值（浅色 / 深色）：`#dbeafe` / `#dbeafe`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-300`
- 值（浅色 / 深色）：`#93c5fd` / `#93c5fd`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-400`
- 值（浅色 / 深色）：`#60a5fa` / `#60a5fa`（浅深相同）
- **直接引用的 UI 元素**：
  - 终端命令块 TerminalBlock（dsh-web-frontend·dist 构建产物/命令执行终端块）：ANSI SGR 前景色映射表 `xf` 的条目 `"85,85,255":"var(--dsw-static-blue-400)"`（ANSI 标准蓝 85,85,255）；dsh-web-frontend/dist/assets/index-ClqxG24t.js:56，经 `bf()` 转为输出 token 的内联 `color` 样式（**仅 dist**；client.js 中仅 theme 定义行 124，已排除）

### `--dsw-static-blue-450`
- 值（浅色 / 深色）：`#4d93f8` / `#4d93f8`（浅深相同）
- **直接引用的 UI 元素**：
  - 上下文占用仪表盘 ContextMeter（dsh-client-ui-conversation·发送按钮旁 context 占用环 + 点击展开的 system/tools/messages 明细面板）：选择器 `.JObwrW_colorMessages{--meter-tint:var(--dsw-static-blue-450)}`（dsh-client-ui-conversation/lib/client.js:3036）→ 自定义属性 --meter-tint，被 `.JObwrW_segment{background:var(--meter-tint,var(--dsw-alias-label-tertiary))}` 与 `.JObwrW_swatch{background:var(--meter-tint)}` 消费 → messages 段条/图例色块背景

### `--dsw-static-blue-50`
- 值（浅色 / 深色）：`#eff6ff` / `#eff6ff`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-500`
- 值（浅色 / 深色）：`#3b82f6` / `#3b82f6`（浅深相同）
- **直接引用的 UI 元素**：
  - 运行轨迹表 TrajectoryTable（dsh-client-ui-trajectory·轨迹时间线/运行记录表）：dsh-client-ui-trajectory/lib/client.js:2995，两处：
  - `.Y0dWHa_table{--trajectory-turn-accent:color-mix(in srgb, var(--dsw-static-blue-500) 22%, var(--dsw-alias-bg-layer-1))}` → 自定义属性 --trajectory-turn-accent（表底色混蓝）
  - `.Y0dWHa_turnLabelActive{color:color-mix(in srgb, var(--dsw-static-blue-500) 55%, var(--dsw-alias-label-tertiary));background:var(--trajectory-turn-accent)}` → 当前激活 turn 标签的 color / background

### `--dsw-static-blue-50p`
- 值（浅色 / 深色）：`#eaf3ff` / `#eaf3ff`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-600`
- 值（浅色 / 深色）：`#2563eb` / `#2563eb`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-75`
- 值（浅色 / 深色）：`#e5f0ff` / `#e5f0ff`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-800`
- 值（浅色 / 深色）：`#1e40af` / `#1e40af`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-900`
- 值（浅色 / 深色）：`#0e3074` / `#0e3074`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-label-primary-bluish`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-blue-950`
- 值（浅色 / 深色）：`#172554` / `#172554`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-100`
- 值（浅色 / 深色）：`#e4edfd` / `#e4edfd`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-business-tertiary`；specific 1 个：`--dsw-specific-sidebar-nav-item-active-accent`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-200`
- 值（浅色 / 深色）：`#d3e2ff` / `#d3e2ff`（浅深相同）
- 被以下变量定义指向：specific 1 个：`--dsw-specific-bubble-highlight`
- **直接引用的 UI 元素**：
  - 聊天视图 ChatView 的 turn 状态文本（dsh-client-ui-conversation·"Deep diving..." 工作状态指示，shimmer 动画渐变文字）：`.Md3f7G_turnStatus{background:linear-gradient(90deg, var(--dsw-static-deepseek-500) 0%, var(--dsw-static-deepseek-500) 40%, var(--dsw-static-deepseek-200) 50%, var(--dsw-static-deepseek-500) 60%, var(--dsw-static-deepseek-500) 100%);color:#0000;-webkit-text-fill-color:transparent;background-clip:text}`（dsh-client-ui-conversation/lib/client.js:5452）→ background（渐变扫描光带的中间亮色）

### `--dsw-static-deepseek-300`
- 值（浅色 / 深色）：`#b7c8fe` / `#b7c8fe`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-400`
- 值（浅色 / 深色）：`#679efe` / `#679efe`（浅深相同）
- 被以下变量定义指向：alias 3 个：`--dsw-alias-button-info-fill`、`--dsw-alias-button-info-hover`、`--dsw-alias-state-business-primary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-450`
- 值（浅色 / 深色）：`#5686fe` / `#5686fe`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-brand-primary-new-colorprimary-new-color`
- **直接引用的 UI 元素**：
  - 运行状态指示点 StateDot（dsh-web-frontend·dist 构建产物/终端命令块 prompt 前的状态 orb，ongoing 态为矩阵动画）：`._dot_10orb_3,._matrix_10orb_4{--dsh-state-ongoing:var(--dsw-static-deepseek-450)}`，被 `._matrix_10orb_4{color:var(--dsh-state-ongoing)}` 与 `._cell_10orb_54{fill:currentColor}` 消费 → ongoing 状态 color/fill（dsh-web-frontend/dist/assets/index-C6eRlFa6.css:1，**仅 dist**；client.js 中仅 theme 定义行 124，已排除）

### `--dsw-static-deepseek-50`
- 值（浅色 / 深色）：`#edf3fe` / `#edf3fe`（浅深相同）
- 被以下变量定义指向：specific 1 个：`--dsw-specific-bubble`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-500`
- 值（浅色 / 深色）：`#4176e6` / `#4176e6`（浅深相同）
- 被以下变量定义指向：alias 3 个：`--dsw-alias-button-info-fill`、`--dsw-alias-button-info-hover`、`--dsw-alias-state-business-primary`
- **直接引用的 UI 元素**：
  - 聊天视图 ChatView 的 turn 状态文本（dsh-client-ui-conversation·"Deep diving..." 工作状态指示，同一渐变声明中出现 4 次）：`.Md3f7G_turnStatus{background:linear-gradient(90deg, var(--dsw-static-deepseek-500) 0%, var(--dsw-static-deepseek-500) 40%, var(--dsw-static-deepseek-200) 50%, var(--dsw-static-deepseek-500) 60%, var(--dsw-static-deepseek-500) 100%);color:#0000;-webkit-text-fill-color:transparent;background-clip:text}`（dsh-client-ui-conversation/lib/client.js:5452）→ background（渐变主体色）

### `--dsw-static-deepseek-600`
- 值（浅色 / 深色）：`#4868b2` / `#4868b2`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-700-delete`
- 值（浅色 / 深色）：`#2f4c8f` / `#2f4c8f`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-800`
- 值（浅色 / 深色）：`#34415b` / `#34415b`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-business-tertiary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-deepseek-900`
- 值（浅色 / 深色）：`#283142` / `#283142`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-green-100`
- 值（浅色 / 深色）：`#e6faed` / `#e6faed`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-success-tertiary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-green-400`
- 值（浅色 / 深色）：`#4ed17e` / `#4ed17e`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-success-secondary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-green-500`
- 值（浅色 / 深色）：`#22c55e` / `#22c55e`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-success-primary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-green-900`
- 值（浅色 / 深色）：`#233c2c` / `#233c2c`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-success-tertiary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-00`
- 值（浅色 / 深色）：`#fff` / `#fff`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-100`
- 值（浅色 / 深色）：`#f5f5f5` / `#f5f5f5`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-1000`
- 值（浅色 / 深色）：`#000` / `#000`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-150`
- 值（浅色 / 深色）：`#ededed` / `#ededed`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-200`
- 值（浅色 / 深色）：`#e5e5e5` / `#e5e5e5`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-scrollbar-bg-l1`、`--dsw-alias-scrollbar-bg-l2`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-250`
- 值（浅色 / 深色）：`#dcdcdc` / `#dcdcdc`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-300`
- 值（浅色 / 深色）：`#d4d4d4` / `#d4d4d4`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-scrollbar-hover-l1`、`--dsw-alias-scrollbar-hover-l2`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-400`
- 值（浅色 / 深色）：`#a2a4a6` / `#a2a4a6`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-50`
- 值（浅色 / 深色）：`#fafafa` / `#fafafa`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-500`
- 值（浅色 / 深色）：`#7f8287` / `#7f8287`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-550`
- 值（浅色 / 深色）：`#65676b` / `#65676b`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-scrollbar-hover-l2`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-600`
- 值（浅色 / 深色）：`#545557` / `#545557`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-scrollbar-bg-l2`、`--dsw-alias-scrollbar-hover-l1`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-700`
- 值（浅色 / 深色）：`#3c3c3d` / `#3c3c3d`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-scrollbar-bg-l1`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-800`
- 值（浅色 / 深色）：`#292929` / `#292929`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-850`
- 值（浅色 / 深色）：`#212123` / `#212123`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-bg-multi-select`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-900`
- 值（浅色 / 深色）：`#0f0f0f` / `#0f0f0f`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-00`
- 值（浅色 / 深色）：`#fff` / `#fff`（浅深相同）
- 被以下变量定义指向：alias 9 个：`--dsw-alias-bg-base`、`--dsw-alias-bg-layer-1`、`--dsw-alias-bg-layer-2`、`--dsw-alias-bg-layer-3`、`--dsw-alias-button-elevated-fill`、`--dsw-alias-button-floating-fill`、`--dsw-alias-label-primary-foreground`、`--dsw-alias-label-primary-inverted`、`--dsw-alias-markdown-code-segment-selected`；specific 1 个：`--dsw-specific-input-major`
- **直接引用的 UI 元素**：
  - 提示气泡 Tooltip（dsh-web-frontend·dist 构建产物/web shell 通用 Tooltip，`role="tooltip"` 气泡）：`._bubble_owhem_8{position:fixed;z-index:100;...;background:var(--dsw-alias-tooltip-bg);color:var(--dsw-static-neutral-bluish-00);...}`（dsh-web-frontend/dist/assets/index-C6eRlFa6.css:1，**仅 dist**；client.js 中仅 theme 定义行 124，已排除）→ color（tooltip 文字色）

### `--dsw-static-neutral-bluish-100`
- 值（浅色 / 深色）：`#ebeef2` / `#ebeef2`（浅深相同）
- 被以下变量定义指向：alias 6 个：`--dsw-alias-button-ghost-active-fill`、`--dsw-alias-button-primary-dimmed`、`--dsw-alias-button-primary-hover`、`--dsw-alias-label-primary-dimmed`、`--dsw-alias-markdown-citation`、`--dsw-alias-markdown-inline-code`；specific 1 个：`--dsw-specific-sidebar-nav-item-active`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-1000`
- 值（浅色 / 深色）：`#0f1115` / `#0f1115`（浅深相同）
- 被以下变量定义指向：alias 5 个：`--dsw-alias-brand-primary`、`--dsw-alias-brand-primary-invert`、`--dsw-alias-brand-text`、`--dsw-alias-label-primary`、`--dsw-alias-label-primary-foreground`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-150`
- 值（浅色 / 深色）：`#e9ecf2` / `#e9ecf2`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-bg-overlay`、`--dsw-alias-button-ghost-active-hover`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-200`
- 值（浅色 / 深色）：`#e1e5ee` / `#e1e5ee`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-label-dimmed`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-300`
- 值（浅色 / 深色）：`#cfd3d6` / `#cfd3d6`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-label-secondary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-400`
- 值（浅色 / 深色）：`#adb2b8` / `#adb2b8`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-label-caption`、`--dsw-alias-label-tertiary`
- **直接引用的 UI 元素**：
  - 上下文占用仪表盘 ContextMeter（dsh-client-ui-conversation·system 段）：`.JObwrW_colorSystem{--meter-tint:var(--dsw-static-neutral-bluish-400)}`（dsh-client-ui-conversation/lib/client.js:3036）→ --meter-tint（system 段条/图例色块背景，机制同 blue-450）
  - 外观设置行 AppearanceRow（dsh-client-ui-theme·General 设置中的主题/外观选择卡片）：`._8HJdBW_selected{background:var(--dsw-alias-bg-module-platform);border-color:var(--dsw-static-neutral-bluish-400)}`（dsh-client-ui-theme/lib/client.js:26）→ border-color（选中主题色卡的边框）

### `--dsw-static-neutral-bluish-50`
- 值（浅色 / 深色）：`#f9fafb` / `#f9fafb`（浅深相同）
- 被以下变量定义指向：alias 8 个：`--dsw-alias-brand-primary`、`--dsw-alias-brand-primary-invert`、`--dsw-alias-brand-text`、`--dsw-alias-button-contrast-fill`、`--dsw-alias-label-primary`、`--dsw-alias-label-primary-bluish`、`--dsw-alias-markdown-code-block`、`--dsw-alias-markdown-code-block-banner`；specific 2 个：`--dsw-specific-login-input`、`--dsw-specific-sidebar-fill`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-500`
- 值（浅色 / 深色）：`#979da6` / `#979da6`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-button-ghost-active-border`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-60`
- 值（浅色 / 深色）：`#f5f6f7` / `#f9fafb`
- 被以下变量定义指向：alias 3 个：`--dsw-alias-bg-module-platform`、`--dsw-alias-bg-multi-select`、`--dsw-alias-markdown-placeholder`；specific 2 个：`--dsw-specific-selector`、`--dsw-specific-tip`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-600`
- 值（浅色 / 深色）：`#81858c` / `#81858c`（浅深相同）
- 被以下变量定义指向：alias 3 个：`--dsw-alias-button-ghost-active-border`、`--dsw-alias-label-caption`、`--dsw-alias-label-tertiary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-700`
- 值（浅色 / 深色）：`#61666b` / `#61666b`（浅深相同）
- 被以下变量定义指向：alias 4 个：`--dsw-alias-bg-overlay`、`--dsw-alias-button-contrast-fill`、`--dsw-alias-button-ghost-active-hover`、`--dsw-alias-label-secondary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-75`
- 值（浅色 / 深色）：`#f1f3f5` / `#f1f3f5`（浅深相同）
- 被以下变量定义指向：alias 4 个：`--dsw-alias-button-floating-hover`、`--dsw-alias-interactive-bg-hover-solid`、`--dsw-alias-markdown-code-segment-unselected`、`--dsw-alias-markdown-tag`；specific 1 个：`--dsw-specific-sidebar-nav-item-hover`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-750`
- 值（浅色 / 深色）：`#43454a` / `#43454a`（浅深相同）
- 被以下变量定义指向：alias 7 个：`--dsw-alias-button-elevated-fill`、`--dsw-alias-button-ghost-active-fill`、`--dsw-alias-button-primary-dimmed`、`--dsw-alias-button-primary-hover`、`--dsw-alias-label-dimmed`、`--dsw-alias-toast-bg`、`--dsw-alias-tooltip-bg`；specific 2 个：`--dsw-specific-bubble-highlight`、`--dsw-specific-sidebar-nav-item-active`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-800`
- 值（浅色 / 深色）：`#353638` / `#353638`（浅深相同）
- 被以下变量定义指向：alias 8 个：`--dsw-alias-bg-layer-3`、`--dsw-alias-bg-module-platform`、`--dsw-alias-button-floating-hover`、`--dsw-alias-interactive-bg-hover-solid`、`--dsw-alias-label-primary-inverted`、`--dsw-alias-markdown-citation`、`--dsw-alias-markdown-code-segment-selected`、`--dsw-alias-toast-bg`；specific 3 个：`--dsw-specific-selector`、`--dsw-specific-sidebar-nav-item-active-accent`、`--dsw-specific-tip`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-850`
- 值（浅色 / 深色）：`#2c2c2e` / `#2c2c2e`（浅深相同）
- 被以下变量定义指向：alias 7 个：`--dsw-alias-bg-layer-2`、`--dsw-alias-button-floating-fill`、`--dsw-alias-markdown-code-block-banner`、`--dsw-alias-markdown-inline-code`、`--dsw-alias-markdown-placeholder`、`--dsw-alias-markdown-tag`、`--dsw-alias-tooltip-bg`；specific 3 个：`--dsw-specific-bubble`、`--dsw-specific-input-major`、`--dsw-specific-sidebar-nav-item-hover`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-875`
- 值（浅色 / 深色）：`#232324` / `#232324`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-bg-layer-1`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-900`
- 值（浅色 / 深色）：`#1b1b1c` / `#1b1b1c`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-markdown-code-block`、`--dsw-alias-markdown-code-segment-unselected`；specific 2 个：`--dsw-specific-login-input`、`--dsw-specific-sidebar-fill`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-neutral-bluish-950`
- 值（浅色 / 深色）：`#151517` / `#151517`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-bg-base`、`--dsw-alias-label-primary-dimmed`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-red-100`
- 值（浅色 / 深色）：`#fee2e2` / `#fee2e2`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-red-400`
- 值（浅色 / 深色）：`#f25a5a` / `#f25a5a`（浅深相同）
- 被以下变量定义指向：alias 2 个：`--dsw-alias-state-error-primary`、`--dsw-alias-state-error-secondary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-red-50`
- 值（浅色 / 深色）：`#fef2f2` / `#fef2f2`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-red-500`
- 值（浅色 / 深色）：`#ef4444` / `#ef4444`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-red-600`
- 值（浅色 / 深色）：`#ec1313` / `#ec1313`（浅深相同）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-state-error-primary`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-static-red-900`
- 值（浅色 / 深色）：`#570c0c` / `#570c0c`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

## 二、specific 变量（11 个）

> specific 为面向具体界面部位的语义色，大多指向 static；`--dsw-specific-menu` 指向 alias。UI 元素直接使用 specific 时归入本节。

### `--dsw-specific-bubble`
- 值（浅色 / 深色）：var(--dsw-static-deepseek-50) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-deepseek-50`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 用户消息气泡（dsh-client-ui-conversation·gdEzaW 用户消息行）：`.gdEzaW_bubble{background:var(--dsw-specific-bubble);...border-radius:22px;padding:10px 16px}`（父级 `.gdEzaW_userRow/.gdEzaW_userStack`，右对齐、max-width:min(525px,82%)）；dsh-client-ui-conversation/lib/client.js:4254，属性: background
  - 目标内容气泡（dsh-client-ui-goal·oRe1gG 目标行）：`.oRe1gG_bubble{overflow-wrap:anywhere;background:var(--dsw-specific-bubble);...font:var(--dsw-font-markdown-code);border-radius:22px}`（右对齐用户型气泡，代码字体展示目标内容）；dsh-client-ui-goal/lib/client.js:254，属性: background

### `--dsw-specific-bubble-highlight`
- 值（浅色 / 深色）：var(--dsw-static-deepseek-200) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-deepseek-200`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-specific-input-major`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 附件轮播箭头按钮（dsh-client-ui-attachment·JVDQca 附件轮播）：`.JVDQca_arrow{...border:1px solid var(--dsw-alias-border-l2-darkmode-thin);background:var(--dsw-specific-input-major);width:24px;height:24px;...position:absolute;top:50%;transform:translateY(-50%)}`；dsh-client-ui-attachment/lib/client.js:27，属性: background
  - 图片灯箱查看器（dsh-client-ui-attachment·fNh4Da 图片预览）：`.fNh4Da_image{object-fit:contain;background:var(--dsw-specific-input-major);...}` 与 `.fNh4Da_close{...border:1px solid ...;background:var(--dsw-specific-input-major);...}`（父级 `.fNh4Da_backdrop/.fNh4Da_mask`，全屏 fixed 灯箱）；dsh-client-ui-attachment/lib/client.js:382，属性: background（image 画布背景 + close 按钮背景）
  - 合成器输入卡片（dsh-client-ui-conversation·uV2eYG composer）：`.uV2eYG_card{...border:1px solid var(--dsw-alias-border-l2-darkmode-thin);background:var(--dsw-specific-input-major);box-shadow:var(--dsw-shadow-lv2);border-radius:22px;...}`（含 cardWorkspaceTrigger/accessory/modes/tools/trailing/add 等子类，即消息输入合成器主体卡片）；dsh-client-ui-conversation/lib/client.js:3463，属性: background
  - 合成器上方警示条卡片（dsh-client-ui-conversation·bqrRRG）：`.bqrRRG_card{...border:1px solid var(--dsw-alias-state-warn-secondary);background:var(--dsw-specific-input-major);...border-radius:20px}`，配 `_strip{background:var(--dsw-alias-state-warn-tertiary)}`（composer 上方、含 command/dot/headline/actionRow，推断为会话状态/草稿恢复类警示条卡片）；（推断）dsh-client-ui-conversation/lib/client.js:6010，属性: background
  - 用户提问卡片 v1（dsh-client-ui-user-questions·LVzXQa）：`.LVzXQa_card{...border:1px solid var(--dsw-alias-state-warn-secondary);background:var(--dsw-specific-input-major);max-height:min(60vh,520px);border-radius:20px}`（composer 区域提问卡片，含 actions/discuss/feedback/dot/footer/body）；dsh-client-ui-user-questions/lib/client.js:115，属性: background
  - 用户提问卡片 v2（dsh-client-ui-user-questions·Mbwy4a）：`.Mbwy4a_card{...border:1px solid var(--dsw-alias-border-l2-darkmode-thin);background:var(--dsw-specific-input-major);...}`（选项列表式提问卡片，含 optionCopy/optionLine/optionLabel/badge/customRow）；dsh-client-ui-user-questions/lib/client.js:233，属性: background

### `--dsw-specific-login-input`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-50) / var(--dsw-static-neutral-bluish-900)
> 指向：`--dsw-static-neutral-bluish-50`、`--dsw-static-neutral-bluish-900`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-specific-menu`
- 值（浅色 / 深色）：var(--dsw-alias-bg-layer-3) / var(--dsw-alias-bg-layer-3)（浅深相同）
> 指向：`--dsw-alias-bg-layer-3`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 命令面板下拉卡片（dsh-client-ui-commands·mufS8W 命令面板）：`.mufS8W_card{...border:1px solid var(--dsw-alias-border-inverted);background:var(--dsw-specific-menu);...border-radius:12px;position:absolute;bottom:calc(100% + 4px);left:0}`（含 viewport/footer/itemWrap/item 等子类，slash 命令弹出列表）；dsh-client-ui-commands/lib/client.js:875，属性: background
  - 令牌用量仪表弹层（dsh-client-ui-conversation·JObwrW token 用量指示器）：`.JObwrW_panel{...border:1px solid var(--dsw-alias-border-inverted);background:var(--dsw-specific-menu);width:264px;...position:absolute;bottom:calc(100% + 8px);right:0}`（含 _track/_fill 环形进度、_bar/_segment/_colorSystem/_colorTools/_colorMessages 用量分段、_rows 明细，即合成器旁的 token 用量悬浮面板）；dsh-client-ui-conversation/lib/client.js:3036，属性: background
  - Cordis 插件面板（dsh-client-ui-cordis·Nqubda 插件停靠面板）：`.Nqubda_panel{...border:1px solid var(--dsw-alias-border-inverted);background:var(--dsw-specific-menu);width:420px;max-height:60vh;...border-radius:12px}`（父级 `.Nqubda_rail` 带 badge/footerButtons 的侧栏轨道）；dsh-client-ui-cordis/lib/client.js:572，属性: background
  - 输入触发菜单（dsh-client-ui-input-trigger·_3e4SsG）：`._3e4SsG_menu{...border:1px solid var(--dsw-alias-border-inverted);background:var(--dsw-specific-menu);min-width:min(260px,100%);max-height:320px;...position:absolute;bottom:calc(100% + 4px);left:0}`（含 viewport 子类，输入触发条 @/mention 下拉菜单）；dsh-client-ui-input-trigger/lib/client.js:717，属性: background
  - 任务列表下拉菜单（dsh-client-ui-jobs·QsffPG）：`.QsffPG_menu{...border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-specific-menu);width:336px;max-height:min(420px,100vh - 140px);...}`（触发钮 `.QsffPG_trigger` + count/triggerDot，jobs 面板展开菜单）；dsh-client-ui-jobs/lib/client.js:11，属性: background
  - 消息反馈备注面板（dsh-client-ui-message-feedback·_8_XoUG）：`._8_XoUG_notePanel{...border:1px solid var(--dsw-alias-border-inverted);background:var(--dsw-specific-menu);width:320px;max-height:calc(100vh - 24px);...}`（noteOpen 触发按钮，消息反馈备注弹层）；dsh-client-ui-message-feedback/lib/client.js:329，属性: background
  - 模型选择下拉（dsh-client-ui-model-selection·_7KE1Ra）：`._7KE1Ra_menu{...border:1px solid var(--dsw-alias-border-inverted);background:var(--dsw-specific-menu);...max-height:min(360px,100vh - 96px);...}` 与 `._7KE1Ra_groupTitle{...background:var(--dsw-specific-menu);...position:sticky;top:0}`（含 retry/groups/groupTitle/option，模型选择器分组下拉，分组标题吸顶复用 menu 底色）；dsh-client-ui-model-selection/lib/client.js:234，属性: background（menu 本体 + groupTitle 吸顶背景）
  - 子代理祖先切换下拉（dsh-client-ui-subagent·ZKlsPq）：`.ZKlsPq_menu{...background:var(--dsw-specific-menu);width:336px;max-height:min(560px,100vh - 140px);...}`（父级 `_ancestorSwitcherTrigger/_switcherTrigger/_trigger`，子代理祖先切换器菜单）；dsh-client-ui-subagent/lib/client.js:13，属性: background
  - 基础 Menu 组件的列表/子菜单（dsh-web-frontend dist·@deepseek-ai/dsh-client-ui-primitives Menu）：`._list_19372_8,._submenu_19372_9{...border:1px solid var(--dsw-alias-border-inverted);border-radius:12px;background:var(--dsw-specific-menu);box-shadow:var(--dsw-shadow-lv3)}`（dist 导出表 Re={root,list,submenu,portal,item,...}，共享 Menu 原语，工作区等通过 `_deepseek_ai_dsh_client_ui_primitives.Menu` 使用）；仅 dist：dsh-web-frontend/dist/assets/index-C6eRlFa6.css:1，属性: background

### `--dsw-specific-selector`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-60) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-60`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 合成器附加按钮（dsh-client-ui-conversation·uV2eYG composer）：`.uV2eYG_add{background:var(--dsw-specific-selector);width:28px;height:28px;color:var(--dsw-alias-label-primary);cursor:pointer;border:none;border-radius:999px;...}`（`.uV2eYG_tools/.uV2eYG_modes/.uV2eYG_trailing` 工具条中的圆形"添加"按钮）；dsh-client-ui-conversation/lib/client.js:3463，属性: background

### `--dsw-specific-sidebar-fill`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-50) / var(--dsw-static-neutral-bluish-900)
> 指向：`--dsw-static-neutral-bluish-50`、`--dsw-static-neutral-bluish-900`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 布局框架侧栏列（dsh-client-ui-layout·pI_x6G 三栏布局）：`.pI_x6G_sidebarCol{background:var(--dsw-specific-sidebar-fill);border-right:1px solid var(--dsw-alias-border-l1);...}`（`.pI_x6G_frame` 网格内的 sidebarCol 列）；dsh-client-ui-layout/lib/client.js:56，属性: background
  - 侧边栏根容器（dsh-client-ui-sidebar·hHd-Xa）：`.hHd-Xa_root{--dsh-sidebar-inline-padding:12px;...background:var(--dsw-specific-sidebar-fill);...}`（含 collapsed 折叠态，左侧导航侧边栏整体背景）；dsh-client-ui-sidebar/lib/client.js:26，属性: background
  - 轨迹表格表头（dsh-client-ui-trajectory·Y0dWHa 运行轨迹表）：`.Y0dWHa_table th{...border-bottom:1px solid var(--dsw-alias-border-l2);...background:var(--dsw-specific-sidebar-fill);...position:sticky;top:0}`（轨迹表 eventColumn/contentColumn 的吸顶表头单元格）；dsh-client-ui-trajectory/lib/client.js:2995，属性: background
  - 工作区会话列表底部渐隐（dsh-client-ui-workspace·qDHVXG 会话树）：`.qDHVXG_fade{left:0;right:var(--dsh-session-list-edge-inset);background:linear-gradient(to bottom, transparent, var(--dsw-specific-sidebar-fill));...height:24px;position:absolute;bottom:0}`（列表底部 fade 遮罩，渐隐到侧栏底色）；dsh-client-ui-workspace/lib/client.js:969，属性: background（渐变色终点）
  - 主题设置面板颜色项（dsh-client-ui-theme·主题色设置列表）：条目 `{name:"--dsw-specific-sidebar-fill", description:"Sidebar column and title-row background.", valueType:"CSS color", requiresLightAndDark:true, cssVariable:"--dsw-specific-sidebar-fill"}`；dsh-client-ui-theme/lib/client.js:1093（name）与 1097（cssVariable），属性: 设置面板内可自定义主题色条目（使用处）

### `--dsw-specific-sidebar-nav-item-active`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-100) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-neutral-bluish-100`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 设置页导航激活项（dsh-client-ui-settings-general·VOzbGW 设置导航）：`.VOzbGW_navCell.VOzbGW_active{background:var(--dsw-specific-sidebar-nav-item-active)}`（`.VOzbGW_navCell` 导航单元 + `.VOzbGW_active` 激活态，设置面板内左侧导航选中底色）；dsh-client-ui-settings-general/lib/client.js:28，属性: background
  - 注：dsh-client-ui-user-questions/lib/client.js:233 的字符串命中为 `--dsw-specific-sidebar-nav-item-active-accent` 的子串（`grep -o "dsw-specific-sidebar-nav-item-active[^-]"` 验证无独立出现），不计入。

### `--dsw-specific-sidebar-nav-item-active-accent`
- 值（浅色 / 深色）：var(--dsw-static-deepseek-100) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-deepseek-100`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 用户提问选项徽标（dsh-client-ui-user-questions·Mbwy4a 提问选项卡片）：`.Mbwy4a_badge{background:var(--dsw-specific-sidebar-nav-item-active-accent);color:var(--dsw-alias-button-info-fill);border-radius:6px;padding:0 4px;font-size:11px;font-weight:600}`（`_optionLine/_optionLabel/_badge`，选项行上的小徽标，如 agent/技能标记）；（推断）dsh-client-ui-user-questions/lib/client.js:233，属性: background

### `--dsw-specific-sidebar-nav-item-hover`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-75) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-75`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 设置页导航悬停项（dsh-client-ui-settings-general·VOzbGW 设置导航）：`.VOzbGW_navCell:hover{background:var(--dsw-specific-sidebar-nav-item-hover)}`；dsh-client-ui-settings-general/lib/client.js:28，属性: background

### `--dsw-specific-tip`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-60) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-60`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 会话提示/进度面板（dsh-client-ui-conversation·lXshSW）：`.lXshSW_root{...border:1px solid var(--dsw-alias-border-l1);background:var(--dsw-specific-tip);--dsh-scrollbar-thumb:...;border-radius:12px;...}`（含 header/lead/title/progress/chevron/list/item/glyphCompleted/glyphPending/glyphProgress + `lXshSW_todo-progress-spin` 动画，即会话中的 todo/进度提示条）；（推断）dsh-client-ui-conversation/lib/client.js:6473，属性: background
  - 会话提示 Dock 面板（dsh-client-ui-conversation·_7yHdaG）：`._7yHdaG_panel{background:var(--dsw-specific-tip);--dsh-scrollbar-thumb:...;border-radius:12px 12px 0 0;...}`（父级 `._7yHdaG_dock` 位于 composer 底部 dock，含 header/count/chevron/list/row/preview/editor/actions，即底部 dock 提示面板，如引用/草稿列表）；dsh-client-ui-conversation/lib/client.js:6680，属性: background
  - 目标栏（dsh-client-ui-goal·nLMEza）：`.nLMEza_bar{...border:1px solid var(--dsw-alias-border-l1);background:var(--dsw-specific-tip);border-radius:12px;...height:36px;...}`（父级 `.nLMEza_dock`，含 goalGlyph/label/objective/error/objectiveInput/actions，即聊天区顶部的当前目标栏）；dsh-client-ui-goal/lib/client.js:11，属性: background
  - 仅 dist：dsh-web-frontend/dist/assets/index-C6eRlFa6.css:1（`index-ClqxG24t.js`、`vendor-CjyC-hUb.css` 及全部 32 个 client.js 均无命中）。
  - 定义 + 使用的完整选择器上下文（同一 CSS 模块，dist CSS 内相邻类）：
  - 组件推断结论：这是 **@deepseek-ai/dsh-client-ui-primitives 包的 HoverCard 悬浮卡片组件**（dist JS 共享组件导出表 `Kd` 中 `HoverCard:tf`；`function tf({anchor, content, openDelayMs=500, disabled, copyText, copyLabel="复制", copiedLabel="复制成功"})`）。它包裹在锚点元素外的 fixed 定位悬浮卡片（宽 244px，位于锚点右侧 +8px），悬停 500ms 后显示 `content`；当传入 `copyText` 时卡片可点击复制（"复制"/"复制成功" 反馈态由 `_feedback/_copied/_status` 呈现）。
  - 使用方（消费该组件的 UI 元素，dsh-client-ui-workspace）：
  - dsh-client-ui-workspace/lib/client.js:538 —— 工作区选择器行：`HoverCard{anchor: ownRow, content: WorkspaceHoverContent{label, cwd, createdAt, ...}}`，悬停会话行显示名称/路径/创建时间。
  - dsh-client-ui-workspace/lib/client.js:717 —— 会话列表行：`HoverCard{anchor: sessionRow(treeitem), content: SessionHoverContent{node, now, t}, disabled: menuOpen||drag.active, copyText: row.title, copyLabel: t("copy"), copiedLabel: t("hover.copied")}`，悬停显示会话摘要，点击复制会话标题并显示"复制成功"。
  - 注：dsh-client-ui-primitives 包本体不在 BASE 中（构建期依赖，dist 内为编译产物），故该变量只在 dist CSS 出现（"仅 dist"）。

## 三、alias 变量（78 个）

> alias 为全局语义层，绝大多数指向 static，个别指向其他 alias（`--dsw-alias-button-primary-fill` → `--dsw-alias-brand-primary`）。这是 UI 元素引用最多的一层。

### `--dsw-alias-bg-base`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-950)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-950`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 聊天界面·消息行内编辑器 `._7yHdaG_editor`（dsh-client-ui-conversation，输入区内可折叠列表面板的行内编辑框）：`. _7yHdaG_editor{...border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-base)...}`；conversation/lib/client.js:6680，属性: background
  - 聊天界面·聊天主视图根容器 `.wSkVaW_root`（conversation）：`.wSkVaW_root{background:var(--dsw-alias-bg-base);...}`；conversation/lib/client.js:7118，属性: background
  - 聊天界面·输入区停靠渐变遮罩 `.wSkVaW_root[data-phase=active] .wSkVaW_composerSeat`（conversation）：`background:linear-gradient(180deg, color-mix(in srgb, var(--dsw-alias-bg-base) 0%, transparent) 0px, var(--dsw-alias-bg-base) 36px)`；conversation/lib/client.js:7118，属性: background(linear-gradient)
  - 聊天界面·右侧详情面板根容器 `.ydkMvW_root`（conversation）：`.ydkMvW_root{border-left:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-base);...}`；conversation/lib/client.js:7429，属性: background
  - 聊天界面·推理过程行运行扫光 `.QWLzlG_root[data-state=running] .QWLzlG_row:after`（conversation）：`background:linear-gradient(90deg, transparent 0%, color-mix(in srgb, var(--dsw-alias-bg-base) 60%, transparent) 55%, transparent 100%)`；conversation/lib/client.js:9350，属性: background(linear-gradient+color-mix)
  - 聊天界面·命令执行行运行扫光 `._Xvjua_root[data-state=running] ._Xvjua_row:after`（conversation）：同上模式；conversation/lib/client.js:9556，属性: background(linear-gradient+color-mix)
  - cordis 插件面板·业务信息卡片 `.cvtE3a_business`（dsh-client-ui-cordis）：`.cvtE3a_business{border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-base);...}`；cordis/lib/client.js:116，属性: background
  - cordis 插件面板·"检查(inspect)"按钮 `.gNWCoW_inspectButton`（cordis）：`.gNWCoW_inspectButton{border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-base);...}`；cordis/lib/client.js:211，属性: background
  - 目标面板·目标输入框 `.nLMEza_objectiveInput`（dsh-client-ui-goal）：`.nLMEza_objectiveInput{border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-base);...}`；goal/lib/client.js:11，属性: background
  - 布局框架·主 frame `.pI_x6G_frame`（dsh-client-ui-layout）：`.pI_x6G_frame{background:var(--dsw-alias-bg-base);height:100%;...}`；layout/lib/client.js:56，属性: background
  - 技能卡片·运行扫光 `.iWrAna_row[data-state=running]...:after` + "检查"按钮 `.iWrAna_inspectButton`（dsh-client-ui-skill）：扫光 `background:linear-gradient(...var(--dsw-alias-bg-base) 60%...)`；inspect 按钮 `border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-base)`；skill/lib/client.js:11，属性: background / background(linear-gradient+color-mix)
  - 工具调用卡片·工具行扫光 `.o3BgMG_root[data-state=running] .o3BgMG_row:after` + "检查"按钮 `.o3BgMG_inspectButton`（dsh-client-ui-tool）：扫光 `background:linear-gradient(...color-mix(in srgb, var(--dsw-alias-bg-base) 60%, transparent)...)`；inspect 按钮 `border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-base)`；tool/lib/client.js:627，属性: background / background(linear-gradient+color-mix)
  - 工具调用卡片·bash 卡片扫光 `.CY-8Ka_root[data-state=running]:after` + "检查"按钮 `.CY-8Ka_inspectButton`（tool）：同上模式；tool/lib/client.js:1128，属性: background / background(linear-gradient+color-mix)
  - 轨迹界面·面板图片 `.Y0dWHa_panelImage`（dsh-client-ui-trajectory）：`.Y0dWHa_panelImage{border-radius:inherit;background:var(--dsw-alias-bg-base);...}`；trajectory/lib/client.js:2995，属性: background
  - 轨迹界面·工具目录定义区 `.Y0dWHa_toolCatalogDefinition`（trajectory）：`.Y0dWHa_toolCatalogDefinition{background:var(--dsw-alias-bg-base);...}`；trajectory/lib/client.js:2995，属性: background
  - 主题设置面板·主题色选择项（dsh-client-ui-theme）：`name: "--dsw-alias-bg-base"` 与 `cssVariable: "--dsw-alias-bg-base"`；theme/lib/client.js:1009、1013，属性: 设置项键值（非 CSS 属性）
  - （dist 另有 shell 组件命中：启动屏 `._boot_1ionb_3` background、代码块横幅 `._bannerWrap_178r4_21` background-color、markdown 图片 `._image_1r4m5_268` background、全局 body background；因 client.js 已有命中，按规则不记录）

### `--dsw-alias-bg-layer-1`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-875)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-875`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 代理预设·图标按钮 hover `.rtSEdW_iconButton:hover:not(:disabled)` / 次按钮 hover `.rtSEdW_secondaryButton:hover:not(:disabled)` / 表单输入框 `.rtSEdW_input`（dsh-client-ui-agent-preset）：`background:var(--dsw-alias-bg-layer-1)`；agent-preset/lib/client.js:976，属性: background
  - 消息反馈·备注输入框 `._8_XoUG_noteInput`（dsh-client-ui-message-feedback）：`border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-layer-1)`；message-feedback/lib/client.js:329，属性: background
  - 模型设置·输入框/选择框 `.zGbnIq_input`（dsh-client-ui-settings-models）：`background:var(--dsw-alias-bg-layer-1)`；settings-models/lib/client.js:58，属性: background
  - 插件清单·搜索输入框 `.qSYn7G_search input` / 配置标签 `.qSYn7G_configTag`（dsh-client-ui-settings-plugin-inventory）：`background:var(--dsw-alias-bg-layer-1)`；settings-plugin-inventory/lib/client.js:11，属性: background
  - 子代理·提示条 `.XJ7liG_frame`（dsh-client-ui-subagent）：`.XJ7liG_frame{border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-layer-1);...}`；subagent/lib/client.js:682，属性: background
  - 轨迹界面·主分割容器 `.Y0dWHa_split`（trajectory）：`background:var(--dsw-alias-bg-layer-1)`；trajectory/lib/client.js:2995，属性: background
  - 轨迹界面·历史加载条 `.Y0dWHa_historyLoadingBar` / 历史加载按钮 `.Y0dWHa_historyLoadButton`（trajectory）：`background:var(--dsw-alias-bg-layer-1)`；trajectory/lib/client.js:2995，属性: background
  - 轨迹界面·轨迹表格 `.Y0dWHa_table`（trajectory）：`background:var(--dsw-alias-bg-layer-1)`，另有自定义属性 `--trajectory-turn-accent:color-mix(in srgb, var(--dsw-static-blue-500) 22%, var(--dsw-alias-bg-layer-1))`；trajectory/lib/client.js:2995，属性: background / 自定义属性值
  - 轨迹界面·请求边界控制点 `.Y0dWHa_requestBoundaryControl:before`（trajectory）：`box-shadow:0 0 0 2px var(--dsw-alias-bg-layer-1), 0 0 0 3px transparent`；激活态 `.Y0dWHa_requestBoundaryControlActive:hover:before` 等：`background:color-mix(in srgb, var(--dsw-alias-brand-primary-new-colorprimary-new-color) 18%, var(--dsw-alias-bg-layer-1))`；trajectory/lib/client.js:2995，属性: box-shadow / background(color-mix)
  - 轨迹界面·请求边界提示气泡 `.Y0dWHa_requestBoundaryControl:after`（trajectory）：`background:var(--dsw-alias-bg-layer-1)`；trajectory/lib/client.js:2995，属性: background
  - 轨迹界面·提示词 diff 区 `.Y0dWHa_promptDiff` / 行元信息 `.Y0dWHa_promptDiffLinemeta` / 删除行 `.Y0dWHa_promptDiffLineremoved`（trajectory）：`background:var(--dsw-alias-bg-layer-1)` 及 `background:color-mix(in srgb, var(--dsw-alias-state-error-primary) 12%, var(--dsw-alias-bg-layer-1))`；trajectory/lib/client.js:2995，属性: background / background(color-mix)
  - 轨迹界面·角色着色背景（assistant 紫亮 `.Y0dWHa_assistantVioletBright`、子工具琥珀 `.Y0dWHa_subtoolAmber`、错误行 `.Y0dWHa_table tbody tr[data-error=true] .Y0dWHa_turnRail` 等）（trajectory）：多处 `color-mix(in srgb, ... , var(--dsw-alias-bg-layer-1))` 作为混合底色；trajectory/lib/client.js:2995，属性: background(color-mix)
  - 轨迹界面·右侧详情面板 `.Y0dWHa_details` / 详情头 `.Y0dWHa_overviewHeading` / 概览预览 `.Y0dWHa_overviewPreview` / schema 区 `.Y0dWHa_schema` / assistant 输出 `.Y0dWHa_assistantOutput`（trajectory）：`background:var(--dsw-alias-bg-layer-1)`；trajectory/lib/client.js:2995，属性: background
  - 轨迹界面·工具栏 `.fV0t5q_root` / 开关滑块 `.fV0t5q_controlThumb` / 搜索框 focus `.fV0t5q_search:focus-within`（trajectory）：`background:var(--dsw-alias-bg-layer-1)`；trajectory/lib/client.js:5300，属性: background
  - 轨迹界面·时间轴选择遮罩 `._1p9O6q_selectionEdges`（trajectory）：`box-shadow:-100vw 0 0 100vw color-mix(in srgb, var(--dsw-alias-bg-layer-1) 58%, transparent), 100vw 0 0 100vw ...`；trajectory/lib/client.js:5552，属性: box-shadow(color-mix)
  - 轨迹界面·主容器 `.qBU-ya_root`（trajectory）：`background:var(--dsw-alias-bg-layer-1)`；trajectory/lib/client.js:6935，属性: background
  - 主题设置面板·主题色选择项（theme）：`name:/cssVariable: "--dsw-alias-bg-layer-1"`；theme/lib/client.js:1016、1020，属性: 设置项键值

### `--dsw-alias-bg-layer-2`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 代理预设·选中卡片 `.rtSEdW_cardActive` / 代码查看器 `.rtSEdW_viewerCode`（dsh-client-ui-agent-preset）：`background:var(--dsw-alias-bg-layer-2)`；agent-preset/lib/client.js:976，属性: background
  - 目录选择·加载浮标 `.ZuhsRW_loadingFloat`（dsh-client-ui-directory-picker-browse）：`background:var(--dsw-alias-bg-layer-2)`；directory-picker-browse/lib/client.js:27，属性: background
  - 设置-通用·设置对话框面板 `.VOzbGW_panel`（dsh-client-ui-settings-general）：`.VOzbGW_panel{z-index:1;background:var(--dsw-alias-bg-layer-2);...}`；settings-general/lib/client.js:28，属性: background
  - 插件设置·展开卡片 `.YyYd_a_cardOpen`（dsh-client-ui-settings-plugins）：`background:var(--dsw-alias-bg-layer-2)`；settings-plugins/lib/client.js:155，属性: background
  - 轨迹界面·kind 提示气泡 `.Y0dWHa_kindSlot [role=tooltip]`（trajectory）：`border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-layer-2)`；trajectory/lib/client.js:2995，属性: background
  - 轨迹界面·工具栏搜索框 `.fV0t5q_search`（trajectory）：`background:var(--dsw-alias-bg-layer-2)`；trajectory/lib/client.js:5300，属性: background
  - 轨迹界面·时间轴 plot 区 `._1p9O6q_plot` / 更早历史按钮 `._1p9O6q_earlierHistory`（linear-gradient） / 选中 span 描边 `._1p9O6q_span[data-hovered=true]`、`[data-current=true]` box-shadow / assistant 首字延迟色 `--trajectory-assistant-ttft-color:color-mix(...,var(--dsw-alias-bg-layer-2))`（trajectory）：`background:var(--dsw-alias-bg-layer-2)`、`box-shadow:0 0 0 1px var(--dsw-alias-bg-layer-2)...`、自定义属性 color-mix；trajectory/lib/client.js:5552，属性: background / box-shadow / 自定义属性值
  - 主题设置面板·主题色选择项（theme）：`name:/cssVariable: "--dsw-alias-bg-layer-2"`；theme/lib/client.js:1023、1027，属性: 设置项键值

### `--dsw-alias-bg-layer-3`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- 被以下变量定义指向：specific 1 个：`--dsw-specific-menu`
- **直接引用的 UI 元素**：
  - 代理预设·卡片 `.rtSEdW_card`（dsh-client-ui-agent-preset）：`.rtSEdW_card{border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-layer-3);...}`；agent-preset/lib/client.js:976，属性: background
  - 代理预设·坏标签/使用中标签的文字色 `.rtSEdW_brokenBadge`、`.rtSEdW_inUse`、图标按钮 tooltip 文字色 `.rtSEdW_iconButton:after`（agent-preset）：`color:var(--dsw-alias-bg-layer-3)`（作为前景色用于深色底上的文字）；agent-preset/lib/client.js:976，属性: color
  - 插件清单·卡片 `.qSYn7G_card`（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_card{border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-layer-3);...}`；settings-plugin-inventory/lib/client.js:11，属性: background
  - 插件设置·配置输入框 `.At1oFq_input`（dsh-client-ui-settings-plugins）：`background:var(--dsw-alias-bg-layer-3)`；settings-plugins/lib/client.js:13，属性: background
  - 插件设置·插件卡片 `.YyYd_a_card`（settings-plugins）：`background:var(--dsw-alias-bg-layer-3)`；settings-plugins/lib/client.js:155，属性: background
  - 插件设置·保存按钮文字色 `.YyYd_a_save`（settings-plugins）：`background:var(--dsw-alias-label-primary);color:var(--dsw-alias-bg-layer-3)`；settings-plugins/lib/client.js:155，属性: color

### `--dsw-alias-bg-mask-1`
- 值（浅色 / 深色）：`#0000003d` / `#00000080`
- **直接引用的 UI 元素**：
  - 附件·图片预览灯箱遮罩 `.fNh4Da_mask`（dsh-client-ui-attachment）：`.fNh4Da_mask{background:var(--dsw-alias-bg-mask-1);backdrop-filter:var(--dsw-mask-blur);...}`；attachment/lib/client.js:382，属性: background / backdrop-filter
  - 设置-通用·设置对话框遮罩 `.VOzbGW_mask`（dsh-client-ui-settings-general）：`.VOzbGW_mask{background:var(--dsw-alias-bg-mask-1);backdrop-filter:var(--dsw-mask-blur);...}`；settings-general/lib/client.js:28，属性: background / backdrop-filter
  - （dist 另有 shell 通用对话框遮罩 `._mask_15u5s_14` 命中，client.js 已有命中，按规则不记录）

### `--dsw-alias-bg-mask-2`
- 值（浅色 / 深色）：`#0000001f` / `#0003`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-bg-mask-3`
- 值（浅色 / 深色）：`#0000007a` / `#0000007a`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-bg-mask-drop`
- 值（浅色 / 深色）：`#ffffffb3` / `#272730b3`
- **直接引用的 UI 元素**：
  - 附件·拖放上传遮罩 `.BInVoG_mask`（dsh-client-ui-attachment）：`.BInVoG_mask{z-index:1000;pointer-events:none;background-color:var(--dsw-alias-bg-mask-drop);backdrop-filter:blur(10px);...}`；attachment/lib/client.js:196，属性: background-color / backdrop-filter

### `--dsw-alias-bg-mask-photo`
- 值（浅色 / 深色）：`#000000e0` / `#000000e0`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-bg-module-platform`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-60) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-60`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 本地化/语言设置·下拉选择器 `.hVGvvW_selector`（dsh-client-locale）：`background:var(--dsw-alias-bg-module-platform)`；locale/lib/client.js:879，属性: background
  - 代理预设设置·下拉选择器 `._5QVD0a_selector`（dsh-client-ui-agent-preset）：`background:var(--dsw-alias-bg-module-platform)`；agent-preset/lib/client.js:261，属性: background
  - 聊天界面·会话设置行下拉选择器 `.T1PP_q_selector`（dsh-client-ui-conversation）：`background:var(--dsw-alias-bg-module-platform)`；conversation/lib/client.js:4176，属性: background
  - 权限预设·下拉选择器 `.oY77xG_selector`（dsh-client-ui-permission-presets）：`background:var(--dsw-alias-bg-module-platform)`；permission-presets/lib/client.js:34，属性: background
  - 模型选择器·警告条 `._7KE1Ra_warning`（dsh-client-ui-model-selection）：`background:var(--dsw-alias-bg-module-platform)`；model-selection/lib/client.js:234，属性: background
  - 模型设置·编辑器面板 `.zGbnIq_editor` / 添加卡片、设置卡片 `.zGbnIq_addCard,.zGbnIq_setupCard`（dsh-client-ui-settings-models）：`background:var(--dsw-alias-bg-module-platform)`；settings-models/lib/client.js:58，属性: background
  - 插件清单·卡片详情区 `.qSYn7G_cardDetails`（dsh-client-ui-settings-plugin-inventory）：`border-top:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-module-platform)`；settings-plugin-inventory/lib/client.js:11，属性: background
  - 插件设置·徽章 `.At1oFq_badge`（dsh-client-ui-settings-plugins）：`background:var(--dsw-alias-bg-module-platform)`；settings-plugins/lib/client.js:13，属性: background
  - 插件设置·待处理标签 `.YyYd_a_pending`（settings-plugins）：`background:var(--dsw-alias-bg-module-platform)`；settings-plugins/lib/client.js:155，属性: background
  - 轨迹界面·轮次标签 `.Y0dWHa_turnLabel` / 系统中性角色标签 `.Y0dWHa_systemNeutral` / 压缩行 `.Y0dWHa_compacted` / 提示词 diff 行元信息 `.Y0dWHa_promptDiffLinemeta`（dsh-client-ui-trajectory）：`background:var(--dsw-alias-bg-module-platform)`；trajectory/lib/client.js:2995，属性: background
  - 用户提问·自定义答案块 `.Mbwy4a_customBlock`（dsh-client-ui-user-questions）：`border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-bg-module-platform)`；user-questions/lib/client.js:233，属性: background
  - 工作流执行·运行头部 `.DBuyfa_runHeader`（dsh-client-ui-workflow-run）：`.DBuyfa_runHeader{...background:var(--dsw-alias-bg-module-platform);...}`；workflow-run/lib/client.js:12，属性: background
  - 主题设置面板·选中的主题色块 `._8HJdBW_selected`（dsh-client-ui-theme）：`._8HJdBW_selected{background:var(--dsw-alias-bg-module-platform);border-color:var(--dsw-static-neutral-bluish-400)}`；theme/lib/client.js:26，属性: background

### `--dsw-alias-bg-multi-select`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-60) / var(--dsw-static-neutral-850)
> 指向：`--dsw-static-neutral-bluish-60`、`--dsw-static-neutral-850`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-bg-overlay`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-150) / var(--dsw-static-neutral-bluish-700)
> 指向：`--dsw-static-neutral-bluish-150`、`--dsw-static-neutral-bluish-700`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 用户提问·选项序号徽标 `.Mbwy4a_number`（dsh-client-ui-user-questions）：`.Mbwy4a_number{background:var(--dsw-alias-bg-overlay);...}`；user-questions/lib/client.js:233，属性: background
  - 主题设置面板·主题色选择项（dsh-client-ui-theme）：`name:/cssVariable: "--dsw-alias-bg-overlay"`；theme/lib/client.js:1030、1034，属性: 设置项键值

### `--dsw-alias-bg-skeleton`
- 值（浅色 / 深色）：`#0000000a` / `#ffffff14`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-border-inverted`
- 值（浅色 / 深色）：`#0000` / `#ffffff0f`
- **直接引用的 UI 元素**：
  - 命令面板·命令卡片 `.mufS8W_card` / 搜索框 `.mufS8W_search` / 重试按钮 `.mufS8W_retry`（dsh-client-ui-commands）：`border:1px solid var(--dsw-alias-border-inverted)`；commands/lib/client.js:875，属性: border
  - 聊天界面·进度指示面板 `.JObwrW_panel`（dsh-client-ui-conversation）：`.JObwrW_panel{...border:1px solid var(--dsw-alias-border-inverted);background:var(--dsw-specific-menu);...}`；conversation/lib/client.js:3036，属性: border
  - cordis 插件面板·浮层面板 `.Nqubda_panel`（dsh-client-ui-cordis）：`border:1px solid var(--dsw-alias-border-inverted)`；cordis/lib/client.js:572，属性: border
  - 输入触发条·触发菜单 `._3e4SsG_menu`（dsh-client-ui-input-trigger）：`border:1px solid var(--dsw-alias-border-inverted)`；input-trigger/lib/client.js:717，属性: border
  - 消息反馈·备注浮层面板 `._8_XoUG_notePanel`（dsh-client-ui-message-feedback）：`border:1px solid var(--dsw-alias-border-inverted)`；message-feedback/lib/client.js:329，属性: border
  - 模型选择器·下拉菜单 `._7KE1Ra_menu`（dsh-client-ui-model-selection）：`border:1px solid var(--dsw-alias-border-inverted)`；model-selection/lib/client.js:234，属性: border
  - （dist 另有 shell 组件命中：通用菜单 `._list_19372_8,._submenu_19372_9`、通用对话框 `._dialog_15u5s_22`；client.js 已有命中，按规则不记录）

### `--dsw-alias-border-inverted2`
- 值（浅色 / 深色）：`#0000` / `#ffffff14`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-border-l1`
- 值（浅色 / 深色）：`#0000000a` / `#ffffff0f`
- **直接引用的 UI 元素**：
  - 聊天界面·输入区提示条 `.lXshSW_root`（dsh-client-ui-conversation）：`.lXshSW_root{...border:1px solid var(--dsw-alias-border-l1);background:var(--dsw-specific-tip);...}`；conversation/lib/client.js:6473，属性: border
  - 聊天界面·行内编辑面板描边 `._7yHdaG_panel:after`（conversation）：`border:1px solid var(--dsw-alias-border-l1)`；行间分隔 `._7yHdaG_row+._7yHdaG_row`：`box-shadow:inset 0 1px 0 var(--dsw-alias-border-l1)`；conversation/lib/client.js:6680，属性: border / box-shadow(inset)
  - 聊天界面·命令执行行正文 `._Xvjua_body`（conversation）：`border:1px solid var(--dsw-alias-border-l1)`；conversation/lib/client.js:9556，属性: border
  - cordis 插件面板·输出代码块 `.gNWCoW_output`（dsh-client-ui-cordis）：`border:1px solid var(--dsw-alias-border-l1)`；cordis/lib/client.js:211，属性: border
  - 目标面板·目标输入条 `.nLMEza_bar`（dsh-client-ui-goal）：`.nLMEza_bar{...border:1px solid var(--dsw-alias-border-l1);background:var(--dsw-specific-tip);...}`；goal/lib/client.js:11，属性: border
  - 布局框架·侧栏分隔 `.pI_x6G_sidebarCol`（dsh-client-ui-layout）：`border-right:1px solid var(--dsw-alias-border-l1)`；layout/lib/client.js:56，属性: border-right
  - 插件清单·展开卡片边框色 `.qSYn7G_card[data-open=true]`（dsh-client-ui-settings-plugin-inventory）：`border-color:var(--dsw-alias-border-l1)`；settings-plugin-inventory/lib/client.js:11，属性: border-color
  - 技能卡片·说明卡片 `.iWrAna_instructionsCard`（dsh-client-ui-skill）：`border:1px solid var(--dsw-alias-border-l1)`；skill/lib/client.js:11，属性: border
  - 工具调用卡片·IO 卡片 `.o3BgMG_ioCard` / 终端框 `.o3BgMG_terminalBody`（dsh-client-ui-tool）：`border:1px solid var(--dsw-alias-border-l1)`；tool/lib/client.js:627，属性: border
  - 工具调用卡片·bash 终端 `.CY-8Ka_terminal` / IO 卡片 `.CY-8Ka_ioCard`（tool）：`border:1px solid var(--dsw-alias-border-l1)`；tool/lib/client.js:1128，属性: border
  - 轨迹界面·表格行下边框 `.Y0dWHa_table td`（trajectory）：`border-bottom:1px solid var(--dsw-alias-border-l1)`；轮次起始分隔线 `tr[data-turn-start=true]:not(:first-child) td:before`：`background:var(--dsw-alias-border-l1)`；工具目录项 `.Y0dWHa_toolCatalogItem`：`border-bottom:1px solid var(--dsw-alias-border-l1)`；请求边界提示气泡 `.Y0dWHa_requestBoundaryControl:after`：`border:1px solid var(--dsw-alias-border-l1)`；trajectory/lib/client.js:2995，属性: border-bottom / border / background
  - 轨迹界面·时间轴标签分隔 `._1p9O6q_labels`（trajectory）：`border-right:1px solid var(--dsw-alias-border-l1)`；trajectory/lib/client.js:5552，属性: border-right
  - 主题设置面板·主题色选择项（dsh-client-ui-theme）：`name:/cssVariable: "--dsw-alias-border-l1"`；theme/lib/client.js:1037、1041，属性: 设置项键值

### `--dsw-alias-border-l2`
- 值（浅色 / 深色）：`#0000001a` / `#ffffff1f`
- **直接引用的 UI 元素**：
  - 本地化/语言设置·设置行分隔 `.hVGvvW_row`（dsh-client-locale）：`border-bottom:1px solid var(--dsw-alias-border-l2)`；locale/lib/client.js:879，属性: border-bottom
  - 代理预设·设置行分隔 `._5QVD0a_row`（dsh-client-ui-agent-preset）：`border-bottom:1px solid var(--dsw-alias-border-l2)`；agent-preset/lib/client.js:261，属性: border-bottom
  - 代理预设·卡片 `.rtSEdW_card` / 徽章 `.rtSEdW_badge` / 卡片脚 `.rtSEdW_cardFoot` / 表单输入框 `.rtSEdW_input` / 代码查看器 `.rtSEdW_viewerCode`（agent-preset）：`border:1px solid var(--dsw-alias-border-l2)`、`border-top:1px solid ...`；agent-preset/lib/client.js:976，属性: border / border-top
  - 聊天界面·会话设置行分隔 `.T1PP_q_row`（dsh-client-ui-conversation）：`border-bottom:1px solid var(--dsw-alias-border-l2)`；conversation/lib/client.js:4176，属性: border-bottom
  - 聊天界面·"回到底部"浮动按钮 `.Md3f7G_toBottom`（conversation）：`border:1px solid var(--dsw-alias-border-l2)`；conversation/lib/client.js:5452，属性: border
  - 聊天界面·行内编辑器 `._7yHdaG_editor`（conversation）：`border:1px solid var(--dsw-alias-border-l2)`；conversation/lib/client.js:6680，属性: border
  - 聊天界面·模态输入框 `.pXSMma_modalInput`（conversation）：`border:1px solid var(--dsw-alias-border-l2)`；conversation/lib/client.js:6949，属性: border
  - 聊天界面·主视图头部分隔线 `.wSkVaW_header:after`（conversation）：`background:var(--dsw-alias-border-l2);height:1px`；conversation/lib/client.js:7118，属性: background
  - 聊天界面·右侧详情面板 `.ydkMvW_root`（border-left）与头部 `.ydkMvW_header`（border-bottom）（conversation）：`border-left:1px solid var(--dsw-alias-border-l2)` / `border-bottom:1px solid ...`；conversation/lib/client.js:7429，属性: border-left / border-bottom
  - cordis 插件面板·业务卡片 `.cvtE3a_business` / 输出块 `.cvtE3a_output`（dsh-client-ui-cordis）：`border:1px solid var(--dsw-alias-border-l2)`；cordis/lib/client.js:116，属性: border
  - cordis 插件面板·"检查"按钮 `.gNWCoW_inspectButton` / 源码标签页底边 `.gNWCoW_sourceTabs`（cordis）：`border:1px solid ...` / `border-bottom:1px solid ...`；cordis/lib/client.js:211，属性: border / border-bottom
  - cordis 插件面板·插件行 `.Nqubda_row` / 版本选择器 `select` / 转换操作按钮 `.Nqubda_transitionActions button`（cordis）：`border:1px solid var(--dsw-alias-border-l2)`；cordis/lib/client.js:572，属性: border
  - 目录选择·面包屑激活边框 `.ZuhsRW_crumbBar:has(.ZuhsRW_crumbEditZone:enabled:hover)` 等 / 创建输入框 `.ZuhsRW_createInput`（dsh-client-ui-directory-picker-browse）：`border-color:var(--dsw-alias-border-l2)` / `border:1px solid ...`；directory-picker-browse/lib/client.js:27，属性: border / border-color
  - 目标面板·目标输入框 `.nLMEza_objectiveInput`（dsh-client-ui-goal）：`border:1px solid var(--dsw-alias-border-l2)`；goal/lib/client.js:11，属性: border
  - 任务列表·任务菜单 `.QsffPG_menu`（dsh-client-ui-jobs）：`border:1px solid var(--dsw-alias-border-l2)`；jobs/lib/client.js:11，属性: border
  - 布局框架·详情栏分隔 `.pI_x6G_detailsCol`（dsh-client-ui-layout）：`border-left:1px solid var(--dsw-alias-border-l2)`；layout/lib/client.js:56，属性: border-left
  - 消息反馈·备注输入框 `._8_XoUG_noteInput`（dsh-client-ui-message-feedback）：`border:1px solid var(--dsw-alias-border-l2)`；message-feedback/lib/client.js:329，属性: border
  - 权限预设·设置行分隔 `.oY77xG_row`（dsh-client-ui-permission-presets）：`border-bottom:1px solid var(--dsw-alias-border-l2)`；permission-presets/lib/client.js:34，属性: border-bottom
  - 模型设置·行卡片 `.zGbnIq_rowCard` / 次按钮 `.zGbnIq_secondaryButton` / 自定义区顶边 `.zGbnIq_customized` / 模型目录顶边 `.zGbnIq_modelCatalog` / 模型条目 `.zGbnIq_modelEntry` / 添加模型按钮 `.zGbnIq_addModelButton` / 输入框 `.zGbnIq_input`（dsh-client-ui-settings-models）：`border:1px solid ...`、`border-top:1px solid ...`；settings-models/lib/client.js:58，属性: border / border-top
  - 插件清单·失败重试按钮 `.qSYn7G_failure button` / 搜索输入 `.qSYn7G_search input` / 卡片 `.qSYn7G_card` / 卡片详情顶边 `.qSYn7G_cardDetails`（dsh-client-ui-settings-plugin-inventory）：`border:1px solid ...`、`border-top:1px solid ...`；settings-plugin-inventory/lib/client.js:11，属性: border / border-top
  - 插件设置·字段分隔 `.At1oFq_field+.At1oFq_field` / 输入框 `.At1oFq_input`（dsh-client-ui-settings-plugins）：`border-top:1px solid ...` / `border:1px solid ...`；settings-plugins/lib/client.js:13，属性: border / border-top
  - 插件设置·插件卡片 `.YyYd_a_card` / 展开体顶边 `.YyYd_a_body` / 卡片脚 `.YyYd_a_footer` / 放弃按钮 `.YyYd_a_discard`（settings-plugins）：`border:1px solid ...`、`border-top:1px solid ...`；settings-plugins/lib/client.js:155，属性: border / border-top
  - 插件设置·标签页底边 `.pbvGtq_tabs`（settings-plugins）：`border-bottom:1px solid var(--dsw-alias-border-l2)`；settings-plugins/lib/client.js:364，属性: border-bottom
  - 侧边栏·新建会话按钮 `.hHd-Xa_newSession`（dsh-client-ui-sidebar）：`border:1px solid var(--dsw-alias-border-l2)`；sidebar/lib/client.js:26，属性: border
  - 技能卡片·说明头底边 `.iWrAna_instructionsHeader` / "检查"按钮 `.iWrAna_inspectButton`（dsh-client-ui-skill）：`border-bottom:1px solid ...` / `border:1px solid ...`；skill/lib/client.js:11，属性: border / border-bottom
  - 子代理·树形连线 `.ZKlsPq_children:before`、`.ZKlsPq_children>.ZKlsPq_node:before`（border-left）、`.ZKlsPq_children>.ZKlsPq_node>.ZKlsPq_row:before`（border-top）（dsh-client-ui-subagent）：`border-left:1px solid var(--dsw-alias-border-l2)` / `border-top:1px solid ...`；subagent/lib/client.js:13，属性: border-left / border-top
  - 子代理·提示条 `.XJ7liG_frame`（subagent）：`border:1px solid var(--dsw-alias-border-l2)`；subagent/lib/client.js:682，属性: border
  - 工具调用卡片·"检查"按钮 `.o3BgMG_inspectButton` / IO 分隔 `.o3BgMG_ioDivider`（dsh-client-ui-tool）：`border:1px solid ...` / `background:var(--dsw-alias-border-l2)`；tool/lib/client.js:627，属性: border / background
  - 工具调用卡片·子调用列表 `.ztWv_q_subCalls`（tool）：`border-left:1px solid var(--dsw-alias-border-l2)`；tool/lib/client.js:872，属性: border-left
  - 工具调用卡片·bash "检查"按钮 `.CY-8Ka_inspectButton` / IO 分隔 `.CY-8Ka_ioDivider`（tool）：同上；tool/lib/client.js:1128，属性: border / background
  - 轨迹界面·历史加载条 `.Y0dWHa_historyLoadingBar`（border-bottom）/ 加载 spinner `.Y0dWHa_historyLoadingSpinner`（border）/ 表头 `.Y0dWHa_table th`（border-bottom）/ kind 提示气泡 `.Y0dWHa_kindSlot [role=tooltip]`（border）/ 详情面板 `.Y0dWHa_details`（border-left）/ 详情头 `.Y0dWHa_detailsHeader`（border-bottom）/ 详情标签页 `.Y0dWHa_detailTabs`（border-bottom）（dsh-client-ui-trajectory）：trajectory/lib/client.js:2995，属性: border / border-bottom / border-left
  - 轨迹界面·工具栏 `.fV0t5q_root`（border-bottom）/ 开关轨道 `.fV0t5q_controlTrack`（background）/ 搜索框 `.fV0t5q_search`（border）（trajectory）：trajectory/lib/client.js:5300，属性: border / border-bottom / background
  - 轨迹界面·时间轴根 `._1p9O6q_root`（border-bottom）/ 更早历史按钮 focus `._1p9O6q_earlierHistory:focus-visible`（box-shadow inset）/ 轮次边界线 `._1p9O6q_turnBoundary`（background）（trajectory）：trajectory/lib/client.js:5552，属性: border-bottom / box-shadow / background
  - 用户提问·选中选项边框 `.Mbwy4a_optionSelected`、`.Mbwy4a_customRow:focus-within`（border-color）/ 自定义答案块 `.Mbwy4a_customBlock`（border）（dsh-client-ui-user-questions）：user-questions/lib/client.js:233，属性: border-color / border
  - 工作区·会话重命名输入 `.YDXeBa_renameInput`（dsh-client-ui-workspace）：`border:1px solid var(--dsw-alias-border-l2)`；workspace/lib/client.js:334，属性: border
  - 工作区·搜索展开框 `.qDHVXG_searchExpanded` / 重命名输入 `.qDHVXG_renameInput`（workspace）：`border:1px solid var(--dsw-alias-border-l2)`；workspace/lib/client.js:969，属性: border
  - 会话导出·导出按钮 `.nL4_yW_sessionLogButton`（dsh-session-log-export）：`border:1px solid var(--dsw-alias-border-l2)`；session-log-export/lib/client.js:172，属性: border
  - 主题设置面板·面板样式（dsh-client-ui-theme）：分组底边 `._8HJdBW_group{border-bottom:1px solid var(--dsw-alias-border-l2);...}`、主题色块边框 `._8HJdBW_themeCube{...border:1px solid var(--dsw-alias-border-l2)...}`；theme/lib/client.js:26，属性: border-bottom / border
  - 主题设置面板·主题色选择项（theme）：`name:/cssVariable: "--dsw-alias-border-l2"`；theme/lib/client.js:1044、1048，属性: 设置项键值
  - （dist 另有 shell 组件命中：启动 spinner `._spinner_1ionb_47`、outline 按钮 `._outline_kz6gm_56`、搜索框 `._wrap_1ao1y_1`、菜单脚 `._footer_19372_63`、终端块头 `._header_10eou_38`、markdown 分隔线 `._markdown_1r4m5_5 hr`、表格单元格 `._tableScroll_1r4m5_174 td`；client.js 已有命中，按规则不记录）

### `--dsw-alias-border-l2-darkmode-thin`
- 值（浅色 / 深色）：`#0000001a` / `#ffffff0f`
- **直接引用的 UI 元素**：
  - 附件·缩略图帧 `.JVDQca_thumbnail` / 左右箭头按钮 `.JVDQca_arrow`（dsh-client-ui-attachment）：`border:1px solid var(--dsw-alias-border-l2-darkmode-thin)`；attachment/lib/client.js:27，属性: border
  - 附件·图片预览灯箱关闭按钮 `.fNh4Da_close`（attachment）：`border:1px solid var(--dsw-alias-border-l2-darkmode-thin)`；attachment/lib/client.js:382，属性: border
  - 附件·消息内附件画廊帧 `.R_Yw7q_frame` / 错误块 `.R_Yw7q_error`（attachment）：`border:1px solid var(--dsw-alias-border-l2-darkmode-thin)`；attachment/lib/client.js:618，属性: border
  - 聊天界面·输入区（composer）主卡片 `.uV2eYG_card`（dsh-client-ui-conversation）：`.uV2eYG_card{...border:1px solid var(--dsw-alias-border-l2-darkmode-thin);background:var(--dsw-specific-input-major);...}`；conversation/lib/client.js:3463，属性: border
  - 布局框架·拖拽把手浮标 `.pI_x6G_handle[data-side=details]:after`（dsh-client-ui-layout）：`border:1px solid var(--dsw-alias-border-l2-darkmode-thin)`；layout/lib/client.js:56，属性: border
  - 用户提问·选项卡片 `.Mbwy4a_card`（dsh-client-ui-user-questions）：`border:1px solid var(--dsw-alias-border-l2-darkmode-thin)`；user-questions/lib/client.js:233，属性: border

### `--dsw-alias-border-l3`
- 值（浅色 / 深色）：`#0000001f` / `#ffffff29`
- **直接引用的 UI 元素**：
  - 代理预设·新建按钮虚线框 `.rtSEdW_creatorButton`（dsh-client-ui-agent-preset）：`border:1px dashed var(--dsw-alias-border-l3)`；agent-preset/lib/client.js:976，属性: border(dashed)
  - 聊天界面·进度环轨道 `.JObwrW_track`（dsh-client-ui-conversation）：`stroke:var(--dsw-alias-border-l3)`（SVG）；conversation/lib/client.js:3036，属性: stroke
  - 聊天界面·下拉触发按钮 focus `.Sh0Q9G_trigger:focus-visible`（conversation）：`box-shadow:0 0 0 2px var(--dsw-alias-border-l3)`；conversation/lib/client.js:3224，属性: box-shadow
  - 交付物·文件行/显示文件夹 focus `.P4kPIW_file:focus-visible,.P4kPIW_showFolder:focus-visible`（dsh-client-ui-deliverables）：`box-shadow:inset 0 0 0 2px var(--dsw-alias-border-l3)`；deliverables/lib/client.js:160，属性: box-shadow(inset)
  - 目录选择·头部底边 `.ZuhsRW_header` / 列分隔线 `.ZuhsRW_divider` / 底部栏顶边 `.ZuhsRW_footerBar`（dsh-client-ui-directory-picker-browse）：`border-bottom:1px solid ...` / `background:var(--dsw-alias-border-l3)` / `border-top:1px solid ...`；directory-picker-browse/lib/client.js:27，属性: border-bottom / background / border-top
  - 布局框架·拖拽把手 hover 边框色 `.pI_x6G_handle[data-side=details]:hover:after`（dsh-client-ui-layout）：`border-color:var(--dsw-alias-border-l3)`；layout/lib/client.js:56，属性: border-color
  - 模型选择器·触发按钮 focus `._7KE1Ra_trigger:focus-visible`（dsh-client-ui-model-selection）：`box-shadow:0 0 0 2px var(--dsw-alias-border-l3)`；model-selection/lib/client.js:234，属性: box-shadow
  - 模型设置·行标签 `.zGbnIq_rowTag`（border）/ 按钮组 focus（box-shadow）/ 虚线添加按钮 `.zGbnIq_addButton`（border dashed）/ 空态框 `.zGbnIq_modelEmpty`（border dashed）（dsh-client-ui-settings-models）：settings-models/lib/client.js:58，属性: border / box-shadow
  - 轨迹界面·移动端详情面板边框色 `.Y0dWHa_details`（trajectory，@media width<=760px）：`border-left-color:var(--dsw-alias-border-l3)`；trajectory/lib/client.js:2995，属性: border-left-color
  - （dist 另有 shell markdown 表格表头 `._tableScroll_1r4m5_174 th` border-bottom 命中；client.js 已有命中，按规则不记录）

### `--dsw-alias-border-l4`
- 值（浅色 / 深色）：`#00000029` / `#fff3`
- **直接引用的 UI 元素**：
  - 聊天界面·输入区·工作区入口卡片虚线描边 `.uV2eYG_cardWorkspaceTrigger:after`（dsh-client-ui-conversation）：`background:var(--dsw-alias-border-l4)`（配合 -webkit-mask 形成描边效果）；conversation/lib/client.js:3463，属性: background
  - 用户提问·复选框中框 `.Mbwy4a_checkbox:before`（dsh-client-ui-user-questions）：`border:1px solid var(--dsw-alias-border-l4)`；user-questions/lib/client.js:233，属性: border
  - （dist 另有 shell 确认对话框勾选框 focus `._acknowledgement_1nu42_38 input:focus-visible` outline 命中；client.js 已有命中，按规则不记录）

### `--dsw-alias-brand-primary`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-1000) / var(--dsw-static-neutral-bluish-50)
> 指向：`--dsw-static-neutral-bluish-1000`、`--dsw-static-neutral-bluish-50`（浅深分别见上）
- 被以下变量定义指向：alias 1 个：`--dsw-alias-button-primary-fill`
- **直接引用的 UI 元素**：
  - 代理预设·卡片主体 focus `.rtSEdW_cardMain:focus-visible`（outline）/ 图标按钮 focus `.rtSEdW_iconButton:focus-visible`（outline）/ 输入框 focus `.rtSEdW_input:focus`（border-color）（dsh-client-ui-agent-preset）：agent-preset/lib/client.js:976，属性: outline / border-color
  - 模型设置·输入框 focus `.zGbnIq_input:focus`（dsh-client-ui-settings-models）：`border-color:var(--dsw-alias-brand-primary)`；settings-models/lib/client.js:58，属性: border-color
  - 插件设置·输入框 focus `.At1oFq_input:focus-visible`（border-color）/ 卡片头 focus `.YyYd_a_header:focus-visible`（outline）/ 按钮 focus `.YyYd_a_discard:focus-visible,.YyYd_a_save:focus-visible`（outline）（dsh-client-ui-settings-plugins）：settings-plugins/lib/client.js:13、155，属性: border-color / outline
  - 主题设置面板·主题色选择项（dsh-client-ui-theme）：`name:/cssVariable: "--dsw-alias-brand-primary"`；theme/lib/client.js:1051、1055，属性: 设置项键值
  - （dist 另有 shell 组件命中：启动 spinner 弧 `._spinner_1ionb_47:after` conic-gradient、搜索框 focus `._wrap_1ao1y_1:focus-within` border-color；client.js 已有命中，按规则不记录）

### `--dsw-alias-brand-primary-invert`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-1000) / var(--dsw-static-neutral-bluish-50)
> 指向：`--dsw-static-neutral-bluish-1000`、`--dsw-static-neutral-bluish-50`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-brand-primary-new-colorprimary-new-color`
- 值（浅色 / 深色）：`#4176e6` / var(--dsw-static-deepseek-450)
> 指向：`--dsw-static-deepseek-450`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 轨迹界面·请求边界控制点激活/悬停 `.Y0dWHa_requestBoundaryControl:hover:before`（background）/ 激活点 `.Y0dWHa_requestBoundaryControlActive:before`（background color-mix 18% + box-shadow 1.5px 环）（dsh-client-ui-trajectory）：trajectory/lib/client.js:2995，属性: background / box-shadow / background(color-mix)
  - 轨迹界面·轮次轨/选择轨 `.Y0dWHa_turnRail,.Y0dWHa_selectionRail`（trajectory）：`background:var(--dsw-alias-brand-primary-new-colorprimary-new-color)`；trajectory/lib/client.js:2995，属性: background
  - 轨迹界面·assistant 紫亮角色色 `.Y0dWHa_assistantVioletBright`（trajectory）：`color:color-mix(in srgb, var(--dsw-alias-brand-primary-new-colorprimary-new-color) 60%, var(--dsw-alias-state-error-secondary));background:color-mix(in srgb, color-mix(in srgb, ...55%...) 15%, var(--dsw-alias-bg-layer-1))`；trajectory/lib/client.js:2995，属性: color / background(color-mix)
  - 轨迹界面·时间轴消息段 `._1p9O6q_span[data-timeline-span=message]`（trajectory）：自定义属性 `--trajectory-assistant-decoding-color:color-mix(in srgb, var(--dsw-alias-brand-primary-new-colorprimary-new-color) 60%, var(--dsw-alias-state-error-secondary))`；trajectory/lib/client.js:5552，属性: 自定义属性值(color-mix)

### `--dsw-alias-brand-text`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-1000) / var(--dsw-static-neutral-bluish-50)
> 指向：`--dsw-static-neutral-bluish-1000`、`--dsw-static-neutral-bluish-50`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-button-contrast-fill`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-700) / var(--dsw-static-neutral-bluish-50)
> 指向：`--dsw-static-neutral-bluish-700`、`--dsw-static-neutral-bluish-50`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 附件·缩略图删除按钮 `.JVDQca_remove`（dsh-client-ui-attachment）：`.JVDQca_remove{z-index:1;background:var(--dsw-alias-button-contrast-fill);...color:var(--dsw-alias-label-primary-inverted)...}`；attachment/lib/client.js:27，属性: background
  - （dist 另有 shell Toast `_toast_fvpz7_1` background 命中；client.js 已有命中，按规则不记录）

### `--dsw-alias-button-elevated-fill`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 侧边栏·新建会话按钮 `.hHd-Xa_newSession`（dsh-client-ui-sidebar）：`border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-button-elevated-fill)`；sidebar/lib/client.js:26，属性: background
  - 工作区·会话重命名输入 `.YDXeBa_renameInput`（dsh-client-ui-workspace）：`border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-button-elevated-fill)`；workspace/lib/client.js:334，属性: background

### `--dsw-alias-button-floating-fill`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 聊天界面·"回到底部"浮动按钮 `.Md3f7G_toBottom`（dsh-client-ui-conversation）：`border:1px solid var(--dsw-alias-border-l2);background:var(--dsw-alias-button-floating-fill)`；conversation/lib/client.js:5452，属性: background
  - 布局框架·拖拽把手浮标 `.pI_x6G_handle[data-side=details]:after`（dsh-client-ui-layout）：`background:var(--dsw-alias-button-floating-fill);border:1px solid var(--dsw-alias-border-l2-darkmode-thin)`；layout/lib/client.js:56，属性: background

### `--dsw-alias-button-floating-hover`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-75) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-75`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 聊天界面·"回到底部"按钮 hover `.Md3f7G_toBottom:hover`（dsh-client-ui-conversation）：`background:var(--dsw-alias-button-floating-hover)`；conversation/lib/client.js:5452，属性: background
  - 布局框架·拖拽把手 hover/拖拽中 `.pI_x6G_handle[data-side=details]:hover:after`（dsh-client-ui-layout）：`background:var(--dsw-alias-button-floating-hover)`；layout/lib/client.js:56，属性: background
  - 侧边栏·新建会话按钮 hover `.hHd-Xa_newSession:hover`（dsh-client-ui-sidebar）：`background:var(--dsw-alias-button-floating-hover)`；sidebar/lib/client.js:26，属性: background

### `--dsw-alias-button-ghost-active-border`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-500) / var(--dsw-static-neutral-bluish-600)
> 指向：`--dsw-static-neutral-bluish-500`、`--dsw-static-neutral-bluish-600`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 仅 dist：web-shell 分段/胶囊按钮（Pill）激活态 `._active_e3ygd_23`（dsh-web-frontend/dist/assets/index-C6eRlFa6.css:1）：`box-shadow:inset 0 0 0 1px var(--dsw-alias-button-ghost-active-border)`，属性: box-shadow(inset)。所有 client.js 均无该变量的使用命中（theme 仅定义行），故按规则记录 dist。

### `--dsw-alias-button-ghost-active-fill`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-100) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-neutral-bluish-100`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：
  - cordis 插件面板·消息块 `.cvtE3a_message`（dsh-client-ui-cordis）：`background:var(--dsw-alias-button-ghost-active-fill)`；cordis/lib/client.js:116，属性: background
  - cordis 插件面板·插件状态标签 `.Nqubda_rowStatus`（含 idle 等状态变体，cordis）：`background:var(--dsw-alias-button-ghost-active-fill)`；cordis/lib/client.js:572，属性: background
  - （dist 另有 shell Pill 激活态 `._active_e3ygd_23` background 命中；client.js 已有命中，按规则不记录）

### `--dsw-alias-button-ghost-active-hover`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-150) / var(--dsw-static-neutral-bluish-700)
> 指向：`--dsw-static-neutral-bluish-150`、`--dsw-static-neutral-bluish-700`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-button-info-fill`
- 值（浅色 / 深色）：var(--dsw-static-deepseek-500) / var(--dsw-static-deepseek-400)
> 指向：`--dsw-static-deepseek-500`、`--dsw-static-deepseek-400`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 聊天界面·输入区工具行·信息（i）按钮 `.uV2eYG_primary`（dsh-client-ui-conversation）：`background:var(--dsw-alias-button-info-fill);color:#fff`；conversation/lib/client.js:3463，属性: background
  - 聊天界面·重试摘要 focus `.gdEzaW_retrySummary:focus-visible`（conversation）：`outline:1.5px solid var(--dsw-alias-button-info-fill)`；conversation/lib/client.js:4254，属性: outline
  - 目录选择·选中行图标色 `.ZuhsRW_rowIconSelected`（dsh-client-ui-directory-picker-browse）：`color:var(--dsw-alias-button-info-fill)`；directory-picker-browse/lib/client.js:27，属性: color
  - 用户提问·徽章文字色 `.Mbwy4a_badge`（dsh-client-ui-user-questions）：`color:var(--dsw-alias-button-info-fill)`；user-questions/lib/client.js:233，属性: color

### `--dsw-alias-button-info-hover`
- 值（浅色 / 深色）：var(--dsw-static-deepseek-400) / var(--dsw-static-deepseek-500)
> 指向：`--dsw-static-deepseek-400`、`--dsw-static-deepseek-500`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 聊天界面·输入区工具行·信息按钮 hover `.uV2eYG_primary:hover:not(:disabled)`（dsh-client-ui-conversation）：`background:var(--dsw-alias-button-info-hover)`；conversation/lib/client.js:3463，属性: background

### `--dsw-alias-button-primary-dimmed`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-100) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-neutral-bluish-100`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-button-primary-fill`
- 值（浅色 / 深色）：var(--dsw-alias-brand-primary) / var(--dsw-alias-brand-primary)（浅深相同）
> 指向：`--dsw-alias-brand-primary`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 消息反馈·备注保存按钮 `._8_XoUG_noteSave`（dsh-client-ui-message-feedback）：`background:var(--dsw-alias-button-primary-fill);color:var(--dsw-alias-label-primary-foreground)`；message-feedback/lib/client.js:329，属性: background
  - 模型设置·主按钮 `.zGbnIq_primaryButton`（dsh-client-ui-settings-models）：`background:var(--dsw-alias-button-primary-fill);color:var(--dsw-alias-label-primary-foreground)`；settings-models/lib/client.js:58，属性: background
  - （dist 另有 shell Button primary 变体 `._primary_kz6gm_38` background、确认对话框勾选框 `._acknowledgement_1nu42_38 input` accent-color 命中；client.js 已有命中，按规则不记录）

### `--dsw-alias-button-primary-hover`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-750) / var(--dsw-static-neutral-bluish-100)
> 指向：`--dsw-static-neutral-bluish-750`、`--dsw-static-neutral-bluish-100`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 消息反馈·备注保存按钮 hover `._8_XoUG_noteSave:hover:not(:disabled)`（dsh-client-ui-message-feedback）：`background:var(--dsw-alias-button-primary-hover)`；message-feedback/lib/client.js:329，属性: background
  - 模型设置·主按钮 hover `.zGbnIq_primaryButton:hover:not(:disabled)`（dsh-client-ui-settings-models）：`background:var(--dsw-alias-button-primary-hover)`；settings-models/lib/client.js:58，属性: background
  - （dist 另有 shell Button primary hover `._primary_kz6gm_38:hover:not(:disabled)` 命中；client.js 已有命中，按规则不记录）

### `--dsw-alias-button-tool-bar-fill`
- 值（浅色 / 深色）：`#54555780` / `#54555780`（浅深相同）
- **直接引用的 UI 元素**：
  - 仅 dist：web-shell 按钮组件（Button）工具栏变体 `._toolbar_kz6gm_65`（dsh-web-frontend/dist/assets/index-C6eRlFa6.css:1）：`background:var(--dsw-alias-button-tool-bar-fill)`，属性: background。所有 client.js 均无该变量的使用命中（theme 仅定义行），故按规则记录 dist。

### `--dsw-alias-button-tool-bar-fill-invisible`
- 值（浅色 / 深色）：`#1f1f1f5c` / `#1f1f1f5c`（浅深相同）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-button-tool-bar-hover`
- 值（浅色 / 深色）：`#54555799` / `#54555799`（浅深相同）
- **直接引用的 UI 元素**：
  - 仅 dist：web-shell 按钮组件（Button）工具栏变体 hover `._toolbar_kz6gm_65:hover:not(:disabled)`（dsh-web-frontend/dist/assets/index-C6eRlFa6.css:1）：`background:var(--dsw-alias-button-tool-bar-hover)`，属性: background。所有 client.js 均无该变量的使用命中（theme 仅定义行），故按规则记录 dist。

### `--dsw-alias-interactive-bg-active`
- 值（浅色 / 深色）：`#2631481a` / `#ffffff24`
- **直接引用的 UI 元素**：
  - 目录选择器·选中行（dsh-client-ui-directory-picker-browse·浏览对话框行列表）：`.ZuhsRW_rowSelected,.ZuhsRW_rowSelected:hover`；client.js:27；background（带 fallback `var(--dsw-alias-interactive-bg-hover)`）
  - 轨迹视图·表格选中行（dsh-client-ui-trajectory·运行轨迹表）：`.Y0dWHa_table tbody tr[data-selected=true]`；client.js:2995；background
  - （dist 补充）基础按钮库·ghost 按钮按下态：`._ghost_kz6gm_47:active:not(:disabled)`；distCSS:1；background

### `--dsw-alias-interactive-bg-hover`
- 值（浅色 / 深色）：`#2631480f` / `#ffffff14`
- **直接引用的 UI 元素**：
  - 语言选择器·选项 hover（dsh-client-locale）：`.hVGvvW_selector:hover`；client.js:879；background
  - 代理预设·预设选择器 hover（dsh-client-ui-agent-preset）：`._5QVD0a_selector:hover:not(:disabled)`；client.js:261；background
  - 代理预设·坐席选择器 hover/展开（dsh-client-ui-agent-preset）：`.cubgiG_seat:not(:disabled):hover,.cubgiG_seat[aria-expanded=true]`；client.js:336；background
  - 代理预设·创建者按钮 hover（dsh-client-ui-agent-preset）：`.rtSEdW_creatorButton:hover:not(:disabled)`；client.js:976；background
  - 附件·缩略图底 / 上传卡帧底（dsh-client-ui-attachment）：`.JVDQca_thumbnail`、`.R_Yw7q_frame`；client.js:27,618；background
  - 命令面板·活动行底（dsh-client-ui-commands）：`.mufS8W_rowActive`；client.js:875；background
  - 会话·用量统计面板触发器/条底（dsh-client-ui-conversation·JObwrW）：`.JObwrW_trigger:hover`、`.JObwrW_bar`；client.js:3036；background
  - 会话·触发器 hover（dsh-client-ui-conversation·Sh0Q9G）：`.Sh0Q9G_trigger:hover:not(:disabled)`；client.js:3224；background
  - 会话·撰写器提示条/选择器 hover（dsh-client-ui-conversation·uV2eYG）：`.uV2eYG_notice`、`.uV2eYG_select:hover:not(:disabled)`；client.js:3463；background / background-color
  - 会话·选择器弹窗 hover（dsh-client-ui-conversation·T1PP_q）：`.T1PP_q_selector:hover`；client.js:4176；background
  - 会话·压缩按钮 hover（dsh-client-ui-conversation·gdEzaW）：`.gdEzaW_compactionButton:not(:disabled):hover`；client.js:4254；background
  - 会话·消息操作按钮 hover（dsh-client-ui-conversation·p-xYUq）：`.p-xYUq_action:hover`；client.js:5014；background
  - 会话·折叠面板操作按钮 hover（dsh-client-ui-conversation·_7yHdaG）：`._7yHdaG_action:hover:not(:disabled)`；client.js:6680；background
  - 会话·工作区选择器预览徽标边框/工作区按钮 hover（dsh-client-ui-conversation·pXSMma）：`.pXSMma_previewBadge`、`.pXSMma_workspace:not(:disabled):hover,.pXSMma_workspace[aria-expanded=true]`；client.js:6949；border / background
  - 会话·会话头部面包屑 hover（dsh-client-ui-conversation·wSkVaW）：`.wSkVaW_crumb:hover:not(:disabled)`；client.js:7118；background
  - 会话·代码查看器关闭按钮 hover（dsh-client-ui-conversation·ydkMvW）：`.ydkMvW_close:hover`；client.js:7429；background
  - 会话·停止提示条（dsh-client-ui-conversation·Sxvs8a）：`.Sxvs8a_stopped`；client.js:9443；background
  - 插件面板·inspect 项 hover（dsh-client-ui-cordis·cvtE3a）：`.cvtE3a_inspect:hover`；client.js:116；background
  - 插件面板·源码标签页 hover（dsh-client-ui-cordis·gNWCoW）：`.gNWCoW_sourceTab:hover:not(:disabled)`；client.js:211；background
  - 插件面板·运行行徽标/过渡操作/操作按钮 hover（dsh-client-ui-cordis·Nqubda）：`.Nqubda_badge:hover,.Nqubda_badge[data-active]`、`.Nqubda_transitionActions button:hover:not(:disabled)`、`.Nqubda_actionButton:hover:not(:disabled)`；client.js:572；background
  - 交付物·文件行底（dsh-client-ui-deliverables）：`.P4kPIW_file`；client.js:160；background
  - 目录选择·行 hover/选中行（dsh-client-ui-directory-picker-browse）：`.ZuhsRW_row:hover`、`.ZuhsRW_rowSelected,.ZuhsRW_rowSelected:hover`；client.js:27；background
  - 目标面板·图标按钮 hover（dsh-client-ui-goal）：`.nLMEza_iconBtn:hover`；client.js:11；background
  - 输入触发条·菜单项 hover/激活（dsh-client-ui-input-trigger）：`._3e4SsG_item:hover,._3e4SsG_item._3e4SsG_active`；client.js:717；background
  - 消息反馈·操作/打开备注/取消备注 hover（dsh-client-ui-message-feedback）：`._8_XoUG_action:hover`、`._8_XoUG_noteOpen:hover,._8_XoUG_noteOpen[aria-expanded=true]`、`._8_XoUG_noteCancel:hover`；client.js:329；background
  - 模型选择·触发器/选项/单元格 hover（dsh-client-ui-model-selection）：`._7KE1Ra_trigger:hover:not(:disabled)`、`._7KE1Ra_option:hover:not(:disabled),._7KE1Ra_option:focus-visible`、`._7KE1Ra_cell:hover`；client.js:234；background
  - 权限预设·选择器 hover（dsh-client-ui-permission-presets）：`.oY77xG_selector:hover:not(:disabled)`；client.js:34；background
  - 设置面板·导航触发器/关闭按钮 hover（dsh-client-ui-settings-general·VOzbGW）：`.VOzbGW_trigger:hover`、`.VOzbGW_close:hover`；client.js:28；background
  - 模型设置·各按钮 hover（dsh-client-ui-settings-models·zGbnIq）：`.zGbnIq_secondaryButton:hover:not(:disabled),.zGbnIq_addButton:hover:not(:disabled)`、`.zGbnIq_linkButton:hover:not(:disabled)`、`.zGbnIq_iconButton:hover:not(:disabled)`、`.zGbnIq_addModelButton:hover:not(:disabled)`；client.js:58；background
  - 插件清单·卡片内容 hover/展开（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_cardContent:hover,.qSYn7G_card[data-open=true]>.qSYn7G_cardContent`；client.js:11；background
  - 侧边栏·图标按钮/折叠态新建会话 hover（dsh-client-ui-sidebar）：`.hHd-Xa_iconButton:hover`、`.hHd-Xa_collapsed .hHd-Xa_newSession:hover`；client.js:26；background
  - 子代理·行点击区/刷新按钮 hover（dsh-client-ui-subagent）：`.ZKlsPq_row:hover>.ZKlsPq_clickarea,.ZKlsPq_row:focus-visible>.ZKlsPq_clickarea`、`.ZKlsPq_refresh:hover`；client.js:13；background
  - 主题设置面板·主题色块 hover（dsh-client-ui-theme·主题设置面板样式字符串）：`._8HJdBW_themeCube:hover:not(._8HJdBW_selected)`；client.js:26；background
  - 轨迹视图·历史加载/表格行/关闭/详情页签/工具调用/工具目录 hover（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_historyLoadButton:hover:not(:disabled)`、`.Y0dWHa_table tbody tr:not([data-collapsed-summary]):not([data-virtual-spacer]):not([data-history-load]):not([data-selected=true]):hover`、`.Y0dWHa_table tbody tr[data-collapsed-summary]:hover`、`.Y0dWHa_close:hover`、`.Y0dWHa_detailTab:hover`、`.Y0dWHa_assistantToolCallButton:hover`、`.Y0dWHa_assistantToolCallButton:focus-visible`、`.Y0dWHa_toolCatalogSummary:hover`、`.Y0dWHa_toolCatalogSummary:focus-visible`；client.js:2995；background
  - 轨迹视图·控制开关/操作按钮 hover（dsh-client-ui-trajectory·fV0t5q）：`.fV0t5q_toggle:hover,.fV0t5q_toggle[aria-pressed=true]`、`.fV0t5q_action:hover`；client.js:5300；background
  - 用户提问·图标按钮/选项/自定义行 hover（dsh-client-ui-user-questions·Mbwy4a）：`.Mbwy4a_iconButton:hover:not(:disabled)`、`.Mbwy4a_option:hover:not(:disabled),.Mbwy4a_optionSelected`、`.Mbwy4a_customRow:hover,.Mbwy4a_customRow:focus-within,.Mbwy4a_customRowActive`；client.js:233；background
  - 工作区·项目/会话/搜索结果行 hover 与菜单打开态（dsh-client-ui-workspace·YDXeBa）：`.YDXeBa_projectRow:hover,.YDXeBa_sessionRow:hover,.YDXeBa_sessionRow.YDXeBa_selected`、`.YDXeBa_searchResultRow:hover,.YDXeBa_searchResultRow.YDXeBa_selected`、`.YDXeBa_projectRow.YDXeBa_menuOpen,.YDXeBa_sessionRow.YDXeBa_menuOpen`；client.js:334；background
  - 工作区·搜索面板图标/搜索/清除按钮 hover（dsh-client-ui-workspace·qDHVXG）：`.qDHVXG_iconButton:hover`、`.qDHVXG_searchButton:hover`、`.qDHVXG_clearButton:hover`、`.qDHVXG_rail .qDHVXG_searchButton:hover`；client.js:969；background
  - 会话导出·导出按钮 hover（dsh-session-log-export）：`.nL4_yW_sessionLogButton:hover:not(:disabled)`；client.js:172；background
  - （dist 补充）基础按钮库 ghost/outline 按钮、interactive 状态、菜单 item、弹窗 close、copyButton、toggle hover：`._ghost_kz6gm_47:hover:not(:disabled)`、`._outline_kz6gm_56:hover:not(:disabled)`、`._interactive_e3ygd_15:hover`、`._item_19372_91:hover:not(:disabled)`、`._close_15u5s_61:hover`、`._copyButton_4qrvp_143:hover`、`._toggle_1ye18_5:hover`；distCSS:1；background

### `--dsw-alias-interactive-bg-hover-accent`
- 值（浅色 / 深色）：`#26314824` / `#ffffff3d`
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-interactive-bg-hover-danger`
- 值（浅色 / 深色）：`#ec13130d` / `#f25a5a26`
- **直接引用的 UI 元素**：
  - 代理预设·预设卡危险图标/删除确认按钮 hover（dsh-client-ui-agent-preset·agent 预设管理卡）：`.rtSEdW_iconDanger:hover:not(:disabled)`、`.rtSEdW_deleteConfirm:hover:not(:disabled)`；client.js:976；background
  - 附件·上传出错区（dsh-client-ui-attachment·上传卡）：`.R_Yw7q_error`；client.js:618；background
  - 会话·命令审批卡拒绝按钮 hover（dsh-client-ui-conversation）：`.bqrRRG_reject:hover:not(:disabled)`；client.js:6010；background
  - 插件面板·失败状态行状态徽标底（dsh-client-ui-cordis·插件运行列表）：`.Nqubda_row[data-cordis-status=failed] .Nqubda_rowStatus`；client.js:572；background
  - 模型选择·错误/警告选项底（dsh-client-ui-model-selection）：`._7KE1Ra_error,._7KE1Ra_warning`；client.js:234；background
  - 模型设置·危险按钮/危险图标按钮/删除确认 hover（dsh-client-ui-settings-models）：`.zGbnIq_dangerButton:hover:not(:disabled)`、`.zGbnIq_iconButtonDanger:hover:not(:disabled)`、`.zGbnIq_deleteConfirm:hover:not(:disabled)`；client.js:58；background
  - （dist 补充）基础菜单·危险项 hover：`._danger_19372_193:hover:not(:disabled)`；distCSS:1；background

### `--dsw-alias-interactive-bg-hover-solid`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-75) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-75`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 附件·缩略图箭头 hover（dsh-client-ui-attachment）：`.JVDQca_arrow:hover`；client.js:27；background
  - 会话·输入区“添加”按钮 hover（dsh-client-ui-conversation·撰写器）：`.uV2eYG_add:hover:not(:disabled)`；client.js:3463；background
  - 会话·更早历史加载按钮（dsh-client-ui-conversation·历史区）：`.Md3f7G_older button`；client.js:5452；background
  - 插件面板·inspect 按钮 hover（dsh-client-ui-cordis·插件详情卡）：`.gNWCoW_inspectButton:hover`；client.js:211；background
  - 模型设置·次按钮 hover（dsh-client-ui-settings-models）：`.zGbnIq_secondaryButton:hover:not(:disabled)`；client.js:58；background
  - 技能·检查按钮 hover（dsh-client-ui-skill）：`.iWrAna_inspectButton:hover`；client.js:11；background
  - 工具调用·检查按钮 hover（dsh-client-ui-tool·工具卡）：`.o3BgMG_inspectButton:hover`、`.CY-8Ka_inspectButton:hover`；client.js:627,1128；background

### `--dsw-alias-label-caption`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-400) / var(--dsw-static-neutral-bluish-600)
> 指向：`--dsw-static-neutral-bluish-400`、`--dsw-static-neutral-bluish-600`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 代理预设·坐席选择器箭头/项描述（dsh-client-ui-agent-preset·cubgiG）：`.cubgiG_chevron`、`.cubgiG_itemDesc`；client.js:336；color
  - 会话·触发器箭头（dsh-client-ui-conversation·Sh0Q9G）：`.Sh0Q9G_chevron`；client.js:3224；color
  - 会话·撰写器提示文字/输入占位（dsh-client-ui-conversation·uV2eYG）：`.uV2eYG_hint`、`.uV2eYG_input::placeholder`；client.js:3463；color / -webkit-text-fill-color
  - 会话·压缩分隔条（dsh-client-ui-conversation·gdEzaW）：`.gdEzaW_compactionSep`；client.js:4254；background
  - 会话·附件目录卡字段键/文件操作/目录提示/区块名/转发者/召回计数（dsh-client-ui-conversation·NM4-hq）：`.NM4-hq_fieldKey`、`.NM4-hq_fileAction`、`.NM4-hq_catalogNotice`、`.NM4-hq_sectionName`、`.NM4-hq_relaySender`、`.NM4-hq_recallCounts`；client.js:4354；color
  - 会话·引用块分隔条（dsh-client-ui-conversation·pC0e7a）：`.pC0e7a_sep`；client.js:4911；background
  - 会话·转轮状态时钟（dsh-client-ui-conversation·Md3f7G）：`.Md3f7G_turnStatusClock`；client.js:5452；color / -webkit-text-fill-color
  - 会话·任务进度待定字形（dsh-client-ui-conversation·lXshSW）：`.lXshSW_glyphPending`；client.js:6473；color
  - 会话·工作区选择器箭头/输入占位（dsh-client-ui-conversation·pXSMma）：`.pXSMma_chevron`、`.pXSMma_modalInput::placeholder`；client.js:6949；color
  - 会话·会话头部面包屑分隔符（dsh-client-ui-conversation·wSkVaW）：`.wSkVaW_crumbSep`；client.js:7118；color
  - 会话·思考行分隔条 / 命令行分隔条（dsh-client-ui-conversation·QWLzlG/_Xvjua）：`.QWLzlG_separator`、`._Xvjua_separator`；client.js:9350,9556；background
  - 插件面板·状态文本（dsh-client-ui-cordis·cvtE3a）：`.cvtE3a_status`；client.js:116；color
  - 插件面板·详情卡提示/状态标签/提示条/终结卡片文字/区块标签（dsh-client-ui-cordis·gNWCoW）：`.gNWCoW_panelHint`、`.gNWCoW_statusLabel`、`.gNWCoW_notice`、`.gNWCoW_card[data-terminal] .gNWCoW_title,.gNWCoW_card[data-terminal] .gNWCoW_name,.gNWCoW_card[data-terminal] .gNWCoW_purpose,.gNWCoW_card[data-terminal] .gNWCoW_statusLabel`（color）、`.gNWCoW_card[data-terminal] .gNWCoW_separator`（background）、`.gNWCoW_sectionLabel`；client.js:211；color / background
  - 插件面板·运行列表分组/行状态/版本选择器/过渡/当前版本（dsh-client-ui-cordis·Nqubda）：`.Nqubda_group`、`.Nqubda_rowStatus`、`.Nqubda_row[data-cordis-status=idle] .Nqubda_rowStatus`、`.Nqubda_versionPicker`、`.Nqubda_transition`、`.Nqubda_activeVersion`；client.js:572；color
  - 目录选择·编辑路径禁用/显示隐藏开关禁用/新建输入占位（dsh-client-ui-directory-picker-browse）：`.ZuhsRW_crumbEditZone:disabled .ZuhsRW_crumbEditGlyph`、`.ZuhsRW_showHiddenToggle:disabled`、`.ZuhsRW_createInput::placeholder`；client.js:27；color
  - 目标面板·目标输入占位（dsh-client-ui-goal）：`.nLMEza_objectiveInput::placeholder`；client.js:11；color
  - 模型选择·触发器 effort/箭头（dsh-client-ui-model-selection）：`._7KE1Ra_triggerEffort`、`._7KE1Ra_chevron`；client.js:234；color
  - 技能·分隔条/说明标题（dsh-client-ui-skill）：`.iWrAna_separator`（background）、`.iWrAna_instructionsHeader`（color）；client.js:11
  - 子代理·分隔符（dsh-client-ui-subagent）：`.ZKlsPq_separator`；client.js:13；color
  - 工具调用·分隔点/IO 标签（dsh-client-ui-tool）：`.o3BgMG_sep`、`.o3BgMG_ioLabel`；client.js:627；background / color；`.CY-8Ka_ioLabel`、`.CY-8Ka_sep`；client.js:1128；color / background
  - 轨迹视图·请求边界控制点/提示差异元行/无输出文本/箭头/概览与源块图标（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_requestBoundaryControl:before`（background）、`.Y0dWHa_promptDiffLinemeta`、`.Y0dWHa_noOutputText`、`.Y0dWHa_arrow`、`.Y0dWHa_overviewHierarchyJumpIconTight`、`.Y0dWHa_overviewTitleIcon`、`.Y0dWHa_sourceBlockJumpIcon`、`.Y0dWHa_assistantToolCallIcon`、`.Y0dWHa_toolCatalogChevron,.Y0dWHa_toolCatalogIcon`；client.js:2995；color
  - 轨迹视图·搜索框文字与 hover 边框/占位（dsh-client-ui-trajectory·fV0t5q）：`.fV0t5q_search`、`.fV0t5q_search:hover`（border-color）、`.fV0t5q_searchInput::placeholder`；client.js:5300；color / border-color
  - 轨迹视图·时间轴标签/空态（dsh-client-ui-trajectory·_1p9O6q）：`._1p9O6q_labels`、`._1p9O6q_empty`；client.js:5552；color
  - 用户提问·字段输入占位（dsh-client-ui-user-questions·Mbwy4a）：`.Mbwy4a_fieldInput::placeholder`；client.js:233；color
  - 工作区·树箭头/搜索展开态（dsh-client-ui-workspace）：`.YDXeBa_chevron`；client.js:334；`.qDHVXG_searchExpanded`；client.js:969；color
  - （dist 补充）markdown 渲染器·引用块左边框：`._markdown_1r4m5_5 blockquote`；distCSS:1；border-left

### `--dsw-alias-label-dimmed`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-200) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-neutral-bluish-200`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 代理预设·卡片 hover 边框/卡片 ID/输入占位（dsh-client-ui-agent-preset·rtSEdW）：`.rtSEdW_card:hover:not(.rtSEdW_cardActive)`（border-color）、`.rtSEdW_cardId`、`.rtSEdW_input::placeholder`；client.js:976；color / border-color
  - 会话·触发器禁用态/工作区输入禁用态（dsh-client-ui-conversation）：`.Sh0Q9G_trigger:disabled`；client.js:3224；`.pXSMma_modalInput:disabled`；client.js:6949；color
  - 输入触发条·加载态（dsh-client-ui-input-trigger）：`._3e4SsG_loading`；client.js:717；color
  - 模型选择·触发器/选项禁用态（dsh-client-ui-model-selection）：`._7KE1Ra_trigger:disabled`、`._7KE1Ra_option:disabled`；client.js:234；color
  - 模型设置·输入占位（dsh-client-ui-settings-models）：`.zGbnIq_input::placeholder`；client.js:58；color
  - 插件设置·卡片 hover/展开/放弃按钮 hover 边框（dsh-client-ui-settings-plugins·YyYd_a）：`.YyYd_a_card:hover`、`.YyYd_a_cardOpen`、`.YyYd_a_discard:hover:not(:disabled)`；client.js:155；border-color
  - 子代理·禁用态（dsh-client-ui-subagent）：`.ZKlsPq_disabled`；client.js:13；color
  - 轨迹视图·控制项禁用态（dsh-client-ui-trajectory·fV0t5q）：`.fV0t5q_control:disabled`；client.js:5300；color
  - 用户提问·图标按钮禁用态（dsh-client-ui-user-questions）：`.Mbwy4a_iconButton:disabled`；client.js:233；color
  - 工作区·重命名输入禁用态（dsh-client-ui-workspace）：`.qDHVXG_renameInput:disabled`；client.js:969；color
  - 会话导出·按钮禁用态（dsh-session-log-export）：`.nL4_yW_sessionLogButton:disabled`；client.js:172；color
  - （dist 补充）基础输入框·占位符：`._input_1ao1y_25::placeholder`；distCSS:1；color

### `--dsw-alias-label-primary`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-1000) / var(--dsw-static-neutral-bluish-50)
> 指向：`--dsw-static-neutral-bluish-1000`、`--dsw-static-neutral-bluish-50`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 语言选择器·标题/选择器（dsh-client-locale）：`.hVGvvW_title`、`.hVGvvW_selector`；client.js:879；color
  - 代理预设·预设选择器标题/文本（dsh-client-ui-agent-preset·_5QVD0a）：`._5QVD0a_title`、`._5QVD0a_selector`；client.js:261；color
  - 代理预设·坐席选择器/图标/项名（dsh-client-ui-agent-preset·cubgiG）：`.cubgiG_seat`、`.cubgiG_seatIcon`、`.cubgiG_itemName`；client.js:336；color
  - 代理预设·预设卡（dsh-client-ui-agent-preset·rtSEdW）：`.rtSEdW_section`、`.rtSEdW_cardActive`（border-color）、`.rtSEdW_inUse`（background）、`.rtSEdW_iconButton:hover:not(:disabled)`、`.rtSEdW_iconButton:after`（background）、`.rtSEdW_input`、`.rtSEdW_creatorButton`；client.js:976；color / border-color / background
  - 附件·包裹文字/关闭按钮（dsh-client-ui-attachment）：`.BInVoG_wrap`；client.js:196；`.fNh4Da_close`；client.js:382；color
  - 命令面板·行/勾选/搜索/重试（dsh-client-ui-commands）：`.mufS8W_row`、`.mufS8W_check`、`.mufS8W_search`、`.mufS8W_retry`；client.js:875；color
  - 会话·用量统计（dsh-client-ui-conversation·JObwrW）：`.JObwrW_figures`、`.JObwrW_percent`、`.JObwrW_row dd`；client.js:3036；color
  - 会话·撰写器（dsh-client-ui-conversation·uV2eYG）：`.uV2eYG_backdrop`、`.uV2eYG_add`；client.js:3463；color
  - 会话·选择器弹窗（dsh-client-ui-conversation·T1PP_q）：`.T1PP_q_title`、`.T1PP_q_selector`；client.js:4176；color
  - 会话·压缩气泡（dsh-client-ui-conversation·gdEzaW）：`.gdEzaW_bubble`；client.js:4254；color
  - 会话·历史区到底按钮（dsh-client-ui-conversation·Md3f7G）：`.Md3f7G_toBottom`；client.js:5452；color
  - 会话·审批卡标题（dsh-client-ui-conversation·bqrRRG）：`.bqrRRG_headline`；client.js:6010；color
  - 会话·任务进度标题（dsh-client-ui-conversation·lXshSW）：`.lXshSW_title`；client.js:6473；color
  - 会话·折叠面板头部/编辑器（dsh-client-ui-conversation·_7yHdaG）：`._7yHdaG_header`、`._7yHdaG_editor`；client.js:6680；color
  - 会话·工作区选择器（dsh-client-ui-conversation·pXSMma）：`.pXSMma_headline`、`.pXSMma_fish`、`.pXSMma_workspace`、`.pXSMma_folder`、`.pXSMma_modalInput`；client.js:6949；color
  - 会话·会话头部当前面包屑（dsh-client-ui-conversation·wSkVaW）：`.wSkVaW_crumbCurrent`；client.js:7118；color
  - 会话·代码查看器标题/代码（dsh-client-ui-conversation·ydkMvW）：`.ydkMvW_title`、`.ydkMvW_code`；client.js:7429；color
  - 会话·停止提示条根（dsh-client-ui-conversation·Sxvs8a）：`.Sxvs8a_root`；client.js:9443；color
  - 会话·命令行主体（dsh-client-ui-conversation·_Xvjua）：`._Xvjua_body`；client.js:9556；color
  - 插件面板·inspect 图标/标题/分隔条（dsh-client-ui-cordis·cvtE3a）：`.cvtE3a_icon`、`.cvtE3a_title`、`.cvtE3a_separator`；client.js:116；color / background
  - 插件面板·详情卡（dsh-client-ui-cordis·gNWCoW）：`.gNWCoW_sourceTab:hover:not(:disabled)`、`.gNWCoW_inspectButton:hover`、`.gNWCoW_title`、`.gNWCoW_name`、`.gNWCoW_purpose`；client.js:211；color
  - 插件面板·运行行徽标/标题/行名（dsh-client-ui-cordis·Nqubda）：`.Nqubda_badge`、`.Nqubda_title`、`.Nqubda_rowName`；client.js:572；color
  - 交付物·文件行 hover（dsh-client-ui-deliverables）：`.P4kPIW_file:hover`；client.js:160；color
  - 目录选择·标题/面包屑/路径输入/行名/开关 hover 与激活/新建（dsh-client-ui-directory-picker-browse）：`.ZuhsRW_title`、`.ZuhsRW_crumb:hover`、`.ZuhsRW_crumbEditZone:enabled:hover .ZuhsRW_crumbEditGlyph,.ZuhsRW_crumbEditZone:focus-visible .ZuhsRW_crumbEditGlyph`、`.ZuhsRW_pathInput`、`.ZuhsRW_rowName`、`.ZuhsRW_showHiddenToggle:hover`、`.ZuhsRW_showHiddenToggleActive`、`.ZuhsRW_createTitle`、`.ZuhsRW_createIn`、`.ZuhsRW_createInput`；client.js:27；color
  - 目标面板·标签/输入/气泡（dsh-client-ui-goal）：`.nLMEza_label`、`.nLMEza_objectiveInput`；client.js:11；`.oRe1gG_bubble`；client.js:254；color
  - 输入触发条·菜单项（dsh-client-ui-input-trigger）：`._3e4SsG_item`；client.js:717；color
  - 任务列表·行（dsh-client-ui-jobs）：`.QsffPG_row`；client.js:11；color
  - 消息反馈·激活操作/备注输入（dsh-client-ui-message-feedback）：`._8_XoUG_action[data-active]`、`._8_XoUG_noteInput`；client.js:329；color
  - 模型选择·菜单/勾选/单元格（dsh-client-ui-model-selection）：`._7KE1Ra_menu`、`._7KE1Ra_check`、`._7KE1Ra_cell`；client.js:234；color
  - 权限预设·标题/选择器（dsh-client-ui-permission-presets）：`.oY77xG_title`、`.oY77xG_selector`；client.js:34；color
  - 设置面板·触发器/导航标题/导航单元格/关闭（dsh-client-ui-settings-general·VOzbGW）：`.VOzbGW_trigger`、`.VOzbGW_navTitle`、`.VOzbGW_navCell`、`.VOzbGW_close`；client.js:28；color
  - 模型设置·页面各文字（dsh-client-ui-settings-models·zGbnIq）：`.zGbnIq_section`、`.zGbnIq_title`、`.zGbnIq_rowName`、`.zGbnIq_secondaryButton,.zGbnIq_addButton`、`.zGbnIq_editorTitle`、`.zGbnIq_customizedSummary:hover`、`.zGbnIq_iconButton:hover:not(:disabled)`、`.zGbnIq_addModelButton`、`.zGbnIq_input`；client.js:58；color；`.jLrgrW_title`；client.js:2111；color
  - 插件清单·区块/失败按钮/搜索输入/条目值（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_section`、`.qSYn7G_failure button`、`.qSYn7G_search input`、`.qSYn7G_entryValue`；client.js:11；color
  - 插件设置·标签/重置/输入/卡片名/保存/页签（dsh-client-ui-settings-plugins）：`.At1oFq_label`、`.At1oFq_reset:hover:not(:disabled)`、`.At1oFq_input`；client.js:13；`.YyYd_a_name`、`.YyYd_a_discard:hover:not(:disabled)`、`.YyYd_a_save`（background）；client.js:155；`.pbvGtq_section`、`.pbvGtq_tab:hover,.pbvGtq_tab[data-active=true]`、`.pbvGtq_tab[data-active=true]:after,.pbvGtq_tab:focus-visible:after`（background）、`.pbvGtq_tab:focus-visible`；client.js:364；color / background
  - 侧边栏·根/图标按钮/构建版本/新建会话（dsh-client-ui-sidebar）：`.hHd-Xa_root`、`.hHd-Xa_collapsed .hHd-Xa_iconButton`、`.hHd-Xa_buildRevision`（background）、`.hHd-Xa_newSession`；client.js:26；color / background
  - 技能·检查按钮 hover（dsh-client-ui-skill）：`.iWrAna_inspectButton:hover`；client.js:11；color
  - 子代理·切换触发器/行/展开（dsh-client-ui-subagent）：`.ZKlsPq_switcherTrigger`、`.ZKlsPq_switcherTrigger:hover,.ZKlsPq_switcherTrigger:focus-visible`、`.ZKlsPq_row`、`.ZKlsPq_disclosure:hover`；client.js:13；`.XJ7liG_frame strong`；client.js:682；color
  - 主题设置面板·标题/主题色块（dsh-client-ui-theme·L26 面板样式）：`._8HJdBW_title`、`._8HJdBW_themeCube`；client.js:26；color
  - 主题设置面板·主题色选择项（dsh-client-ui-theme·JS 列表）：`name: "--dsw-alias-label-primary"`；client.js:1058；`cssVariable: "--dsw-alias-label-primary"`；client.js:1062（JS 使用，供主题色选择 UI 读取）
  - 工具调用·文件链接 hover/检查按钮 hover/代码/IO 文本（dsh-client-ui-tool）：`.o3BgMG_fileLink:hover`、`.o3BgMG_inspectButton:hover`；client.js:627；`.xDAfVq_code`；client.js:977；`.CY-8Ka_inspectButton:hover`；client.js:1128；color
  - 轨迹视图·表格/详情面板/概览/promptDiff/工具目录/结果块等（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_historyLoadButton:hover:not(:disabled)`、`.Y0dWHa_table`、`.Y0dWHa_kindSlot [role=tooltip]`、`.Y0dWHa_content`、`.Y0dWHa_promptDiff`、`.Y0dWHa_promptDiffLineadded`、`.Y0dWHa_toolCallNameTypeface`、`.Y0dWHa_detailsTitle`、`.Y0dWHa_close:hover`、`.Y0dWHa_detailTab:hover`、`.Y0dWHa_overviewHierarchyNavLink:hover`、`.Y0dWHa_overviewHierarchyNavLink:hover .Y0dWHa_overviewHierarchyJumpIconTight,.Y0dWHa_overviewHierarchyNavLink:focus-visible .Y0dWHa_overviewHierarchyJumpIconTight`、`.Y0dWHa_overviewHierarchyNavLink:focus-visible`、`.Y0dWHa_overview dd`、`.Y0dWHa_overviewTitle:hover .Y0dWHa_overviewTitleIcon`、`.Y0dWHa_markdownPreview,.Y0dWHa_markdownPayload`、`.Y0dWHa_schemaName`、`.Y0dWHa_payload`、`.Y0dWHa_sourceBlockJumpTarget:hover .Y0dWHa_sourceBlockJumpIcon`、`.Y0dWHa_sourceBlockContent`、`.Y0dWHa_toolCatalogName`、`.Y0dWHa_resultBlockText`；client.js:2995；color
  - 轨迹视图·控制开关/操作/搜索输入（dsh-client-ui-trajectory·fV0t5q）：`.fV0t5q_toggle:hover,.fV0t5q_toggle[aria-pressed=true]`、`.fV0t5q_control:hover:not(:disabled),.fV0t5q_control[aria-checked=true],.fV0t5q_control[aria-pressed=true]`、`.fV0t5q_action:hover`、`.fV0t5q_searchInput`；client.js:5300；color
  - 轨迹视图·时间轴根组件（dsh-client-ui-trajectory·qBU-ya）：`.qBU-ya_root`；client.js:6935；color
  - 用户提问·卡片/讨论按钮/字段输入/复选框（dsh-client-ui-user-questions）：`.LVzXQa_card`、`.LVzXQa_discuss:hover:not(:disabled)`；client.js:115；`.Mbwy4a_card`、`.Mbwy4a_iconButton:hover:not(:disabled)`、`.Mbwy4a_checkboxChecked:before`（border-color + background）、`.Mbwy4a_fieldInput`；client.js:233；color / border-color / background
  - 工作区·树行/图标按钮/搜索输入/重命名输入（dsh-client-ui-workspace）：`.YDXeBa_projectRow,.YDXeBa_sessionRow`、`.YDXeBa_searchResultRow`、`.YDXeBa_iconButton:hover`；client.js:334；`.qDHVXG_searchInput`、`.qDHVXG_rail .qDHVXG_iconButton`、`.qDHVXG_rail .qDHVXG_searchButton`、`.qDHVXG_renameInput`；client.js:969；color
  - 会话导出·导出按钮（dsh-session-log-export）：`.nL4_yW_sessionLogButton`；client.js:172；color
  - （dist 补充）基础组件库（boot 屏 wordmark/失败标题、按钮/激活项/输入/菜单项/勾选/弹窗标题/描述/警告 acknowledge/复制块 root/copyButton/expander、命令块/文件树块/diff 块/JSON 块/markdown 正文、toggle body、body 根文字）：`._wordmark_1ionb_33`、`._failedTitle_1ionb_80`、`._button_kz6gm_4`、`._active_e3ygd_23`、`._input_1ao1y_25`、`._item_19372_91`、`._check_19372_181`、`._title_15u5s_53`、`._description_15u5s_80`、`._acknowledgement_1nu42_38`、`._root_4qrvp_1`、`._copyButton_4qrvp_143:hover`、`._expander_4qrvp_78:hover`、`._block_10eou_7`、`._command_10eou_122`、`._block_biesw_7`、`._label_biesw_32`、`._content_biesw_99`、`._block_srovd_7`、`._path_srovd_53`、`._block_s66q0_7`、`._filePath_s66q0_88`、`._block_178r4_4`、`._infostring_178r4_42`、`._plain_178r4_94`、`._markdown_1r4m5_5`、`._block_d4nqi_7`、`._body_1ye18_20`、`body`；distCSS:1；color
  - （dist JS 补充）distJS 内 ANSI 颜色映射（黑/白 → 该变量）；distJS:56

### `--dsw-alias-label-primary-bluish`
- 值（浅色 / 深色）：var(--dsw-static-blue-900) / var(--dsw-static-neutral-bluish-50)
> 指向：`--dsw-static-blue-900`、`--dsw-static-neutral-bluish-50`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 会话·工作区选择器预览徽标文字（dsh-client-ui-conversation·pXSMma）：`.pXSMma_previewBadge`；client.js:6949；color

### `--dsw-alias-label-primary-dimmed`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-950) / var(--dsw-static-neutral-bluish-100)
> 指向：`--dsw-static-neutral-bluish-950`、`--dsw-static-neutral-bluish-100`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 会话·压缩标题（dsh-client-ui-conversation·gdEzaW）：`.gdEzaW_compactionTitle`；client.js:4254；color
  - 会话·折叠面板预览（dsh-client-ui-conversation·_7yHdaG）：`._7yHdaG_preview`；client.js:6680；color
  - 目标面板·目标文本（dsh-client-ui-goal）：`.nLMEza_objective`；client.js:11；color

### `--dsw-alias-label-primary-foreground`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-1000)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-1000`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 消息反馈·保存备注按钮（dsh-client-ui-message-feedback）：`._8_XoUG_noteSave`；client.js:329；color
  - 模型设置·主按钮（dsh-client-ui-settings-models）：`.zGbnIq_primaryButton`；client.js:58；color
  - 用户提问·选中复选框（dsh-client-ui-user-questions）：`.Mbwy4a_checkboxChecked`；client.js:233；color
  - （dist 补充）基础按钮库·主按钮文字 / 错误 banner 文字：`._primary_kz6gm_38`、`._banner_ugy7y_1`；distCSS:1；color

### `--dsw-alias-label-primary-inverted`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 附件·移除按钮（dsh-client-ui-attachment·缩略图区）：`.JVDQca_remove`；client.js:27；color
  - 侧边栏·构建版本徽标（dsh-client-ui-sidebar）：`.hHd-Xa_buildRevision`；client.js:26；color
  - （dist 补充）基础 toast·文字色：`._toast_fvpz7_7`；distCSS:1；color
  - （仅 dist JS）DSH 品牌字标徽标（wordmark badge，`#dsh-wordmark-badge-clip` clipPath）的 7 个字形 path：`fill:"var(--dsw-alias-label-primary-inverted)"`；distJS（index-ClqxG24t.js，SVG 内联 fill，非 CSS 选择器）

### `--dsw-alias-label-secondary`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-700) / var(--dsw-static-neutral-bluish-300)
> 指向：`--dsw-static-neutral-bluish-700`、`--dsw-static-neutral-bluish-300`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 代理预设·预设标签（dsh-client-ui-agent-preset·SVAs4q）：`.SVAs4q_label`；client.js:162；color
  - 代理预设·预设卡描述/路径/次按钮/字段标签/查看器代码（dsh-client-ui-agent-preset·rtSEdW）：`.rtSEdW_cardDesc`、`.rtSEdW_revealedPath code`、`.rtSEdW_secondaryButton`、`.rtSEdW_fieldLabel`、`.rtSEdW_viewerCode`；client.js:976；color
  - 附件·缩略图箭头（dsh-client-ui-attachment）：`.JVDQca_arrow`；client.js:27；color
  - 会话·用量统计触发器/面板/行 dt（dsh-client-ui-conversation·JObwrW）：`.JObwrW_trigger`、`.JObwrW_panel`、`.JObwrW_row dt`；client.js:3036；color
  - 会话·触发器（dsh-client-ui-conversation·Sh0Q9G）：`.Sh0Q9G_trigger`；client.js:3224；color
  - 会话·撰写器提示条/选择器（dsh-client-ui-conversation·uV2eYG）：`.uV2eYG_notice`、`.uV2eYG_select`；client.js:3463；color
  - 会话·压缩区（dsh-client-ui-conversation·gdEzaW）：`.gdEzaW_compactionLeading`、`.gdEzaW_retrySummary:hover`、`.gdEzaW_retryRow[data-active] .gdEzaW_retryText`（background 渐变 `color-mix(...50%, var(--dsw-alias-label-secondary) 50%, ...)`）、`.gdEzaW_retryDetailLabel`、`.gdEzaW_turnErrorMessage`；client.js:4254；color / background
  - 会话·附件目录卡正文/路径/条目名/区块文字/召回标签（dsh-client-ui-conversation·NM4-hq）：`.NM4-hq_text`、`.NM4-hq_filePath`、`.NM4-hq_entryName`、`.NM4-hq_sectionText`、`.NM4-hq_recallLabel`；client.js:4354；color
  - 会话·引用块箭头（dsh-client-ui-conversation·pC0e7a）：`.pC0e7a_chevron`；client.js:4911；color
  - 会话·消息操作 hover（dsh-client-ui-conversation·p-xYUq）：`.p-xYUq_action:hover`；client.js:5014；color
  - 会话·历史加载按钮（dsh-client-ui-conversation·Md3f7G）：`.Md3f7G_older button`；client.js:5452；color
  - 会话·任务进度项（dsh-client-ui-conversation·lXshSW）：`.lXshSW_item`；client.js:6473；color
  - 会话·代码查看器关闭/区块标签（dsh-client-ui-conversation·ydkMvW）：`.ydkMvW_close`、`.ydkMvW_sectionLabel`；client.js:7429；color
  - 会话·思考行/命令行箭头（dsh-client-ui-conversation·QWLzlG/_Xvjua）：`.QWLzlG_chevron`、`._Xvjua_chevron`；client.js:9350,9556；color
  - 插件面板·inspect 摘要/错误/输出（dsh-client-ui-cordis·cvtE3a）：`.cvtE3a_summary,.cvtE3a_error`、`.cvtE3a_output`；client.js:116；color
  - 插件面板·详情卡名/审批提示/输出/检查按钮（dsh-client-ui-cordis·gNWCoW）：`.gNWCoW_name`、`.gNWCoW_approvalPrompt`、`.gNWCoW_output`、`.gNWCoW_inspectButton`；client.js:211；color
  - 插件面板·运行行版本下拉/过渡按钮/操作按钮 hover（dsh-client-ui-cordis·Nqubda）：`.Nqubda_versionPicker select`、`.Nqubda_transitionActions button`、`.Nqubda_actionButton:hover:not(:disabled)`；client.js:572；color
  - 交付物·文件行/显示文件夹 hover（dsh-client-ui-deliverables）：`.P4kPIW_file`、`.P4kPIW_showFolder:hover`；client.js:160；color
  - 目录选择·行图标/状态/显示隐藏开关（dsh-client-ui-directory-picker-browse）：`.ZuhsRW_rowIcon`、`.ZuhsRW_status`、`.ZuhsRW_showHiddenToggle`；client.js:27；color
  - 目标面板·图标按钮 hover（dsh-client-ui-goal）：`.nLMEza_iconBtn:hover`；client.js:11；color
  - 任务列表·触发器 hover/类型（dsh-client-ui-jobs）：`.QsffPG_trigger:hover,.QsffPG_trigger:focus-visible`、`.QsffPG_kind`；client.js:11；color
  - 消息反馈·操作/备注开关/取消 hover（dsh-client-ui-message-feedback）：`._8_XoUG_action:hover`、`._8_XoUG_noteOpen:hover,._8_XoUG_noteOpen[aria-expanded=true]`、`._8_XoUG_noteCancel:hover`；client.js:329；color
  - 模型选择·触发器（dsh-client-ui-model-selection）：`._7KE1Ra_trigger`；client.js:234；color
  - 模型设置·行标签/字段标签/链接按钮 hover/自定义摘要/目录标题（dsh-client-ui-settings-models·zGbnIq）：`.zGbnIq_rowTag`、`.zGbnIq_fieldLabel`、`.zGbnIq_linkButton:hover:not(:disabled)`、`.zGbnIq_customizedSummary`、`.zGbnIq_modelCatalogTitle`；client.js:58；`.GL8Viq_description`；client.js:2173；`.t1T8VW_copy`；client.js:2265；color
  - 插件清单·配置标签/详情 dd（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_configTag`、`.qSYn7G_details dd`；client.js:11；color
  - 插件设置·徽标/重置/待定/放弃（dsh-client-ui-settings-plugins）：`.At1oFq_badge`、`.At1oFq_reset`；client.js:13；`.YyYd_a_pending`、`.YyYd_a_discard`；client.js:155；color
  - 侧边栏·图标按钮（dsh-client-ui-sidebar）：`.hHd-Xa_iconButton`；client.js:26；color
  - 技能·箭头/标题/说明/检查按钮（dsh-client-ui-skill）：`.iWrAna_chevron`、`.iWrAna_title`、`.iWrAna_instructions`、`.iWrAna_inspectButton`；client.js:11；color
  - 子代理·触发器 hover（dsh-client-ui-subagent）：`.ZKlsPq_trigger:hover,.ZKlsPq_trigger:focus-visible`；client.js:13；color
  - 工具调用·箭头/文件链接/检查按钮/IO 文本/描述/标题（dsh-client-ui-tool）：`.o3BgMG_chevron`、`.o3BgMG_fileLink`、`.o3BgMG_inspectButton`、`.o3BgMG_ioText`；client.js:627；`.xDAfVq_description`；client.js:977；`.CY-8Ka_ioText`、`.CY-8Ka_chevron`、`.CY-8Ka_title`、`.CY-8Ka_inspectButton`；client.js:1128；color
  - 轨迹视图·历史加载条/按钮/请求边界/系统与上下文行/折叠/差异/工具调用等（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_historyLoadingBar`、`.Y0dWHa_historyLoadButton`、`.Y0dWHa_requestBoundaryControl:after`、`.Y0dWHa_systemNeutral`、`.Y0dWHa_contextGreen`、`.Y0dWHa_compacted`、`.Y0dWHa_promptDiffTitle`、`.Y0dWHa_promptDiffLinecontext`、`.Y0dWHa_collapsedTurnContent`、`.Y0dWHa_toolCallPayload`、`.Y0dWHa_inlineResult`、`.Y0dWHa_requestDetailsDot`（background）、`.Y0dWHa_close`、`.Y0dWHa_overviewHierarchyNavLink`、`.Y0dWHa_usageHeading`、`.Y0dWHa_overviewHeading`、`.Y0dWHa_thinkingQuote`、`.Y0dWHa_thinkingToggle:hover`、`.Y0dWHa_thinkingQuote .Y0dWHa_markdownPreview,.Y0dWHa_thinkingQuote .Y0dWHa_markdownPayload,.Y0dWHa_thinkingQuote .Y0dWHa_payload`、`.Y0dWHa_schemaDescription`、`.Y0dWHa_assistantToolCalls`、`.Y0dWHa_assistantToolCallButton:hover .Y0dWHa_assistantToolCallIcon,.Y0dWHa_assistantToolCallButton:focus-visible .Y0dWHa_assistantToolCallIcon`、`.Y0dWHa_assistantToolCallName`、`.Y0dWHa_toolCatalogFullDescription`；client.js:2995；color / background
  - 轨迹视图·时间轴更早历史/span（dsh-client-ui-trajectory·_1p9O6q）：`._1p9O6q_earlierHistory`、`._1p9O6q_span`（background）、`._1p9O6q_span[data-timeline-span=context]`（background color-mix）；client.js:5552；color / background
  - 用户提问·讨论按钮/进度/数字（dsh-client-ui-user-questions）：`.LVzXQa_discuss`；client.js:115；`.Mbwy4a_progress`、`.Mbwy4a_number`；client.js:233；color
  - 工作流执行·运行标题/状态尾/阶段标题/阶段状态/成员行/成员标签/成员状态（dsh-client-ui-workflow-run·DBuyfa）：`.DBuyfa_runTitle`、`.DBuyfa_statusTail`、`.DBuyfa_phaseTitle`、`.DBuyfa_phaseStatus`、`.DBuyfa_memberRow,.DBuyfa_memberButton`、`.DBuyfa_memberLabel`、`.DBuyfa_memberStatus`；client.js:12；color
  - 工作区·搜索结果片段/菜单状态/图标按钮/搜索/清除/警告/溢出按钮/删除状态（dsh-client-ui-workspace）：`.YDXeBa_searchResultSnippet`；client.js:334；`._G5b-a_menuStatus`；client.js:799；`.qDHVXG_iconButton`、`.qDHVXG_search`、`.qDHVXG_clearButton`、`.qDHVXG_searchWarning`、`.qDHVXG_sessionOverflowButton:hover`、`.qDHVXG_deleteStatus`；client.js:969；color
  - 主题设置面板·主题色选择项（dsh-client-ui-theme·JS）：`name: "--dsw-alias-label-secondary"`；client.js:1065；`cssVariable: "--dsw-alias-label-secondary"`；client.js:1069
  - （dist 补充）基础组件库（boot 失败项/弹窗标题/pill/close/warning 文案/copy 块/展开/markdown li marker 与 checkbox accent/文件树 summary 与 copyButton/引用块 snippet 与状态/toggle）：`._failedItem_1ionb_87`、`._title_9cl6j_64`、`._pill_e3ygd_1`、`._close_15u5s_61`、`._warning_1nu42_19`、`._otherValue_4qrvp_117`、`._copyButton_4qrvp_143`、`._copyButton_10eou_142`、`._expand_10eou_191:hover`、`._copyButton_biesw_62`、`._expand_biesw_103:hover`、`._copyButton_srovd_22`、`._expand_srovd_85:hover`、`._summary_s66q0_30`、`._copyButton_s66q0_40`、`._expand_s66q0_100:hover`、`._markdown_1r4m5_5 li::marker`、`._markdown_1r4m5_5 input[type=checkbox]`（accent-color）、`._snippet_d4nqi_71`、`._empty_d4nqi_91`、`._status_d4nqi_121`、`._toggle_1ye18_5`；distCSS:1；color / accent-color

### `--dsw-alias-label-tertiary`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-600) / var(--dsw-static-neutral-bluish-400)
> 指向：`--dsw-static-neutral-bluish-600`、`--dsw-static-neutral-bluish-400`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 代理预设·预设描述（dsh-client-ui-agent-preset·_5QVD0a）：`._5QVD0a_desc`；client.js:261；color
  - 代理预设·预设卡介绍/组头/徽标/图标按钮/路径（dsh-client-ui-agent-preset·rtSEdW）：`.rtSEdW_intro`、`.rtSEdW_groupHead`、`.rtSEdW_badge`、`.rtSEdW_iconButton`、`.rtSEdW_revealedPath`；client.js:976；color
  - 附件·描述/加载出错文字（dsh-client-ui-attachment）：`.BInVoG_desc`；client.js:196；`.R_Yw7q_loading,.R_Yw7q_error`；client.js:618；color
  - 命令面板·详情/状态（dsh-client-ui-commands）：`.mufS8W_detail`、`.mufS8W_status`；client.js:875；color
  - 会话·消息根（dsh-client-ui-conversation·FJxK0a）：`.FJxK0a_root`；client.js:2808；color
  - 会话·用量统计（dsh-client-ui-conversation·JObwrW）：`.JObwrW_fill`（stroke）、`.JObwrW_headline`、`.JObwrW_segment`（background）；client.js:3036；color / stroke / background
  - 会话·撰写器禁用态（dsh-client-ui-conversation·uV2eYG）：`.uV2eYG_backdropDisabled,.uV2eYG_backdropDisabled :is(.uV2eYG_hlToken,.uV2eYG_hint,.uV2eYG_textRef,.uV2eYG_chip,.uV2eYG_chipInvalid)`；client.js:3463；color
  - 会话·选择器弹窗描述（dsh-client-ui-conversation·T1PP_q）：`.T1PP_q_desc`；client.js:4176；color
  - 会话·压缩区（dsh-client-ui-conversation·gdEzaW）：`.gdEzaW_referenceSummary`、`.gdEzaW_compactionSummary`、`.gdEzaW_compactionBody`、`.gdEzaW_retryRow`、`.gdEzaW_retryRow[data-active] .gdEzaW_retryText`（background 渐变 0%→100% 各段）、`.gdEzaW_turnErrorCode`；client.js:4254；color / background
  - 会话·附件目录卡字段值/条目描述（dsh-client-ui-conversation·NM4-hq）：`.NM4-hq_fieldValue`、`.NM4-hq_entryDescription`；client.js:4354；color
  - 会话·引用块来源/摘要/正文（dsh-client-ui-conversation·pC0e7a）：`.pC0e7a_source`、`.pC0e7a_summary`、`.pC0e7a_body`；client.js:4911；color
  - 会话·消息操作时间/操作（dsh-client-ui-conversation·p-xYUq）：`.p-xYUq_timeStart`、`.p-xYUq_timeEnd`、`.p-xYUq_action`、`.p-xYUq_action[data-unavailable]:hover`；client.js:5014；color
  - 会话·历史区提示（dsh-client-ui-conversation·Md3f7G）：`.Md3f7G_hint`；client.js:5452；color
  - 会话·审批卡命令（dsh-client-ui-conversation·bqrRRG）：`.bqrRRG_command`；client.js:6010；color
  - 会话·任务进度前导/进度/箭头（dsh-client-ui-conversation·lXshSW）：`.lXshSW_lead`、`.lXshSW_progress`、`.lXshSW_chevron`；client.js:6473；color
  - 会话·折叠面板（dsh-client-ui-conversation·_7yHdaG）：`._7yHdaG_header:focus-visible`（outline）、`._7yHdaG_lead`、`._7yHdaG_chevron`、`._7yHdaG_action`、`._7yHdaG_action:focus-visible`（outline）；client.js:6680；color / outline
  - 会话·会话头部面包屑/页签（dsh-client-ui-conversation·wSkVaW）：`.wSkVaW_crumb`、`.wSkVaW_tab`；client.js:7118；color
  - 会话·代码查看器空态（dsh-client-ui-conversation·ydkMvW）：`.ydkMvW_empty`；client.js:7429；color
  - 会话·思考行/命令行摘要与正文（dsh-client-ui-conversation·QWLzlG/_Xvjua）：`.QWLzlG_summary`、`.QWLzlG_thinkBody`；client.js:9350；`._Xvjua_summary`；client.js:9556；color
  - 会话·停止条（dsh-client-ui-conversation·Sxvs8a）：`.Sxvs8a_stopped`；client.js:9443；color
  - 插件面板·inspect/消息（dsh-client-ui-cordis·cvtE3a）：`.cvtE3a_inspect`、`.cvtE3a_message`；client.js:116；color
  - 插件面板·用途/源码页签（dsh-client-ui-cordis·gNWCoW）：`.gNWCoW_purpose`、`.gNWCoW_sourceTab`；client.js:211；color
  - 插件面板·运行行（dsh-client-ui-cordis·Nqubda）：`.Nqubda_badgeCount`、`.Nqubda_note,.Nqubda_readError`、`.Nqubda_rowId`、`.Nqubda_rowPurpose`、`.Nqubda_actionButton`；client.js:572；color
  - 交付物·标签/更多/显示文件夹（dsh-client-ui-deliverables）：`.P4kPIW_label`、`.P4kPIW_more`、`.P4kPIW_showFolder`；client.js:160；color
  - 目录选择·面包屑/箭头/编辑字形/行箭头（dsh-client-ui-directory-picker-browse）：`.ZuhsRW_crumb`、`.ZuhsRW_crumbChevron`、`.ZuhsRW_crumbEditGlyph`、`.ZuhsRW_rowChevron`；client.js:27；color
  - 目标面板·目标字形/图标按钮（dsh-client-ui-goal）：`.nLMEza_goalGlyph`、`.nLMEza_iconBtn`；client.js:11；color
  - 输入触发条·区块标题/项图标/项描述/组标题（dsh-client-ui-input-trigger）：`._3e4SsG_sectionTitle`、`._3e4SsG_itemIcon`、`._3e4SsG_itemDescription`、`._3e4SsG_groupTitle`；client.js:717；color
  - 任务列表·触发器/已结束行/状态与时长（dsh-client-ui-jobs）：`.QsffPG_trigger`、`.QsffPG_rowSettled`、`.QsffPG_status,.QsffPG_duration`；client.js:11；color
  - 消息反馈·操作/备注开关/取消/失败（dsh-client-ui-message-feedback）：`._8_XoUG_action`、`._8_XoUG_noteOpen`、`._8_XoUG_noteCancel`、`._8_XoUG_failure`；client.js:329；color
  - 模型选择·状态/空态/组标题/描述/单元格值/箭头（dsh-client-ui-model-selection）：`._7KE1Ra_status,._7KE1Ra_empty`、`._7KE1Ra_groupTitle`、`._7KE1Ra_description`、`._7KE1Ra_cellValue`、`._7KE1Ra_cellChevron`；client.js:234；color
  - 权限预设·描述（dsh-client-ui-permission-presets）：`.oY77xG_desc`；client.js:34；color
  - 模型设置·介绍/编辑路由/链接按钮/高级提示/目录元/空态/图标按钮/字段标签（dsh-client-ui-settings-models·zGbnIq）：`.zGbnIq_intro`、`.zGbnIq_editorRoute`、`.zGbnIq_linkButton`、`.zGbnIq_advancedHint`、`.zGbnIq_modelCatalogMeta,.zGbnIq_modelEmpty`、`.zGbnIq_iconButton`、`.zGbnIq_modelFieldLabel`；client.js:58；color
  - 插件清单·状态/失败/搜索/占位/目录标题/卡尾/状态点/箭头/详情 dt（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_status,.qSYn7G_failure`、`.qSYn7G_search`、`.qSYn7G_search input::placeholder`、`.qSYn7G_catalogHeading span`、`.qSYn7G_cardTrailing`、`.qSYn7G_statusDot`（background）、`.qSYn7G_chevron`、`.qSYn7G_details dt`；client.js:11；color / background
  - 插件设置·徽标弱化/禁用输入/提示/描述/箭头/只读/介绍/页签/空态（dsh-client-ui-settings-plugins）：`.At1oFq_badgeMuted`、`.At1oFq_input:disabled`、`.At1oFq_hint`；client.js:13；`.YyYd_a_description`、`.YyYd_a_chevron`、`.YyYd_a_readOnly`；client.js:155；`.pbvGtq_intro`、`.pbvGtq_tab`、`.pbvGtq_empty`；client.js:364；color
  - 技能·前导/摘要（dsh-client-ui-skill）：`.iWrAna_leading`、`.iWrAna_summary`；client.js:11；color
  - 子代理·触发器/祖先切换/展开/摘要/指标/提示与错误/框架（dsh-client-ui-subagent）：`.ZKlsPq_trigger,.ZKlsPq_switcherTrigger`、`.ZKlsPq_ancestorSwitcherTrigger`、`.ZKlsPq_ancestorSwitcherTrigger:hover,.ZKlsPq_ancestorSwitcherTrigger:focus-visible`、`.ZKlsPq_disclosure`、`.ZKlsPq_summary,.ZKlsPq_metrics`、`.ZKlsPq_notice,.ZKlsPq_error`；client.js:13；`.XJ7liG_frame`；client.js:682；color
  - 工具调用·摘要/后缀/搜索恢复/恢复/空态/前导（dsh-client-ui-tool）：`.o3BgMG_summary`、`.o3BgMG_summarySuffix`、`.o3BgMG_searchRecovery`；client.js:627；`.xDAfVq_recovery`、`.xDAfVq_empty`；client.js:977；`.CY-8Ka_leading`、`.CY-8Ka_summary`；client.js:1128；color
  - 轨迹视图·表头/轮次标签/工具调用/折叠/详情/概览/思考开关/架构参数/源块/工具目录/无负载等（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_table th`、`.Y0dWHa_turnLabel`、`.Y0dWHa_turnLabelActive`、`.Y0dWHa_subtoolAmber`、`.Y0dWHa_toolCallOnly`、`.Y0dWHa_collapsedTurnEllipsis`、`.Y0dWHa_detailsLocation`、`.Y0dWHa_detailTab`、`.Y0dWHa_overview dt`、`.Y0dWHa_thinkingToggle`、`.Y0dWHa_schemaParametersTitle`、`.Y0dWHa_sourceBlockLabel`、`.Y0dWHa_assistantToolCallArgs`、`.Y0dWHa_toolCatalogDescription`、`.Y0dWHa_noPayload`；client.js:2995；color
  - 轨迹视图·控制开关/操作/图标（dsh-client-ui-trajectory·fV0t5q）：`.fV0t5q_toggle`、`.fV0t5q_control`、`.fV0t5q_action`、`.fV0t5q_actionIcon`；client.js:5300；color
  - 用户提问·眉题/图标按钮/描述（dsh-client-ui-user-questions·Mbwy4a）：`.Mbwy4a_eyebrow`、`.Mbwy4a_iconButton`、`.Mbwy4a_description`；client.js:233；color
  - 工作流执行·运行前导/摘要/阶段前导/计数/分隔条/空态（dsh-client-ui-workflow-run·DBuyfa）：`.DBuyfa_runLeading`、`.DBuyfa_runSummary`、`.DBuyfa_phaseLeading`、`.DBuyfa_phaseCount`、`.DBuyfa_separator`（background）、`.DBuyfa_empty`；client.js:12；color / background
  - 工作区·搜索结果工作区/槽位/元信息/时间/图标按钮/区块头/占位/状态/警告/溢出/空态（dsh-client-ui-workspace）：`.YDXeBa_searchResultWorkspace`、`.YDXeBa_slot`、`.YDXeBa_meta`、`.YDXeBa_time`、`.YDXeBa_iconButton`；client.js:334；`.qDHVXG_sectionHeader`、`.qDHVXG_searchInput::placeholder`、`.qDHVXG_searchStatus,.qDHVXG_searchWarning`、`.qDHVXG_sessionOverflowButton`、`.qDHVXG_empty`；client.js:969；color
  - （dist 补充）基础组件库（boot 提示/弹窗前导/输入图标/菜单项图标与标签/预览省略/cwd/展开/空态/代码块计数与语言/gutter/间距/页脚/行号/文件数/图片 alt/引用块 published 与 truncated）：`._hint_1ionb_41`、`._leading_9cl6j_23`、`._icon_1ao1y_16`、`._itemIcon_19372_143`、`._label_19372_123`、`._previewEllipsis_4qrvp_133`、`._cwd_10eou_114`、`._expand_10eou_191`、`._empty_10eou_207`、`._count_biesw_50`、`._lang_biesw_55`、`._gutter_biesw_88`、`._expand_biesw_103`、`._gap_srovd_60`、`._expand_srovd_85`、`._footer_srovd_103`、`._lineNumber_s66q0_68`、`._fileCount_s66q0_95`、`._expand_s66q0_100`、`._empty_s66q0_116`、`._imageAlt_1r4m5_268`、`._published_d4nqi_79`、`._truncated_d4nqi_85`；distCSS:1；color
  - （dist JS 补充）distJS ANSI 颜色映射（亮黑/灰 85,85,85 → 该变量）；distJS:56

### `--dsw-alias-markdown-citation`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-100) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-100`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 轨迹视图·思考引用块左边框（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_thinkingQuote`；client.js:2995；border-left

### `--dsw-alias-markdown-code-block`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-50) / var(--dsw-static-neutral-bluish-900)
> 指向：`--dsw-static-neutral-bluish-50`、`--dsw-static-neutral-bluish-900`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 会话·引用块正文/代码查看器/命令行正文底色（dsh-client-ui-conversation）：`.pC0e7a_body`；client.js:4911；`.ydkMvW_code`；client.js:7429；`._Xvjua_body`；client.js:9556；background
  - 插件面板·inspect 输出/详情卡输出（dsh-client-ui-cordis）：`.cvtE3a_output`；client.js:116；`.gNWCoW_output`；client.js:211；background
  - 技能·说明卡底色（dsh-client-ui-skill）：`.iWrAna_instructionsCard`；client.js:11；background
  - 工具调用·IO 卡/代码/IO 卡底色（dsh-client-ui-tool）：`.o3BgMG_ioCard`；client.js:627；`.xDAfVq_code`；client.js:977；`.CY-8Ka_ioCard`；client.js:1128；background
  - 轨迹视图·载荷区底色（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_payload`；client.js:2995；background
  - （dist 补充）基础代码块组件（命令块/文件树块/diff 块/shiki 块/引用块/文件路径块/toggle body）：`._block_10eou_7`、`._copyButton_10eou_142`（background-color）、`._block_biesw_7`、`._block_srovd_7`、`._block_s66q0_7`、`._block_178r4_4`、`._block_178r4_4 :where(pre)`、`._block_178r4_4 :where(pre._shiki_178r4_84)`（!important）、`._block_d4nqi_7`、`._body_1ye18_20`；distCSS:1；background

### `--dsw-alias-markdown-code-block-banner`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-50) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-50`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 技能·说明卡头部底色（dsh-client-ui-skill）：`.iWrAna_instructionsHeader`；client.js:11；background
  - （dist 补充）代码块·banner 条/文件头底色：`._banner_biesw_21`、`._header_s66q0_20`；distCSS:1；background
  - （dist 补充）shiki 代码块·自定义属性：`._block_178r4_4`；distCSS:1；`--dsl-code-block-banner-background-color`

### `--dsw-alias-markdown-code-segment-selected`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-00) / var(--dsw-static-neutral-bluish-800)
> 指向：`--dsw-static-neutral-bluish-00`、`--dsw-static-neutral-bluish-800`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-markdown-code-segment-unselected`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-75) / var(--dsw-static-neutral-bluish-900)
> 指向：`--dsw-static-neutral-bluish-75`、`--dsw-static-neutral-bluish-900`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-markdown-inline-code`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-100) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-100`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （仅 dist）markdown 渲染器·行内代码底色：`._markdown_1r4m5_5 :not(pre)>code`；distCSS:1；background-color（client.js 0 命中）

### `--dsw-alias-markdown-placeholder`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-60) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-60`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-markdown-tag`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-75) / var(--dsw-static-neutral-bluish-850)
> 指向：`--dsw-static-neutral-bluish-75`、`--dsw-static-neutral-bluish-850`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-scrollbar-bg-l1`
- 值（浅色 / 深色）：var(--dsw-static-neutral-200) / var(--dsw-static-neutral-700)
> 指向：`--dsw-static-neutral-200`、`--dsw-static-neutral-700`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-scrollbar-bg-l2`
- 值（浅色 / 深色）：var(--dsw-static-neutral-200) / var(--dsw-static-neutral-600)
> 指向：`--dsw-static-neutral-200`、`--dsw-static-neutral-600`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 代理预设·预设卡查看器代码区（dsh-client-ui-agent-preset）：`.rtSEdW_viewerCode`；client.js:976；`--dsh-scrollbar-thumb`
  - 附件·缩略图轨道（dsh-client-ui-attachment）：`.JVDQca_rail`；client.js:27
  - 命令面板·卡片（dsh-client-ui-commands）：`.mufS8W_card`；client.js:875
  - 会话·撰写器卡/审批卡/任务进度根/折叠面板（dsh-client-ui-conversation）：`.uV2eYG_card`；client.js:3463；`.bqrRRG_card`；client.js:6010；`.lXshSW_root`；client.js:6473；`._7yHdaG_panel`；client.js:6680
  - 插件面板·运行列表面板（dsh-client-ui-cordis）：`.Nqubda_panel`；client.js:572
  - 目录选择·对话框（dsh-client-ui-directory-picker-browse）：`.ZuhsRW_dialog.ZuhsRW_dialog`；client.js:27
  - 输入触发条·菜单（dsh-client-ui-input-trigger）：`._3e4SsG_menu`；client.js:717
  - 任务列表·菜单（dsh-client-ui-jobs）：`.QsffPG_menu`；client.js:11
  - 消息反馈·备注面板（dsh-client-ui-message-feedback）：`._8_XoUG_notePanel`；client.js:329
  - 模型选择·菜单（dsh-client-ui-model-selection）：`._7KE1Ra_menu`；client.js:234
  - 设置面板·面板（dsh-client-ui-settings-general）：`.VOzbGW_panel`；client.js:28
  - 模型设置·抓取对话框（dsh-client-ui-settings-models）：`.zGbnIq_fetchDialog`；client.js:58
  - 侧边栏·根（dsh-client-ui-sidebar）：`.hHd-Xa_root`；client.js:26
  - 子代理·菜单（dsh-client-ui-subagent）：`.ZKlsPq_menu`；client.js:13
  - 轨迹视图·分栏/摘要滚动区 hover（dsh-client-ui-trajectory）：`.Y0dWHa_split`、`.Y0dWHa_summaryScrollRegion:hover,.Y0dWHa_summaryScrollRegion:focus-within`；client.js:2995
  - 用户提问·卡片（dsh-client-ui-user-questions）：`.LVzXQa_card`；client.js:115；`.Mbwy4a_card`；client.js:233
  - （dist 补充）基础菜单·列表/子菜单：`._list_19372_8,._submenu_19372_9`；distCSS:1

### `--dsw-alias-scrollbar-hover-l1`
- 值（浅色 / 深色）：var(--dsw-static-neutral-300) / var(--dsw-static-neutral-600)
> 指向：`--dsw-static-neutral-300`、`--dsw-static-neutral-600`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-scrollbar-hover-l2`
- 值（浅色 / 深色）：var(--dsw-static-neutral-300) / var(--dsw-static-neutral-550)
> 指向：`--dsw-static-neutral-300`、`--dsw-static-neutral-550`（浅深分别见上）
- **直接引用的 UI 元素**：
  - dsh-client-ui-agent-preset `.rtSEdW_viewerCode`:976；dsh-client-ui-attachment `.JVDQca_rail`:27；dsh-client-ui-commands `.mufS8W_card`:875；dsh-client-ui-conversation `.uV2eYG_card`:3463 / `.bqrRRG_card`:6010 / `.lXshSW_root`:6473 / `._7yHdaG_panel`:6680；dsh-client-ui-cordis `.Nqubda_panel`:572；dsh-client-ui-directory-picker-browse `.ZuhsRW_dialog`:27；dsh-client-ui-input-trigger `._3e4SsG_menu`:717；dsh-client-ui-jobs `.QsffPG_menu`:11；dsh-client-ui-message-feedback `._8_XoUG_notePanel`:329；dsh-client-ui-model-selection `._7KE1Ra_menu`:234；dsh-client-ui-settings-general `.VOzbGW_panel`:28；dsh-client-ui-settings-models `.zGbnIq_fetchDialog`:58；dsh-client-ui-sidebar `.hHd-Xa_root`:26；dsh-client-ui-subagent `.ZKlsPq_menu`:13；dsh-client-ui-trajectory `.Y0dWHa_split`、`.Y0dWHa_summaryScrollRegion:hover,.Y0dWHa_summaryScrollRegion:focus-within`:2995；dsh-client-ui-user-questions `.LVzXQa_card`:115 / `.Mbwy4a_card`:233；distCSS `._list_19372_8,._submenu_19372_9`:1；属性 `--dsh-scrollbar-thumb-hover`

### `--dsw-alias-state-business-primary`
- 值（浅色 / 深色）：var(--dsw-static-deepseek-500) / var(--dsw-static-deepseek-400)
> 指向：`--dsw-static-deepseek-500`、`--dsw-static-deepseek-400`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （dist）基础 markdown 渲染器·链接/文件提及/表格滚动焦点：`._markdown_1r4m5_5 a`（color）、`._markdown_1r4m5_5 a:hover,._markdown_1r4m5_5 a:focus`（text-decoration）、`._markdown_1r4m5_5 a:focus-visible`（box-shadow）、`._tableScroll_1r4m5_174:focus-visible`（box-shadow）、`._fileMention_1r4m5_288`（color）、`._fileMention_1r4m5_288:hover,._fileMention_1r4m5_288:focus`（text-decoration）、`._sourceLink_d4nqi_60`、`._fetchUrl_d4nqi_103`；distCSS:1
  - （dist）基础组件·焦点轮廓：`._copyable_1b2ny_25:focus-visible`、`._copyButton_4qrvp_143:focus-visible`；distCSS:1；outline
  - （dist JS 补充）ANSI 蓝色映射；distJS:56
  - 会话·撰写器（dsh-client-ui-conversation·uV2eYG）：`.uV2eYG_cardWorkspaceTrigger:hover:after`（background）、`.uV2eYG_pending`（background）、`.uV2eYG_input`（caret-color）、`.uV2eYG_textRef`、`.uV2eYG_chip`（color）；client.js:3463
  - 会话·压缩引用 chip（dsh-client-ui-conversation·gdEzaW）：`.gdEzaW_refChip`；client.js:4254；color
  - 会话·任务进度进行中字形（dsh-client-ui-conversation·lXshSW）：`.lXshSW_glyphProgress`；client.js:6473；color
  - 会话·折叠面板编辑器焦点（dsh-client-ui-conversation·_7yHdaG）：`._7yHdaG_editor:focus`；client.js:6680；border-color
  - 会话·会话头部激活页签（dsh-client-ui-conversation·wSkVaW）：`.wSkVaW_tabActive`（color）、`.wSkVaW_tabActive:after`（background）；client.js:7118
  - 插件面板·inspect 图标/标题/分隔条（dsh-client-ui-cordis·cvtE3a）：`.cvtE3a_icon`、`.cvtE3a_title`、`.cvtE3a_separator`；client.js:116；color / background
  - 插件面板·详情卡标题/箭头/分隔条/激活页签/焦点（dsh-client-ui-cordis·gNWCoW）：`.gNWCoW_card .gNWCoW_title,.gNWCoW_card .gNWCoW_chevron`、`.gNWCoW_separator`（background）、`.gNWCoW_sourceTabActive`、`.gNWCoW_sourceTabActive:after`（background）、`.gNWCoW_sourceTab:focus-visible`（outline）；client.js:211
  - 插件面板·等待审批行边框（dsh-client-ui-cordis·Nqubda）：`.Nqubda_row[data-cordis-awaiting]`；client.js:572；border-color
  - 目标面板·输入焦点边框（dsh-client-ui-goal）：`.nLMEza_objectiveInput:focus`；client.js:11；border-color
  - 插件清单·搜索输入焦点/卡片焦点/加载状态点（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_search input:focus-visible`（border-color + box-shadow）、`.qSYn7G_cardContent:focus-visible`（outline）、`.qSYn7G_statusDot[data-phase=loading]`（background）；client.js:11
  - 插件设置·页签焦点轮廓（dsh-client-ui-settings-plugins）：`.pbvGtq_tab:focus-visible`；client.js:364；outline
  - 工具调用·cordis_ 前缀工具标题/分隔（dsh-client-ui-tool）：`.o3BgMG_root[data-tool^=cordis_] .o3BgMG_leading,.o3BgMG_root[data-tool^=cordis_] .o3BgMG_title`（color）、`.o3BgMG_root[data-tool^=cordis_] .o3BgMG_sep`（background）；client.js:627
  - 轨迹视图·历史加载/表格/详情页签/概览/思考/源块/工具目录焦点与激活（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_historyLoadingSpinner`（border-top-color）、`.Y0dWHa_historyLoadButton:focus-visible`（outline）、`.Y0dWHa_table tbody tr:not([data-collapsed-summary]):focus-visible`（box-shadow）、`.Y0dWHa_table tbody tr[data-collapsed-summary]:focus-visible`（box-shadow）、`.Y0dWHa_user`（color）、`.Y0dWHa_detailTabActive`（color）、`.Y0dWHa_detailTabActive:after`（background）、`.Y0dWHa_close:focus-visible,.Y0dWHa_detailTab:focus-visible`（outline）、`.Y0dWHa_overviewHierarchyNavLink:focus-visible`（outline）、`.Y0dWHa_timestampToggle:focus-visible`（outline）、`.Y0dWHa_overviewTitle:focus-visible`（outline）、`.Y0dWHa_overviewTitle:focus-visible .Y0dWHa_overviewTitleIcon`（color）、`.Y0dWHa_thinkingToggle:focus-visible`（outline）、`.Y0dWHa_sourceBlockJumpTarget:focus-visible .Y0dWHa_sourceBlockJumpIcon`（color）、`.Y0dWHa_assistantToolCallButton:focus-visible`（outline）、`.Y0dWHa_toolCatalogSummary:focus-visible`（outline）；client.js:2995
  - 轨迹视图·控制开关/搜索（dsh-client-ui-trajectory·fV0t5q）：`.fV0t5q_toggle:focus-visible`、`.fV0t5q_control:focus-visible`、`.fV0t5q_action:focus-visible`（outline）、`.fV0t5q_controlTrack[data-on=true]`（background）、`.fV0t5q_search:focus-within`（border-color）；client.js:5300
  - 轨迹视图·时间轴（dsh-client-ui-trajectory·_1p9O6q）：`._1p9O6q_track:focus-visible`（outline）、`._1p9O6q_span[data-timeline-span=user]`（background）、`._1p9O6q_span[data-hovered=true]:not([data-current=true])`（box-shadow）、`._1p9O6q_span[data-current=true]`（box-shadow）、`._1p9O6q_selection`（background color-mix）、`._1p9O6q_hoverLine`（background）、`._1p9O6q_selectionEdges:before,._1p9O6q_selectionEdges:after`（background）、`._1p9O6q_selection[data-dragging=true]`（background color-mix）；client.js:5552
  - 用户提问·输入光标/自定义块焦点（dsh-client-ui-user-questions·Mbwy4a）：`.Mbwy4a_fieldInput`（caret-color）、`.Mbwy4a_customBlock:focus-within`（border-color）；client.js:233
  - 工作流执行·运行/阶段头焦点/成员按钮（dsh-client-ui-workflow-run·DBuyfa）：`.DBuyfa_runHeader:focus-visible`、`.DBuyfa_phaseHeader:focus-visible`（outline）、`.DBuyfa_memberButton .DBuyfa_memberLabel`（color）、`.DBuyfa_memberButton:focus-visible .DBuyfa_memberLabelWrap`（outline）；client.js:12
  - 工作区·激活文件夹/拖放指示（dsh-client-ui-workspace）：`.YDXeBa_folderActive`（color）、`.YDXeBa_sessionRow.YDXeBa_dropBefore:before,.YDXeBa_sessionRow.YDXeBa_dropAfter:after`（background 拖放指示渐变）、`.qDHVXG_listTopDropIndicator,.qDHVXG_workspaceDropBefore:before,.qDHVXG_workspaceDropAfter:after`（background）；client.js:334,969

### `--dsw-alias-state-business-tertiary`
- 值（浅色 / 深色）：var(--dsw-static-deepseek-100) / var(--dsw-static-deepseek-800)
> 指向：`--dsw-static-deepseek-100`、`--dsw-static-deepseek-800`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 会话·工作区选择器预览徽标底（dsh-client-ui-conversation·pXSMma）：`.pXSMma_previewBadge`；client.js:6949；background
  - 轨迹视图·用户行底（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_user`；client.js:2995；background

### `--dsw-alias-state-error-primary`
- 值（浅色 / 深色）：var(--dsw-static-red-600) / var(--dsw-static-red-400)
> 指向：`--dsw-static-red-600`、`--dsw-static-red-400`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （dist）基础组件：状态点 error（`._dot_10orb_3[data-state=error]`）、菜单危险项（`._danger_19372_193,._danger_19372_193 ._itemIcon_19372_143`）、警告图标（`._warningIcon_1nu42_32`）、错误 banner（`._banner_ugy7y_1` background）、复制按钮失败态（`._copyButton_4qrvp_143[data-state=failed]`）、命令状态（`._status_10eou_134`）、diff 删除行（`._del_srovd_67`、`._del_srovd_67:before`）；distCSS:1；color / background
  - （dist JS 补充）ANSI 红色映射；distJS:56
  - 代理预设·预设卡损坏态/删除确认（dsh-client-ui-agent-preset·rtSEdW）：`.rtSEdW_cardBroken,.rtSEdW_cardBroken:hover`（border-color）、`.rtSEdW_brokenBadge`（background）、`.rtSEdW_cardBrokenReason`、`.rtSEdW_iconDanger:hover:not(:disabled)`、`.rtSEdW_error`、`.rtSEdW_deleteConfirm:not(:disabled)`（border-color + color）；client.js:976
  - 命令面板·错误（dsh-client-ui-commands）：`.mufS8W_error`；client.js:875；color
  - 会话·无效 chip/轮转错误标题/打开错误/拒绝 hover/模态错误/代码出错/命令行出错（dsh-client-ui-conversation）：`.uV2eYG_chipInvalid`；client.js:3463；`.gdEzaW_turnErrorTitle`；client.js:4254；`.Md3f7G_openError`；client.js:5452；`.bqrRRG_reject:hover:not(:disabled)`；client.js:6010；`.pXSMma_modalError`；client.js:6949；`.ydkMvW_code[data-error]`；client.js:7429；`._Xvjua_summary[data-error],._Xvjua_body[data-error]`；client.js:9556；color
  - 插件面板·错误/失败状态/请求错误/输出出错/读取错误/失败行/行错误（dsh-client-ui-cordis）：`.cvtE3a_error`、`.cvtE3a_card[data-cordis-status=failed] .cvtE3a_status`；client.js:116；`.gNWCoW_errorSummary`、`.gNWCoW_requestError`、`.gNWCoW_output[data-error]`；client.js:211；`.Nqubda_readError`、`.Nqubda_row[data-cordis-status=failed] .Nqubda_rowStatus`、`.Nqubda_rowError`；client.js:572；color
  - 目录选择·错误（dsh-client-ui-directory-picker-browse）：`.ZuhsRW_error`；client.js:27；color
  - 目标面板·错误（dsh-client-ui-goal）：`.nLMEza_error`；client.js:11；color
  - 模型选择·错误/警告（dsh-client-ui-model-selection）：`._7KE1Ra_error,._7KE1Ra_warning`；client.js:234；color
  - 计划·错误（dsh-client-ui-plan）：`.rS3zOq_error`；client.js:11；color
  - 设置面板·错误（dsh-client-ui-settings-general）：`.me01iq_error`；client.js:303；color
  - 模型设置·凭据缺失点/危险按钮/错误/删除确认/复制错误（dsh-client-ui-settings-models）：`.zGbnIq_credentialDotMissing`（background）、`.zGbnIq_dangerButton`、`.zGbnIq_iconButtonDanger:hover:not(:disabled)`、`.zGbnIq_error`、`.zGbnIq_deleteConfirm:not(:disabled)`（border-color + color）；client.js:58；`.t1T8VW_error`；client.js:2265；color
  - 插件清单·失败状态/失败状态点（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_failure`、`.qSYn7G_statusDot[data-phase=failed]`（background）；client.js:11
  - 技能·错误摘要/出错说明（dsh-client-ui-skill）：`.iWrAna_errorSummary`、`.iWrAna_instructions[data-error]`；client.js:11；color
  - 子代理·错误（dsh-client-ui-subagent）：`.ZKlsPq_error`；client.js:13；color
  - 工具调用·错误摘要/IO 出错/代码出错（dsh-client-ui-tool）：`.o3BgMG_errorSummary`、`.o3BgMG_ioText[data-error]`；client.js:627；`.xDAfVq_code[data-error]`；client.js:977；`.CY-8Ka_ioText[data-error]`、`.CY-8Ka_errorSummary`；client.js:1128；color
  - 轨迹视图·错误请求边界/错误行/提示差异删除行/错误载荷 JSON 树（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_requestBoundaryControl[data-request-status=error]:before,.Y0dWHa_requestBoundaryControl[data-request-status=error]:hover:before,.Y0dWHa_requestBoundaryControl[data-request-status=error]:focus-visible:before`（background）、`.Y0dWHa_table tbody tr[data-error=true] .Y0dWHa_turnRail`（background color-mix）、`.Y0dWHa_table tbody tr[data-error=true] .Y0dWHa_selectionRail`（background）、`.Y0dWHa_promptDiffLineremoved`（color + background color-mix）、`.Y0dWHa_error,.Y0dWHa_overview dd.Y0dWHa_error,.Y0dWHa_details .Y0dWHa_errorPayload`（color）、`.Y0dWHa_details .Y0dWHa_jsonPayload.Y0dWHa_errorPayload,.Y0dWHa_details .Y0dWHa_jsonPreview.Y0dWHa_errorPayload`（`--json-tree-property/-string/-number/-keyword/-punctuation/-icon` 自定义属性）；client.js:2995
  - 轨迹视图·时间轴错误 span（dsh-client-ui-trajectory·_1p9O6q）：`._1p9O6q_span[data-error=true]`；client.js:5552；background
  - 用户提问·反馈（dsh-client-ui-user-questions）：`.LVzXQa_feedback`；client.js:115；`.Mbwy4a_feedback`；client.js:233；color
  - 工作区·模态错误/重命名错误/删除操作（dsh-client-ui-workspace）：`._G5b-a_modalError`；client.js:799；`.qDHVXG_renameError`、`.qDHVXG_deleteAction:not(:disabled)`；client.js:969；color
  - 主题设置面板·主题色选择项（dsh-client-ui-theme·JS）：`name: "--dsw-alias-state-error-primary"`；client.js:1072；`cssVariable: "--dsw-alias-state-error-primary"`；client.js:1076

### `--dsw-alias-state-error-secondary`
- 值（浅色 / 深色）：var(--dsw-static-red-400) / var(--dsw-static-red-400)（浅深相同）
> 指向：`--dsw-static-red-400`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 轨迹视图·助手紫色高亮行（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_assistantVioletBright`（color color-mix + background color-mix）；client.js:2995
  - 轨迹视图·时间轴 message span（dsh-client-ui-trajectory·_1p9O6q）：`._1p9O6q_span[data-timeline-span=message]`；client.js:5552；`--trajectory-assistant-decoding-color`
  - （dist JS 补充）ANSI 亮红映射：`"255,85,85":"var(--dsw-alias-state-error-secondary)"`；distJS:56

### `--dsw-alias-state-success-primary`
- 值（浅色 / 深色）：var(--dsw-static-green-500) / var(--dsw-static-green-500)（浅深相同）
> 指向：`--dsw-static-green-500`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （dist）状态点 done / diff 添加行：`._dot_10orb_3[data-state=done]`、`._add_srovd_76`、`._add_srovd_76:before`；distCSS:1；color
  - （dist JS 补充）ANSI 绿色映射；distJS:56
  - 会话·任务进度完成字形（dsh-client-ui-conversation·lXshSW）：`.lXshSW_glyphCompleted`；client.js:6473；color
  - 插件面板·running 状态（dsh-client-ui-cordis）：`.cvtE3a_card[data-cordis-status=running] .cvtE3a_status`；client.js:116；`.Nqubda_row[data-cordis-status=running] .Nqubda_rowStatus`；client.js:572；color
  - 模型设置·已保存提示/凭据已配置点（dsh-client-ui-settings-models）：`.zGbnIq_savedNotice`、`.zGbnIq_credentialDotConfigured`（background）；client.js:58
  - 插件清单·激活状态点/启用配置标签（dsh-client-ui-settings-plugin-inventory）：`.qSYn7G_statusDot[data-phase=active]`（background）、`.qSYn7G_configTag[data-enabled=true]`（background color-mix + color）；client.js:11
  - 轨迹视图·上下文绿行/提示差异添加行（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_contextGreen`（color color-mix）、`.Y0dWHa_promptDiffLineadded`（color color-mix）；client.js:2995
  - 轨迹视图·时间轴 context span（dsh-client-ui-trajectory·_1p9O6q）：`._1p9O6q_span[data-timeline-span=context]`（background color-mix）；client.js:5552
  - 主题设置面板·主题色选择项（dsh-client-ui-theme·JS）：`name: "--dsw-alias-state-success-primary"`；client.js:1079；`cssVariable: "--dsw-alias-state-success-primary"`；client.js:1083

### `--dsw-alias-state-success-secondary`
- 值（浅色 / 深色）：var(--dsw-static-green-400) / var(--dsw-static-green-400)（浅深相同）
> 指向：`--dsw-static-green-400`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （仅 dist JS）distJS 内 ANSI 颜色映射（亮绿 0,255,0 → 该变量）：`"0,255,0":"var(--dsw-alias-state-success-secondary)"`；distJS:56（JS 对象映射，供 ANSI 彩色输出渲染；client.js 0 命中）

### `--dsw-alias-state-success-tertiary`
- 值（浅色 / 深色）：var(--dsw-static-green-100) / var(--dsw-static-green-900)
> 指向：`--dsw-static-green-100`、`--dsw-static-green-900`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 插件面板·running 行状态徽标底（dsh-client-ui-cordis·Nqubda）：`.Nqubda_row[data-cordis-status=running] .Nqubda_rowStatus`；client.js:572；background
  - 轨迹视图·上下文绿行/提示差异添加行底（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_contextGreen`、`.Y0dWHa_promptDiffLineadded`；client.js:2995；background

### `--dsw-alias-state-warn-label`
- 值（浅色 / 深色）：var(--dsw-static-amber-600) / var(--dsw-static-amber-600)（浅深相同）
> 指向：`--dsw-static-amber-600`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （dist）toast·警示图标：`._icon_fvpz7_35`；distCSS:1；color
  - 会话·撰写器高亮 token（dsh-client-ui-conversation·uV2eYG）：`.uV2eYG_hlToken`；client.js:3463；color
  - 插件面板·等待审批/客户端等待状态（dsh-client-ui-cordis）：`.cvtE3a_card[data-cordis-status=awaiting-approval] .cvtE3a_status,.cvtE3a_card[data-cordis-status=client-pending] .cvtE3a_status`；client.js:116；`.Nqubda_row[data-cordis-status=awaiting-approval] .Nqubda_rowStatus,.Nqubda_row[data-cordis-status=client-pending] .Nqubda_rowStatus`；client.js:572；color
  - 模型选择·警告（dsh-client-ui-model-selection）：`._7KE1Ra_warning`；client.js:234；color
  - 计划·chip 文字/焦点轮廓（dsh-client-ui-plan）：`.rS3zOq_chip`（color）、`.rS3zOq_chip:focus-visible`（outline）；client.js:11
  - 模型设置·提示（dsh-client-ui-settings-models）：`.zGbnIq_notice`；client.js:58；color
  - 轨迹视图·工具琥珀行/子工具琥珀行（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_toolAmber`（color）、`.Y0dWHa_subtoolAmber`（color color-mix）；client.js:2995
  - 轨迹视图·时间轴 tool/subtool span（dsh-client-ui-trajectory·_1p9O6q）：`._1p9O6q_span[data-timeline-span=tool],._1p9O6q_span[data-timeline-span=subtool]`；client.js:5552；background

### `--dsw-alias-state-warn-primary`
- 值（浅色 / 深色）：var(--dsw-static-amber-500) / var(--dsw-static-amber-500)（浅深相同）
> 指向：`--dsw-static-amber-500`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （dist）状态点 warning：`._dot_10orb_3[data-state=warning]`；distCSS:1；color
  - （dist JS 补充）ANSI 黄色映射；distJS:56
  - 会话·最大 token 标题/审批卡警示条与点（dsh-client-ui-conversation）：`.gdEzaW_maxTokensTitle`；client.js:4254；`.bqrRRG_strip`（color）、`.bqrRRG_dot`（background）；client.js:6010
  - 计划·chip hover（dsh-client-ui-plan）：`.rS3zOq_chip:hover:not(:disabled)`；client.js:11；color
  - 用户提问·警示条/点（dsh-client-ui-user-questions·LVzXQa）：`.LVzXQa_strip`（color）、`.LVzXQa_dot`（background）；client.js:115
  - 主题设置面板·主题色选择项（dsh-client-ui-theme·JS）：`name: "--dsw-alias-state-warn-primary"`；client.js:1086；`cssVariable: "--dsw-alias-state-warn-primary"`；client.js:1090

### `--dsw-alias-state-warn-secondary`
- 值（浅色 / 深色）：var(--dsw-static-amber-400) / var(--dsw-static-amber-400)（浅深相同）
> 指向：`--dsw-static-amber-400`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 会话·审批卡边框（dsh-client-ui-conversation·bqrRRG）：`.bqrRRG_card`；client.js:6010；border
  - 用户提问·问题卡边框（dsh-client-ui-user-questions·LVzXQa）：`.LVzXQa_card`；client.js:115；border
  - （dist JS 补充）ANSI 亮黄映射：`"255,255,85":"var(--dsw-alias-state-warn-secondary)"`；distJS:56

### `--dsw-alias-state-warn-tertiary`
- 值（浅色 / 深色）：var(--dsw-static-amber-100) / var(--dsw-static-amber-900)
> 指向：`--dsw-static-amber-100`、`--dsw-static-amber-900`（浅深分别见上）
- **直接引用的 UI 元素**：
  - 会话·审批卡警示条底（dsh-client-ui-conversation·bqrRRG）：`.bqrRRG_strip`；client.js:6010；background
  - 插件面板·等待审批/客户端等待状态徽标底（dsh-client-ui-cordis·Nqubda）：`.Nqubda_row[data-cordis-status=awaiting-approval] .Nqubda_rowStatus,.Nqubda_row[data-cordis-status=client-pending] .Nqubda_rowStatus`；client.js:572；background
  - 计划·chip 底（dsh-client-ui-plan）：`.rS3zOq_chip`；client.js:11；background
  - 轨迹视图·工具琥珀行/子工具琥珀行底（dsh-client-ui-trajectory·Y0dWHa）：`.Y0dWHa_toolAmber`、`.Y0dWHa_subtoolAmber`（background color-mix）；client.js:2995
  - 用户提问·警示条底（dsh-client-ui-user-questions·LVzXQa）：`.LVzXQa_strip`；client.js:115；background

### `--dsw-alias-toast-bg`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-800) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-neutral-bluish-800`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：无（仅被其他变量定义引用）

### `--dsw-alias-tooltip-bg`
- 值（浅色 / 深色）：var(--dsw-static-neutral-bluish-850) / var(--dsw-static-neutral-bluish-750)
> 指向：`--dsw-static-neutral-bluish-850`、`--dsw-static-neutral-bluish-750`（浅深分别见上）
- **直接引用的 UI 元素**：
  - （仅 dist）基础 tooltip 气泡：`._bubble_owhem_8`；distCSS:1；background（`position:fixed;z-index:100;width:max-content;max-width:50vw;padding:3px 7px;border-radius:8px;background:var(--dsw-alias-tooltip-bg);color:var(--dsw-static-neutral-bluish-00)`）。注：轨迹视图内的自定义 tooltip（`.Y0dWHa_kindSlot [role=tooltip]`）使用的是 `--dsw-alias-bg-layer-2`，不引用本变量

### 全局注记（子代理审计要点，不属于单个变量）

- 0 命中的 8 个变量（interactive-bg-hover-accent / markdown-code-segment-selected / markdown-code-segment-unselected / markdown-placeholder / markdown-tag / scrollbar-bg-l1 / scrollbar-hover-l1 / toast-bg）仅在 theme 定义行（L121/L124/L127/L133 的 CSS 表字符串）中出现，按排除规则全部忽略，即**无直接引用**。
- `--dsw-alias-scrollbar-bg-l2` / `--dsw-alias-scrollbar-hover-l2` 的全部 22 处为各组件滚动容器内的 `--dsh-scrollbar-thumb` / `--dsh-scrollbar-thumb-hover` 自定义属性赋值（间接滚动条样式消费链），属性为自定义属性而非 background；真正把 `--dsh-scrollbar-thumb` 画成滚动条的是 theme 定义行 L127（忽略）。另发现 sidebar（`.hHd-Xa_root.hHd-Xa_quietBars`）与 trajectory（`.Y0dWHa_summaryScrollRegion` 非 hover）把 `--dsh-scrollbar-thumb` 覆盖为 `transparent`（间接用法，不引用本变量）。
- `--dsw-alias-label-primary` / `label-secondary` / `label-tertiary` 在 theme 包 L1058–1090 的 `name:`/`cssVariable:` 命中属于**主题设置面板·主题色选择项**（JS 使用），非 CSS。
- distJS:56 的命中全部来自同一段 ANSI 16 色 → CSS 变量映射对象（`const xf={"0,0,0":"var(--dsw-alias-label-primary)",...}`，用于终端/ANSI 彩色输出渲染），属 JS 使用。


## 附录 A：`--dsw-hovercard-bg`（组件局部变量，不在 static/specific/alias 体系内）

- **定义与使用**（仅存在于 web shell 的 dist 产物，client.js 中无对应）：`dsh-web-frontend/dist/assets/index-C6eRlFa6.css` 中 `._card_1b2ny_13` 规则：
  `._card_1b2ny_13{--dsw-hovercard-bg:#2C2C2E;position:fixed;z-index:100;width:244px;padding:12px 16px;border-radius:12px;background:var(--dsw-hovercard-bg);box-shadow:var(--dsw-shadow-lv3)}`
- **所属组件**：`@deepseek-ai/dsh-client-ui-primitives` 包的 HoverCard 悬浮卡片原语（dist JS 导出表 `HoverCard:tf`；同模块类 `_root/_copyable/_feedback/_copied/_status`）。锚点右侧 fixed 悬浮、宽 244px、可点击复制（"复制/复制成功"）。
- **实际使用方**：dsh-client-ui-workspace 的会话行 —— workspace:538 `WorkspaceHoverContent`（label/cwd/createdAt）、workspace:717 `SessionHoverContent`（会话摘要 + 复制会话标题）。
- **浅深**：值为固定 `#2C2C2E`，浅色/深色相同，不随主题切换。

## 附录 B：被排除的非颜色 `--dsw-*` 变量（仅供对照，不属于颜色变量审计范围）

- `--dsw-font-*`（含 `--dsw-font-family`、`--dsw-font-markdown-*`、`--dsw-font-xs-13` 等全部字体令牌）：字体复合值/字重/字号/行高。
- `--dsw-shadow-lv1/1-blur/2/3`：阴影复合值（内部含颜色分量）。
- `--dsw-mask-blur`：`blur()` 滤镜值。
- `--dsw-linear-gradient-think` / `--dsw-linear-think-select`：渐变复合值。
- `--dsh-*` 系列（`--dsh-scrollbar-thumb`、`--dsh-scrollbar-width`、`--dsh-composer-*`、`--dsh-state-*`、`--dsh-boot-*` 等）：非 dsw 前缀的运行时/工具变量。

## 附录 C：统计口径修订

- 变量全集：体系内 162 个（static 73 + specific 11 + alias 78），体系外 1 个（`--dsw-hovercard-bg`），合计 163。
- **有直接 UI 引用的变量：77** = 体系内 76（static 8 + specific 9 + alias 59，其中 alias-1 组 28 + alias-2 组 31）+ 体系外 hovercard 1。
- 无直接引用：86（全部为体系内变量；它们仅存在于 theme 定义表或被其他变量定义 var() 引用）。
- **仅存在于 dist shell 组件**（client.js 无对应命中）的变量共 10 个：static 3（`--dsw-static-blue-400`、`--dsw-static-deepseek-450`、`--dsw-static-neutral-bluish-00`）、alias 6（`--dsw-alias-button-ghost-active-border`、`--dsw-alias-button-tool-bar-fill`、`--dsw-alias-button-tool-bar-hover`、`--dsw-alias-markdown-inline-code`、`--dsw-alias-state-success-secondary`、`--dsw-alias-tooltip-bg`）、体系外 1（`--dsw-hovercard-bg`）。
