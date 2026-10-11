# 给接手同学的交接说明

交接日期：2026-10-11。

## 目标与分工

这是包含网页界面和服务端 API 的完整项目。请完成云端 AI 接入，使照片识别、菜谱生成在双方电脑关闭后仍可使用。

- 拥有者保管 Cloudflare 账号，负责部署、更新和线上 Secret。
- 同学完成 API 代码、测试，并交回源码及配置说明。
- 不需要共享 GitHub 或 Cloudflare 密码。真实密钥只放在本机或云端 Secret，不进入公开代码和压缩包。

最终 AI 提供商尚未确定。代码已有 SiliconFlow 接入，可以继续完成这套配置，也可更换云端提供商。截图中的 Mac 本地 MLX 服务不是本项目依赖；只在个人电脑运行的 AI 会在关机后停止。

## 当前已经完成什么

界面流程：上传照片 → 辨识 → 修改食材 → 确认常备调味料 → 设置时间、人份、口味和忌口 → 查看三道菜、补购清单及步骤 → 下载文字菜谱。

有不需要密钥的“範例體驗”，使用预设食材和菜谱，受示例食材和偏好限制。它不能当作真实 API 验收。

服务端已有识别及生成代码，但真实 AI 的配置和实测交由同学完成。构建成功、模拟测试通过都不代表真实 AI 可用；实际部署见 [部署记录](DEPLOYMENT-STATUS.md)。

页面数据保存在本次 React 状态，刷新可能丢失。没有启用数据库、图片存储或正式账号系统。D1、R2 均为空，此次不需要创建数据库或存储桶。

## 下载后如何启动

1. 解压，找到包含 `package.json` 的目录。
2. 安装 Node.js 24；用 `node --version` 检查。
3. 使用 pnpm 11.25.0，例如执行 `npm install -g pnpm@11.25.0`。
4. 在项目根目录执行：

```sh
pnpm install --frozen-lockfile
pnpm run dev
```

打开终端打印的地址，通常为 `http://127.0.0.1:5173/`。服务运行期间保留终端，后续命令另开窗口执行。

仓库使用 `pnpm-lock.yaml`，没有 `package-lock.json`。不要使用模板遗留的 `npm run install:ci`，它会调用需要 npm 锁文件的 `npm ci`。
若依赖已装好，但 pnpm 在运行脚本时被本机包管理器环境阻断，可用 `node scripts/run-framework.mjs dev` 或 `node scripts/run-framework.mjs build` 排查。

## 同学重点看哪些文件

| 文件 | 接手内容 |
| --- | --- |
| `lib/ai.ts` | 外部请求地址、认证、模型、提示词、返回值转换、错误和限流 |
| `lib/food.ts` | 食材、偏好和菜谱格式；忌口规则及示例数据 |
| `app/api/recognize/route.ts` | 照片识别入口 |
| `app/api/recipes/route.ts` | 菜谱生成入口 |
| `app/api/health/route.ts` | UI 判断是否配置密钥；换提供商时同步更新 |
| `components/kitchen.tsx` | 用户流程，调用同一网站下的三个 API |

保持“浏览器 → 本站服务端 → 云端 AI”的结构，Secret 只在服务端使用。

当前代码请求 `https://api.siliconflow.cn/v1/chat/completions`，使用 `Authorization: Bearer ...`。这是代码现状，账户权限、模型是否可用和余额需要实际确认。

| 环境变量 | 用途 |
| --- | --- |
| `SILICONFLOW_API_KEY` | 私密密钥，仅本机或云端 Secret |
| `SILICONFLOW_VISION_MODEL` | 识图模型，代码默认 `Qwen/Qwen3-VL-8B-Instruct` |
| `SILICONFLOW_RECIPE_MODEL` | 菜谱模型，代码默认 `Qwen/Qwen3-8B` |

本地把 `.env.example` 复制为 `.env.local`，填入自己的测试密钥并重启。线上还需另行设置 Secret，详见 [Cloudflare 部署](CLOUDFLARE.md)。

换提供商时，修改 `completion()` 的地址、认证、参数和响应解析；确认图片输入格式。`enable_thinking` 是当前模型的特定参数，不要假设别的服务也支持。同步更新健康检查、错误映射、`.env.example` 及本交接文档。

## API 合约

POST 使用 `Content-Type: application/json`。成功返回 JSON；失败返回 `{ "error": "用户能理解的说明" }` 和对应 HTTP 状态码。

### `GET /api/health`

当前响应：

