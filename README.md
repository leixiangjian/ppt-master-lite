# PPT Master Lite — 浏览器端 AI 驱动的 PPT 生成器
![](20261013162913.png)

[English](./README.en.md) | 中文

丢进一份 PDF、Word、网页链接或一段文字，AI 自动生成**可在 PowerPoint 中直接编辑**的精美演示文稿。全程在浏览器中运行，无需安装，无需服务器，数据不出本地。

> **打开即用**：将单个 HTML 文件保存到本地，双击即可开始制作 PPT。
访问地址:https://leixiangjian.github.io/ppt-master-lite/

---

## 它解决什么问题

常见 AI PPT 工具的产物有两类：导出成图片的（打开只能看，不能改），以及套模板填空的（版式锁死）。

PPT Master Lite 走的是第三条路线——输出**原生可编辑的 PowerPoint**：图形带调节手柄、文字是真文本框、图表是带数据的原生对象，在 PowerPoint / Keynote / WPS 里都能继续编辑。

> 可编辑早已是及格线——真正拉开差距的是原生深度。PPT Master Lite 交给你的是一份真正的 PowerPoint：母版、原生形状、数据驱动的图表，而不是一堆扁平文本框。

它还不止把幻灯片排得好看——**先替你把逻辑理顺，再谈视觉**。

---

## 核心特性

### 🎯 AI 智能生成

- **多格式素材输入**：支持 PDF、DOCX、TXT、Markdown、网页链接，或直接粘贴文本
- **多文件汇总分析**：一次上传多个文件，AI 自动汇总分析，提炼核心内容
- **两步生成流程**：
  - 第一步：AI 分析素材，输出结构化大纲（可在线编辑每页标题和要点）
  - 第二步：用户确认后，AI 为每页生成详细内容（要点、图表数据、表格数据、讲者备注）
- **自动配图**：可选为每页生成配图，由 Pollinations 免费提供

### 🎨 主题与模板系统

- **8 个内置主题**：商务深蓝、极简白、暗黑科技、暖阳橙、森林绿、玫瑰红、海洋蓝、企业灰
- **PPTX 模板导入**：上传任意 `.pptx` 文件，自动解析主题配色、字体，生成自定义主题和母版
- **三种母版版式**：封面（COVER）、内容（CONTENT）、章节（SECTION），每种版式有不同的装饰元素

### ✏️ 在线可视化编辑

- **所见即所得**：拖拽移动元素、拖动圆点缩放、双击文本直接编辑
- **属性面板**：修改字体、字号、颜色、对齐方式、位置尺寸
- **元素类型**：文本、形状、表格、图表、图片、Emoji 图标
- **图表支持**：柱状图、折线图、饼图，数据实时编辑，预览与导出同步

### 📤 原生 PPTX 导出

- 使用 PptxGenJS 在浏览器端生成 `.pptx` 文件
- **母版装饰**：导出时通过 `defineSlideMaster()` 创建原生母版，包含背景装饰、品牌栏
- **讲者备注**：`addNotes()` 写入原生备注
- **切换动画**：支持淡入淡出、推入、擦除等效果
- 导出的 PPTX 在 PowerPoint 中打开，所有元素均可编辑

### 💾 工程保存

- 保存为 HTML 文件，数据以 JSON 形式内嵌
- 下次打开可继续编辑
- 自动保存到 localStorage，刷新不丢失

---

## 快速开始

### 打开方式

1. 将本项目保存为一个 HTML 文件（如 `ppt-master-lite.html`）
2. 用 Chrome / Edge / Firefox 双击打开
3. 即可开始使用

> 无需安装任何软件、无需注册账号、无需服务器。

### 配置 API

1. 点击右上角「⚙ 设置」
2. 填入 OpenAI 兼容的 API 地址、Key 和模型名称
3. 支持预设：OpenAI / DeepSeek / Kimi / 智谱 / Ollama
4. 配置保存在浏览器 localStorage，只需填写一次

### 生成第一份 PPT

1. 点击「✨ AI 生成 PPT」
2. 选择素材来源（粘贴文字 / 上传文件 / 网页链接）
3. 设置目标页数、内容风格和主题风格
4. 点击「开始分析」
5. AI 分析后展示大纲，可在线编辑每页标题和要点
6. 点击「确认并生成」
7. 逐页生成内容（有进度条和实时日志）
8. 完成后点击「进入编辑」即可修改

### 手动编辑

