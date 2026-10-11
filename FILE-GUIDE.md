# 分享包逐文件说明

本清单解释分享包中的全部 145 个文件，不包含安装后产生的第三方依赖及构建产物。

同学先看 lib/ai.ts、lib/food.ts、三个 app/api 路由和 components/kitchen.tsx；其他框架与 UI 文件保留以保证完整构建。

| 文件 | 用途 |
| --- | --- |
| `.env.example` | 环境变量填写模板；API 密钥留空，可以公开分享。 |
| `.gitignore` | 指定不提交的密钥、依赖、缓存和构建目录。 |
| `.npmrc` | npm 安装偏好，关闭审计、赞助和更新提示。 |
| `.openai/hosting.json` | Sites/Vite 绑定声明；分享副本只保留空 D1/R2，移除原项目编号。 |
| `app/api/health/route.ts` | GET /api/health，返回是否设置密钥；换服务商时同步更新。 |
| `app/api/recipes/route.ts` | POST /api/recipes，读取食材和偏好并生成菜谱。 |
| `app/api/recognize/route.ts` | POST /api/recognize，读取照片请求并调用食材识别。 |
| `app/chatgpt-auth.ts` | 原模板的 ChatGPT 登录辅助函数；当前主页没有使用此登录。 |
| `app/globals.css` | 全站 Tailwind 入口、主题和通用样式。 |
| `app/kitchen.css` | 冰箱料理界面的布局、配色、图片、卡片及响应式样式。 |
| `app/layout.tsx` | HTML 布局、语言、标题、描述、图标及全局样式。 |
| `app/page.tsx` | 网站首页入口，渲染 Kitchen 组件。 |
| `build/connector-preview-plugin.mjs` | 开发时的连接器代理插件，转发到本地预览会话。 |
| `build/connector-preview-worker.mjs` | 本地预览用的连接器 RPC Worker；不是 AI 提供商。 |
| `build/sites-vite-plugin.LICENSE` | 所引用 Sites Vite 插件的许可证，保留第三方归属。 |
| `build/sites-vite-plugin.ts` | 原 Sites 模板的构建辅助与仅本地的模拟登录。 |
| `build/sites-worker.ts` | Cloudflare Worker 请求入口，调用 Vinext 并建立请求级连接器上下文。 |
| `cloudflare-env.d.ts` | Cloudflare Worker 环境变量及可选 D1/R2 的 TypeScript 类型。 |
| `components.json` | shadcn UI 组件生成工具的样式、目录和路径别名配置。 |
| `components/connector-error.tsx` | 原模板的连接器错误展示组件，当前料理主流程不依赖连接器。 |
| `components/kitchen.tsx` | 主要用户界面和 React 状态；上传、食材、偏好、菜谱、步骤及下载。 |
| `components/ui/accordion.tsx` | 通用 UI 库：可展开/折叠的内容分组。 当前料理界面不一定使用此组件。 |
| `components/ui/alert-dialog.tsx` | 通用 UI 库：需要明确确认的对话框。 当前料理界面不一定使用此组件。 |
| `components/ui/alert.tsx` | 通用 UI 库：提示、警告和错误消息区域。 当前料理界面不一定使用此组件。 |
| `components/ui/aspect-ratio.tsx` | 通用 UI 库：保持图片或内容固定宽高比。 当前料理界面不一定使用此组件。 |
| `components/ui/attachment.tsx` | 通用 UI 库：附件、媒体和文件卡片展示。 当前料理界面不一定使用此组件。 |
| `components/ui/avatar.tsx` | 通用 UI 库：头像及缺省占位。 当前料理界面不一定使用此组件。 |
| `components/ui/badge.tsx` | 通用 UI 库：标签和状态徽标。 当前料理界面不一定使用此组件。 |
| `components/ui/breadcrumb.tsx` | 通用 UI 库：当前位置的面包屑导航。 当前料理界面不一定使用此组件。 |
| `components/ui/bubble.tsx` | 通用 UI 库：聊天消息气泡的展示容器。 当前料理界面不一定使用此组件。 |
| `components/ui/button-group.tsx` | 通用 UI 库：组合多个相关按钮。 当前料理界面不一定使用此组件。 |
| `components/ui/button.tsx` | 通用 UI 库：通用按钮及多种样式。 当前料理界面不一定使用此组件。 |
| `components/ui/calendar.tsx` | 通用 UI 库：日期选择日历。 当前料理界面不一定使用此组件。 |
| `components/ui/card.tsx` | 通用 UI 库：通用卡片容器。 当前料理界面不一定使用此组件。 |
| `components/ui/carousel.tsx` | 通用 UI 库：可滑动的轮播内容。 当前料理界面不一定使用此组件。 |
| `components/ui/chart.tsx` | 通用 UI 库：图表容器、主题、图例与提示辅助。 当前料理界面不一定使用此组件。 |
| `components/ui/checkbox.tsx` | 通用 UI 库：勾选框。 当前料理界面不一定使用此组件。 |
| `components/ui/collapsible.tsx` | 通用 UI 库：单个可折叠区域。 当前料理界面不一定使用此组件。 |
| `components/ui/combobox.tsx` | 通用 UI 库：可搜索/组合输入的选择框。 当前料理界面不一定使用此组件。 |
| `components/ui/command.tsx` | 通用 UI 库：命令菜单和快捷搜索列表。 当前料理界面不一定使用此组件。 |
| `components/ui/context-menu.tsx` | 通用 UI 库：右键菜单。 当前料理界面不一定使用此组件。 |
| `components/ui/dialog.tsx` | 通用 UI 库：普通弹窗对话框。 当前料理界面不一定使用此组件。 |
| `components/ui/direction.tsx` | 通用 UI 库：从左向右/从右向左的布局方向设置。 当前料理界面不一定使用此组件。 |
| `components/ui/drawer.tsx` | 通用 UI 库：可拖动的抽屉面板。 当前料理界面不一定使用此组件。 |
| `components/ui/dropdown-menu.tsx` | 通用 UI 库：下拉操作菜单。 当前料理界面不一定使用此组件。 |
| `components/ui/empty.tsx` | 通用 UI 库：没有内容时的占位展示。 当前料理界面不一定使用此组件。 |
| `components/ui/field.tsx` | 通用 UI 库：表单字段、说明和校验状态布局。 当前料理界面不一定使用此组件。 |
| `components/ui/form.tsx` | 通用 UI 库：React Hook Form 的字段关联和错误展示。 当前料理界面不一定使用此组件。 |
| `components/ui/hover-card.tsx` | 通用 UI 库：悬停时显示补充内容的卡片。 当前料理界面不一定使用此组件。 |
| `components/ui/input-group.tsx` | 通用 UI 库：输入框与图标、按钮的组合。 当前料理界面不一定使用此组件。 |
| `components/ui/input-otp.tsx` | 通用 UI 库：一次性验证码分格输入。 当前料理界面不一定使用此组件。 |
| `components/ui/input.tsx` | 通用 UI 库：单行文本输入框。 当前料理界面不一定使用此组件。 |
| `components/ui/item.tsx` | 通用 UI 库：带标题、说明和操作的列表项。 当前料理界面不一定使用此组件。 |
| `components/ui/kbd.tsx` | 通用 UI 库：键盘快捷键样式。 当前料理界面不一定使用此组件。 |
| `components/ui/label.tsx` | 通用 UI 库：表单控件标签。 当前料理界面不一定使用此组件。 |
| `components/ui/marker.tsx` | 通用 UI 库：分组标记、边界和分隔展示。 当前料理界面不一定使用此组件。 |
| `components/ui/menubar.tsx` | 通用 UI 库：横向菜单栏。 当前料理界面不一定使用此组件。 |
| `components/ui/message-scroller.tsx` | 通用 UI 库：消息列表滚动容器。 当前料理界面不一定使用此组件。 |
| `components/ui/message.tsx` | 通用 UI 库：聊天消息、头像和内容布局。 当前料理界面不一定使用此组件。 |
| `components/ui/native-select.tsx` | 通用 UI 库：浏览器原生 select 的样式封装。 当前料理界面不一定使用此组件。 |
| `components/ui/navigation-menu.tsx` | 通用 UI 库：网站导航菜单。 当前料理界面不一定使用此组件。 |
| `components/ui/pagination.tsx` | 通用 UI 库：分页导航。 当前料理界面不一定使用此组件。 |
| `components/ui/popover.tsx` | 通用 UI 库：按钮附近的小型浮动面板。 当前料理界面不一定使用此组件。 |
| `components/ui/progress.tsx` | 通用 UI 库：进度条。 当前料理界面不一定使用此组件。 |
| `components/ui/radio-group.tsx` | 通用 UI 库：单选项组合。 当前料理界面不一定使用此组件。 |
| `components/ui/resizable.tsx` | 通用 UI 库：可调整大小的布局面板。 当前料理界面不一定使用此组件。 |
| `components/ui/scroll-area.tsx` | 通用 UI 库：自定义滚动区域及滚动条。 当前料理界面不一定使用此组件。 |
| `components/ui/select.tsx` | 通用 UI 库：自定义下拉选择框。 当前料理界面不一定使用此组件。 |
| `components/ui/separator.tsx` | 通用 UI 库：分隔线。 当前料理界面不一定使用此组件。 |
| `components/ui/sheet.tsx` | 通用 UI 库：侧边滑入面板。 当前料理界面不一定使用此组件。 |
| `components/ui/sidebar.tsx` | 通用 UI 库：侧边导航栏及状态控制。 当前料理界面不一定使用此组件。 |
| `components/ui/skeleton.tsx` | 通用 UI 库：加载时的骨架占位。 当前料理界面不一定使用此组件。 |
| `components/ui/slider.tsx` | 通用 UI 库：滑动数值选择。 当前料理界面不一定使用此组件。 |
| `components/ui/sonner.tsx` | 通用 UI 库：短暂弹出的 toast 消息。 当前料理界面不一定使用此组件。 |
| `components/ui/spinner.tsx` | 通用 UI 库：加载旋转图标。 当前料理界面不一定使用此组件。 |
| `components/ui/switch.tsx` | 通用 UI 库：开关控件。 当前料理界面不一定使用此组件。 |
| `components/ui/table.tsx` | 通用 UI 库：表格布局。 当前料理界面不一定使用此组件。 |
| `components/ui/tabs.tsx` | 通用 UI 库：标签页切换。 当前料理界面不一定使用此组件。 |
| `components/ui/textarea.tsx` | 通用 UI 库：多行文本输入。 当前料理界面不一定使用此组件。 |
| `components/ui/toggle-group.tsx` | 通用 UI 库：一组可切换状态的按钮。 当前料理界面不一定使用此组件。 |
| `components/ui/toggle.tsx` | 通用 UI 库：单个切换按钮。 当前料理界面不一定使用此组件。 |
| `components/ui/tooltip.tsx` | 通用 UI 库：鼠标悬停/焦点时的简短提示。 当前料理界面不一定使用此组件。 |
| `db/index.ts` | 取得 Cloudflare D1 绑定并创建 Drizzle 数据库连接，当前主流程未使用。 |
| `db/schema.ts` | 数据库表定义入口，目前为空。 |
| `docs/API-SETUP.md` | 历史 SiliconFlow 与 Sites 启用说明；本次以 HANDOFF/CLOUDFLARE 为准。 |
| `docs/CLOUDFLARE.md` | 拥有者部署、后续更新、线上 Secret 配置和验收步骤。 |
| `docs/DEPLOYMENT-STATUS.md` | 本次实际上线网址、验证结果和真实 API 待办。 |
| `docs/FILE-GUIDE.md` | 本文件；分享包中每个项目文件的用途。 |
| `docs/GITHUB-GUIDE.md` | 公开分享 ZIP、上传完整源码、下载及交回修改的图形界面步骤。 |
| `docs/HANDOFF.md` | 同学交接、运行步骤、真实 AI 接入任务和 API 数据合约。 |
| `docs/NETLIFY.md` | 保留的 Netlify 部署路线与说明。 |
| `docs/STARTER-REFERENCE.md` | 本次整理前的框架模板 README 备份，供查阅历史约定。 |
| `drizzle.config.ts` | Drizzle 数据库迁移生成设置；当前业务尚未启用数据库。 |
| `drizzle/meta/_journal.json` | Drizzle 迁移历史索引，目前没有实际业务迁移。 |
| `eslint.config.mjs` | 代码静态检查规则及第三方组件的规则例外。 |
| `examples/d1/app/api/notes/route.ts` | 可选 D1 笔记 API 示例，位于 examples，不是网站启用的路由。 |
| `examples/d1/db/schema.ts` | 可选 D1 笔记数据表示例，不属于当前主业务表。 |
| `handoff-files.json` | 分享包内文件的 SHA-256 与体积清单；不对清单自身计算摘要。 |
| `hooks/use-mobile.ts` | 判断视口是否小于 768px 的 React Hook。 |
| `lib/ai.ts` | 云端 AI 请求、密钥读取、识图和菜谱提示词、输出校验、错误和实例限流。 |
| `lib/connector-context.ts` | 保存请求级连接器上下文，避免跨访客共享能力。 |
| `lib/connector-contract.mts` | 原模板连接器客户端、参数和返回值类型；.mjs 导入由构建器解析。 |
| `lib/connector-errors.mts` | 将连接器错误状态转换为可展示的错误信息。 |
| `lib/connector-preview.d.ts` | 开发预览连接器的虚拟模块与环境 TypeScript 声明。 |
| `lib/connectors.ts` | 取得当前请求的原模板连接器客户端；当前料理业务未调用。 |
| `lib/food.ts` | 食材/偏好/菜谱 schema、忌口词、别名、缺少食材判断和预设菜谱。 |
| `lib/utils.ts` | 合并 CSS class 名称的通用工具。 |
| `netlify.toml` | 保留的 Netlify 构建命令、输出目录和 Next.js 插件配置。 |
| `next.config.ts` | Next.js 配置，供保留的 Next.js/Netlify 路线使用。 |
| `package.json` | 依赖版本、Node/pnpm 要求和启动、构建等脚本。 |
| `pnpm-lock.yaml` | 锁定具体依赖及校验信息，保持安装版本一致。 |
| `pnpm-workspace.yaml` | pnpm 原生依赖构建许可，允许 esbuild、sharp、workerd 等安装步骤。 |
| `portable/assets.d.ts` | 将 PNG 图片作为模块导入的 TypeScript 声明。 |
| `portable/main.tsx` | 离线展示版 React 入口，传入 offline 模式及内嵌图片。 |
| `postcss.config.mjs` | 配置 Tailwind CSS 的 PostCSS 处理。 |
| `public/favicon.svg` | 浏览器标签页图标。 |
| `public/file.svg` | 原模板保留的文件图标。 |
| `public/globe.svg` | 原模板保留的地球图标。 |
| `public/ingredients.png` | 生成的食材示意图片，用于範例及卡片；不是识图结果。 |
| `public/window.svg` | 原模板保留的窗口图标。 |
| `README.md` | 项目入口说明及交接文档导航，后半保留原框架说明。 |
| `scripts/build-netlify.mjs` | 执行 next build --webpack，产生 Netlify 所需的 Next.js 输出。 |
| `scripts/build-portable.mjs` | 打包单文件离线展示 HTML，需先通过 Netlify 构建得到 CSS，不含真实 API。 |
| `scripts/build-verified.sh` | 原 managed-linux 配置的限时构建脚本，普通 Windows 交接无需使用。 |
| `scripts/check-share-secrets.mjs` | 扫描分享副本或构建目录是否含本地密钥和常见私钥，不打印密钥值。 |
| `scripts/connector-preview/connector-preview-session.mjs` | 原模板由开发工具启动的连接器预览会话，不由线上网站运行。 |
| `scripts/connector-preview/host-binding.mjs` | 原预览连接器的权限、大小、超时和结果检查。 |
| `scripts/connector-preview/protocol.mjs` | 原连接器预览协议的 schema 与会话参数校验。 |
| `scripts/execution-profile.mjs` | 读取本地运行模式；干净下载没有本地设置时默认 portable。 |
| `scripts/install-ci.mjs` | 原 npm CI 安装入口；需要 package-lock.json，本次 pnpm 交接不使用。 |
| `scripts/install-ci.sh` | 原 managed-linux 的 npm CI 安装辅助，不是同学的普通安装步骤。 |
| `scripts/install-pnpm.sh` | 原 managed-linux 的 pnpm 安装辅助，普通下载使用 pnpm install。 |
| `scripts/npm-install.mjs` | 原模板 npm 安装进程、缓存和运行环境辅助。 |
| `scripts/package-handoff.mjs` | 创建干净分享副本、生成逐文件说明和 SHA-256 清单；不部署或上传 GitHub。 |
| `scripts/pnpm-install.mjs` | 原模板 pnpm 安装进程与执行环境辅助。 |
| `scripts/qa-desktop.mjs` | 桌面流程、菜谱、下载、缺密钥和模拟 API 的浏览器检查；需额外 Playwright。 |
| `scripts/qa-portable.mjs` | 离线展示版浏览器检查；需先生成离线 HTML，并安装 Playwright。 |
| `scripts/run-framework.mjs` | 选择运行模式，调用 Vinext 或 Vite 的 dev/build。 |
| `scripts/sites-env.mjs` | 保持系统环境，默认把 Wrangler/Miniflare 工具状态放在项目内。 |
| `scripts/sites-env.sh` | 原 managed-linux 环境设置辅助，普通 Windows 路线不需要 Bash。 |
| `scripts/verify-ai.ts` | 已有模拟 AI 合约、食品限制、请求体和错误测试，不消耗真实 API 额度。 |
| `tsconfig.json` | TypeScript 编译检查、React JSX 和 @/ 路径别名。 |
| `vendor/shadcn-tailwind-4.13.0.css` | 保留的 shadcn/Tailwind 动画及样式资源。 |
| `vendor/shadcn-tailwind-4.13.0.LICENSE.md` | 第三方样式的许可证，保留作者归属。 |
| `vite.config.ts` | Vinext/Vite 与 Cloudflare 插件；生成部署配置、连接本地绑定和预览。 |

## 不分享的内容

.env.local 及其他真实环境文件、.git、node_modules、.next、dist、.wrangler、.sites-runtime、.netlify、缓存、artifacts 和 tsconfig.tsbuildinfo 不在包内。它们分别是密钥/本机状态、依赖或生成结果。安装和构建会重新生成需要的文件。

## 分享副本的整理

.openai/hosting.json 移除原 Sites project_id，只保留空的 D1/R2。两份 QA 脚本的原机器专用 Playwright 路径改成可配置导入：默认导入 playwright，也可设置 PLAYWRIGHT_MODULE 为你自己的模块路径。运行这些辅助脚本前自行安装 Playwright 和浏览器。业务代码保持当前工作区版本。

handoff-files.json 为其他文件记录 SHA-256 和体积，不包含自身摘要，帮助检查解压文件是否完整。
