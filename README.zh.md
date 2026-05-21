# paper-craft-skills

[English](./README.md) | 中文

**把学术论文一键变成深度文章、论文框架图和机制图解。**

<p align="center">
  <img src="examples/paper-illustrated/attention-is-all-you-need/transformer-overview-paper-figure.png" width="900" alt="paper-craft-skills 生成的 Transformer 方法总览图"/>
</p>

<p align="center">
  <b>从论文 PDF 到可以直接放 README、文章和视频里的方法图。</b><br/>
  先读论文，推荐该画哪些图，确认语言 / 风格 / 张数，再调用 Codex 生图能力或当前环境可用的生图后端。
</p>

<table>
<tr>
<td width="50%" align="center">
<img src="examples/paper-illustrated/attention-is-all-you-need/self-attention-sketchnote.png" width="320"/><br/>
<b>paper-comic</b><br/>
论文 → 方法图解<br/>
温暖笔记风 / 论文框架图风
</td>
<td width="50%" align="center">
<img src="images/hero_banner.png" width="420"/><br/>
<b>paper-analyzer</b><br/>
论文 → 深度技术文章<br/>
支持公式、源码、图片和多种写作风格
</td>
</tr>
</table>

## 为什么不一样

| Skill | 输出 | 适合做什么 |
|------|------|------------|
| **paper-comic** | 方法总览图、机制拆解图、论文视觉笔记 | README 首屏、视频宣传、技术文章配图、论文讲解 |
| **paper-analyzer** | 深度 Markdown/HTML 长文，多种写作风格 | 论文解读、公众号文章、学习笔记、技术博客 |

`paper-comic` 现在不是固定 10 页漫画，而是论文方法图解：它会先读论文，判断哪些内容值得画，再问你要中文还是英文、要温暖笔记风还是论文框架图风、只要一张概述图还是生成多张机制图。

## 快速开始

### 1. 安装

```bash
npx skills add zsyggg/paper-craft-skills
```

### 2. 配置

| 技能 | 需要配置 |
|------|----------|
| paper-analyzer | `MINERU_TOKEN`，从 [mineru.net](https://mineru.net) 获取 |
| paper-comic | 当前环境可用的生图后端。在 Codex 中会使用内置 `imagegen` skill。 |

```bash
# paper-analyzer 需要
pip install requests markdown
export MINERU_TOKEN="your_token"
```

### 3. 使用

```bash
# 生成论文方法图解
/paper-comic /path/to/paper.pdf
/paper-comic https://arxiv.org/abs/1706.03762 --style paper-figure --language English --pages 1

# 分析论文，生成深度文章
请帮我分析这篇论文：/path/to/paper.pdf
```

## paper-comic：论文方法图解

生成图片前，skill 会先推荐方案：

```text
我建议生成 4 张图：
1. 方法总览图
2. 核心机制 A
3. 核心机制 B
4. 关键结果图

请确认：
- 语言：中文 / English / 双语
- 风格：sketchnote / paper-figure
- 范围：只要第 1 张，还是生成全部 4 张？
```

### 两种视觉风格

| 风格 | 视觉效果 | 适合场景 |
|------|----------|----------|
| **sketchnote** | 温暖科研笔记风，手绘箭头、圈注和理解锚点 | 想让人快速看懂论文在做什么 |
| **paper-figure** | 干净专业的论文框架图，模块、箭头、矩阵和结果更工整 | 想做 README 首屏、技术文章头图、演示文稿 |

### 示例：Attention Is All You Need

<table>
<tr>
<td align="center" width="58%">
<img src="examples/paper-illustrated/attention-is-all-you-need/transformer-overview-paper-figure.png" width="520"/><br/>
<b>paper-figure</b>：Transformer 方法总览
</td>
<td align="center" width="42%">
<img src="examples/paper-illustrated/attention-is-all-you-need/self-attention-sketchnote.png" width="260"/><br/>
<b>sketchnote</b>：自注意力机制图解
</td>
</tr>
</table>

完整示例见：[examples/paper-illustrated/attention-is-all-you-need](./examples/paper-illustrated/attention-is-all-you-need)

## paper-analyzer：深度论文文章

将学术论文转化为深度技术文章，支持 3 种写作风格。

### 写作风格

<table>
<tr>
<td align="center" width="33%">
<b>academic</b><br/>学术型（默认）<br/><br/>
正式严谨，适合学术分享
</td>
<td align="center" width="33%">
<b>storytelling</b><br/>故事型<br/><br/>
生动比喻，适合公众号
</td>
<td align="center" width="33%">
<b>concise</b><br/>精炼型<br/><br/>
表格列表，快速阅读
</td>
</tr>
</table>

![风格对比](images/styles_comparison.png)

### 可选功能

| 功能 | 说明 | 效果 |
|------|------|------|
| **公式讲解** | 插入公式图片，详解符号含义 | <img src="images/formula_feature.png" width="260"/> |
| **代码分析** | 论文概念与 GitHub 源码对照 | <img src="images/code_feature.png" width="260"/> |

## 兼容性

支持以下 AI 编程助手：

- Codex
- Claude Code
- Cursor
- Windsurf
- 其他支持 Claude Code skill 的工具

## 致谢

- **MinerU** - PDF 高精度解析，来自 [mineru.net](https://mineru.net)
- 图片生成使用当前环境可用的生图后端；在 Codex 中会使用内置 `imagegen`。

## License

MIT