- 底部工具栏添加元素：文本 / 形状 / 表格 / 图表 / 图片 / 图标
- 拖拽移动、圆点缩放、双击编辑文本
- 右侧属性面板修改所有属性
- 顶部「🎨 主题」切换配色方案
- 「📦 导入模板」上传 PPTX 模板

### 导出

- 点击「⬇ 导出 PPTX」生成原生 PowerPoint 文件
- 点击「💾 保存」保存为 HTML 工程文件

---

## 技术架构

### 前端技术栈

| 技术 | 用途 |
|---|---|
| PptxGenJS | 浏览器端生成原生 PPTX |
| Chart.js | 图表预览渲染 |
| PDF.js | PDF 文件解析 |
| mammoth.js | DOCX 文件解析 |
| JSZip | PPTX 模板解包 |

### 核心设计

- **单 HTML 文件**：所有 CSS、JavaScript 内嵌，通过 CDN 引入外部库
- **数据模型**：幻灯片以 JSON 结构存储，导出时直接映射为 PptxGenJS 对象
- **坐标系统**：1 英寸 = 96 CSS 像素，与 PptxGenJS 坐标完全一致，所见即所得
- **母版系统**：通过 `defineSlideMaster()` 定义 COVER / CONTENT / SECTION 三种母版

### 工作流程
用户导入素材 → AI 分析生成大纲 → 用户确认 → AI 逐页生成内容 → 在线编辑 → 导出 PPTX


---

## 主题系统

### 内置主题

| 主题 | 主色 | 强调色 | 风格 |
|---|---|---|---|
| 商务深蓝 | #1A1A2E | #E94560 | 专业、沉稳 |
| 极简白 | #333333 | #007AFF | 简洁、现代 |
| 暗黑科技 | #1A1A2E | #00D4AA | 科技、酷炫 |
| 暖阳橙 | #3D2C1E | #FF7A45 | 温暖、活力 |
| 森林绿 | #1B3A2F | #2E9E6B | 自然、清新 |
| 玫瑰红 | #4A1F2E | #D6336C | 优雅、浪漫 |
| 海洋蓝 | #0B3954 | #087E8B | 深邃、冷静 |
| 企业灰 | #2C3E50 | #3498DB | 稳重、商务 |

### 自定义模板

上传任意 `.pptx` 文件，系统自动解析：
- 主题配色（6 种主题色）
- 标题字体和正文字体
- 母版背景色

生成的自定义主题自动包含对应的母版装饰。

---

## 示例

| 输入 | 输出 |
|---|---|
| 一份 20 页的行业报告 PDF | 10 页商务汇报 PPT，含数据图表和表格 |
| 一篇产品发布文章 + 主题「2025 新品发布」 | 8 页产品发布 PPT，含封面、核心卖点、参数对比 |
| 多个文件（PDF + DOCX + TXT） | 汇总所有文件内容，生成综合汇报 PPT |

---

## 能力边界

- 单 HTML 文件，无需安装，数据不出本地
- 浏览器端生成原生 PPTX，可在 PowerPoint / Keynote / WPS 中编辑
- 支持 AI 智能生成 + 人工在线编辑的双模式
- 母版系统提供风格化背景装饰

### 局限性

- 复杂 SVG 排版（如布尔运算、任意曲线）支持有限
- PPTX 模板导入仅解析主题配色和字体，不解析布局占位符
- 需要用户自备 LLM API Key（兼容 OpenAI 格式）

---

## 开发者

本项目基于 [PptxGenJS](https://github.com/gitbrent/PptxGenJS) 构建，参考了 [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) 的设计理念。

### 构建

无需构建工具，直接编辑 HTML 文件即可。

### 目录结构
ppt-master-lite/
├── ppt-master-lite.html # 单文件应用
├── README.md # 中文说明
├── README.en.md # 英文说明
└── LICENSE # 许可证


---

## 许可证

MIT License

---

## 致谢

- [PptxGenJS](https://github.com/gitbrent/PptxGenJS) — 浏览器端 PowerPoint 生成
- [Chart.js](https://www.chartjs.org/) — 图表渲染
- [PDF.js](https://mozilla.github.io/pdf.js/) — PDF 解析
- [mammoth.js](https://github.com/mwilliamson/mammoth.js) — DOCX 解析
- [JSZip](https://stuk.github.io/jszip/) — ZIP 解包
- [Pollinations](https://pollinations.ai/) — 免费图像生成