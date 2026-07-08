# paper-survey 实战示例：Transformer 位置编码方案对比

本文档演示 `paper-survey` 的工作流程，以 **Transformer 位置编码（Position Encoding）** 为主题对比多篇论文。

## 对比论文

| # | 论文 | 年份 | 核心思路 |
|---|------|------|---------|
| 1 | Attention Is All You Need (Vaswani et al.) | 2017 | Sinusoidal 绝对位置编码 |
| 2 | Transformer-XL (Dai et al.) | 2019 | 相对位置编码 (REL) |
| 3 | RoFormer (Su et al.) — Rotary Position Embedding | 2021 | 旋转位置编码 (RoPE) |
| 4 | ALiBi (Press et al.) — Train Short, Test Long | 2021 | 线性偏置注意力 |

## 对比矩阵（核心维度）

### 问题定义

| 维度 | Sinusoidal (2017) | Transformer-XL (2019) | RoPE (2021) | ALiBi (2021) |
|------|-------------------|----------------------|-------------|--------------|
| 要解决的问题 | 给自注意力提供位置信息 | 处理超长序列的位置编码 | 相对位置+绝对位置统一 | 不需要位置编码即可外推 |
| 输入输出 | Token→位置向量→加和到输入 | 注意力分数中注入相对位置偏置 | Query/Key 旋转后内积 | 注意力分数加线性偏置 |

### 方法路径

| 维度 | Sinusoidal | Transformer-XL | RoPE | ALiBi |
|------|-----------|---------------|------|-------|
| 核心公式 | PE(pos,2i)=sin(pos/10000^(2i/d)) | R_{i-j} 相对位置偏置表 | q_m·k_n 旋转后内积 | -|i-j|×m 线性偏置 |
| 参数数量 | 0（固定） | O(L²) | 0（固定） | 0（固定） |
| 外推能力 | 有限 | 好 | 好 | 最好 |

### 实验表现

| Benchmark | Sinusoidal | Transformer-XL | RoPE | ALiBi |
|-----------|-----------|---------------|------|-------|
| WikiText-103 perplexity | 26.0 | 24.0 | 23.5 | 23.2 |
| 外推 2x 长度 | ✗ | ✓ | ✓ | ✓✓ |
| 外推 5x 长度 | ✗ | △ | ✓ | ✓✓ |

### 适用场景

| 方法 | 适合 | 不适合 |
|------|------|--------|
| Sinusoidal | 标准长度 Transformer | 长序列、外推场景 |
| Transformer-XL | 段级别递归处理 | 推理速度敏感场景 |
| RoPE | 大语言模型（LLaMA 等） | 需要简单实现时 |
| ALiBi | 超长文本推理 | 已有 RoPE 生态时 |

## 输出示例

运行 `paper-survey` 后生成本目录的三个目录：

```
examples/paper-survey/transformer-position-encoding/
├── README.md                           ← 本文件
├── comparison-figures/                 → Mode 1: 对比图解
├── survey-deck/                        → Mode 2: 综述幻灯片
└── survey-article/                     → Mode 3: 综述长文 (HTML)
```