```json
{ "configured": false, "provider": "SiliconFlow" }
```

`configured: true` 只证明有环境变量，不证明密钥有效、模型可用或有余额。

### `POST /api/recognize`

请求：

```json
{ "image": "data:image/jpeg;base64,..." }
```

成功响应：

```json
{
  "ingredients": [
    { "name": "番茄", "quantity": "2 顆（估計）", "confidence": "high" }
  ]
}
```

最多 20 项，`confidence` 为 `high`、`medium`、`low`。不能保证食材新鲜度。
浏览器先缩图并转 JPEG；服务端请求体上限约 6 MB，图片字符串最多 5,600,000 字符，只接受 JPEG/PNG data URL。

### `POST /api/recipes`

请求示例：

```json
{
  "ingredients": [
    { "name": "番茄", "quantity": "2 顆", "confidence": "high" },
    { "name": "雞蛋", "quantity": "3 顆", "confidence": "high" }
  ],
  "preferences": {
    "minutes": 30,
    "servings": 2,
    "taste": "家常",
    "diet": "不限",
    "exclusions": []
  }
}
```

食材为 1–24 项，时间整数 15–60 分钟，人份整数 1–6；口味为 `清淡`、`家常`、`微辣`、`香辣`；饮食类型为 `不限`、`蛋奶素`、`全素`；忌口最多 12 项，每项不超过 20 字。请求体最多 32,000 字节。

成功响应为 `{ "recipes": [三道菜谱对象], "source": "ai" }`。方括号里的“三道菜谱对象”是说明，不是可以原样发送的 JSON。每道菜谱结构：

```json
{
  "title": "番茄炒蛋",
  "description": "酸甜番茄搭配炒蛋。",
  "minutes": 15,
  "ingredients": [
    { "name": "番茄", "quantity": "2 顆" },
    { "name": "雞蛋", "quantity": "3 顆" }
  ],
  "steps": ["洗净切块，打散鸡蛋。", "炒熟鸡蛋盛出，再炒番茄。", "放回鸡蛋炒匀，确保熟透。"],
  "tip": "实际菜谱也要完整列出调味料。"
}
```

必须恰好三道，菜名不同，每道至少三步，完整字段限制以 `recipeSchema` 为准。服务端检查时间和常见忌口词，不合格会拒绝展示，不允许偷偷替换用户偏好。新服务若返回其他格式，先在服务端转换。

## 同学交回前的检查

1. 所选服务在云端运行，支持图片和文字，不依赖个人电脑常开。
2. 用真实图片识别，结果可手动修改。
3. 用真实 API 生成三道菜，检查人数、时间、素食、忌口和补购清单。
4. 检查缺密钥、错误密钥、额度不足、超时、返回格式错误时的页面提示。
5. 交回源码、环境变量名称及用途、提供商入口、实测结果。真实密钥不要放在公开附件。
6. 写清楚拥有者需要“只设置 Secret”，还是“先更新代码，再设置 Secret”。

已有 `scripts/verify-ai.ts` 用模拟上游数据验证接口，不调用真实 AI。可用 TypeScript 测试运行器，例如 `pnpm dlx tsx --test scripts/verify-ai.ts`；首次运行该额外工具需联网。
分享包中两份浏览器 QA 脚本使用可配置的 Playwright 导入，需要时自行安装 Playwright 开发依赖及浏览器；默认使用 Microsoft Edge。它们不是启动网站的必需步骤。

## 代码交回后如何上线

同学交回修改 → 拥有者更新源码 → 安装/构建 → 部署同一个 Cloudflare Worker → 设置 Secret → 用线上网址测试真实 AI。

网站可以先上线再接 API。下载和修改代码不会自动改变线上网站，仍需拥有者部署更新。

当前限流只在单个执行实例内存里：同一 IP 每小时 12 次、实例同时处理一笔 AI 请求。它不是全站持久化配额，使用量增大时需要评估平台限流及持久化配额。

## 分享包范围

真实 `.env.local`、登录凭据、依赖、缓存、构建产物、Git 历史和旧 ZIP 均不包含。`.env.example` 密钥留空。分享副本的 `.openai/hosting.json` 只保留空 D1/R2，不带原 Sites 项目编号。

逐文件用途见 [FILE-GUIDE.md](FILE-GUIDE.md)。`API-SETUP.md` 和 `STARTER-REFERENCE.md` 是保留的历史资料，涉及 Sites 平台的步骤不属于独立 Cloudflare 部署的必需步骤。
