---
name: cognitive-distillation
description: >-
  End-to-end workflow for turning any submitted article, URL, PDF, screenshots,
  or article + AI discussion in the 个人认知沉淀 workspace into the full bilingual
  output suite (index.md, HTML workbench, summary PDF, source PDF set, and en/
  English four-piece suite). Activate whenever the user drops an article or
  raw material into chat, or invokes a cognitive distillation prompt.
---

# 个人认知沉淀 · 全套产物生成 SOP

当用户直接发来文章/材料（或附带提示词）时，按以下 5 步执行，不跳步、不漏件。

## 第 1 步：识别输入内容与类型

通读用户提交的全部文字、链接、附件（PDF / 图片 / 文档）与补充说明，先做 4 项判定：

1. **材料形态**：
   - **纯文章 / 纯原文**（仅有文章、PDF、截图或链接，无历史 AI 对话）：参考 [预设熵增/index.md](../../private/预设熵增/index.md) 的写法，在「我想弄懂」「当前停点」「续聊状态」「完整对话」中如实标明「本次材料未涉及历史对话」，「我的思考轨迹」按原文关键逻辑转折组织（标 `[作者]` / `[AI 解释]`），严禁虚构 `C01`、`C02` 用户对话。
   - **原文 + AI 完整对话**：参考 [Naval的杠杆/index.md](../../样例/Naval的杠杆/index.md)，给原文标 `S01`、`S02`…，给对话按原顺序标 `C01`、`C02`…，严格按四种归因还原用户的卡点、追问、明确偏好与待决策提案。
   - **仅对话 / 思考记录**：提取真实对话轮次并整理判断，原文区标明「本次材料未涉及外部原文」。
   - **附带补充说明**：若用户额外附了一句话说明（如「重点看第 3 点」或最新决定），在归因中标 `[我]` 并注明属于此次补充。
2. **原文语种**：
   - **外文原文**（如英文等）：必须输出三份原文 PDF（`<主题短名>·纯英文原文.pdf`、`<主题短名>·纯中文原文.pdf`、`<主题短名>·中英原文.pdf`）。
   - **纯中文原文**：输出 `<主题短名>·原文精排.pdf`（其中 `en/<Topic> - Original Text.pdf` 忠实直译为英文）。
3. **落盘路径**：
   - 若用户已提前放入某个 `<主题目录>/raw/`，沿用该目录；
   - 若用户直接把内容发在对话框，默认使用 `private/<主题短名>/`（若用户明确要求放到其他目录则从其指定）。
4. **主题命名**：
   - 从内容提炼简洁准确的中文 `<主题短名>`（2～8 字）和英文 `<Topic>`（2～6 词），所有输出文件均以之作为前缀，禁止仅叫 `review` 或 `source`。

## 第 2 步：读取规范并归档 `raw/`

1. **先完整读取四份核心规范**（若内容未读过则必须读取）：
   - [README.md](../../README.md)
   - [index.md 框架与生成规范.md](../../index.md%20框架与生成规范.md)
   - [HTML 回顾页规范.md](../../规范/HTML%20回顾页规范.md)
   - [PDF 排版规范.md](../../规范/PDF%20排版规范.md)
2. **保存原始材料到 `<主题目录>/raw/`**：
   - 若输入是通过对话直接粘贴或抓取链接得到的原文/对话，原样写入 `<主题目录>/raw/`（例如 `raw/source_raw.md` 或 `raw/<Topic>_EN.txt`、`raw/chat_raw.md`）；
   - 若原文为网页链接，先获取完整正文并连同来源 URL 一并存入 `raw/`；
   - 若原图/PDF 已在 `raw/` 中，保持原文件原封不动。

## 第 3 步：生成中文主产物

1. **`<主题目录>/index.md`**（唯一事实来源）：
   - 严格使用固定四个二级标题、判断卡四字段（结论 / 为什么成立 / 边界或反例 / 关键例子）、关系图节点与连线表、续聊状态五项与附录证据。
   - 归因一律只用 `[作者]`、`[我]`、`[AI 解释]`、`[AI 提案 · 待决策]`。
2. **`<主题目录>/<主题短名>·认知精华.html`**：
   - 以 `index.md` 为唯一文本与编号来源，遵守 `规范/HTML 回顾页规范.md`。
   - 纯白底 `#FFFFFF` + 深炭黑 `#141413` + 唯一陶红强调 `#B44E2D`/`#8B3A1E`，无彩色小药丸。
   - 100% 离线单文件（CSS/SVG/JS 全内联，零外部请求），含吸顶搜索与快捷索引、速览/精读切换、桌面横向/手机竖向 SVG 思维导图、30 秒口述卡、可就地展开论证与原文对照的判断卡、续聊区与底部折叠原材料库（`./raw/...`、`./index.md`）。
3. **`<主题目录>/<主题短名>·认知精华.pdf`**：
   - 在系统临时目录（如 `/tmp`）编写打印 HTML，调用本机 Chrome 无头导出：
     ```bash
     "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
       --headless=new --disable-gpu --no-pdf-header-footer \
       --print-to-pdf="<目标PDF路径>" "file://<临时打印HTML路径>"
     ```
   - 遵守 `规范/PDF 排版规范.md` 第 1、2 节。
4. **原文精排 PDF**：
   - 外文材料输出 `<主题短名>·纯英文原文.pdf`、`<主题短名>·纯中文原文.pdf`、`<主题短名>·中英原文.pdf`；
   - 纯中文材料输出 `<主题短名>·原文精排.pdf`。

## 第 4 步：生成 `en/` 纯英文四件套

在 `<主题目录>/en/` 下同步生成 4 个 100% 纯英文文件（所有标题、正文、UI 文案、SVG 思维导图、归因微标 `Author` / `Me` / `AI` / `Pending`、页眉页脚、表格均不得出现任何中文字符）：
1. `en/index.md`（若原对话为中文须完整译为英文；原图/原文件引用使用 `../raw/...`）
2. `en/<Topic> - Key Takeaways.html`（原图与原始文件引用指向 `../raw/...`）
3. `en/<Topic> - Key Takeaways.pdf`
4. `en/<Topic> - Original Text.pdf`

## 第 5 步：渲染验收与清理交付

1. **清理临时文件**：确认主题目录及 `en/` 中只保留规范产物与未改动的 `raw/`，所有打印专用临时 HTML 留在 `/tmp` 或删除。
2. **HTML 实测**：通过无头浏览器或本机 Chrome 检查中文与英文两份 HTML：
   - 外链请求 = 0、控制台报错 = 0；
   - 375px 手机竖屏 `scrollWidth <= innerWidth`；
   - 关键词搜索过滤、速览/精读切换、就地展开原文、原图灯箱均工作正常。
3. **PDF 逐页检查**：将所有生成的 PDF 渲染页图或检查页数与版面，确认无页眉页脚折行、无标题孤立、无表格或 SVG 思维导图跨页腰斩。
4. **交付汇报**：在最终回复中给出主题目录、全部产物路径及实测验证结果。
