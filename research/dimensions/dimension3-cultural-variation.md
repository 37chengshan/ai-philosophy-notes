# Dimension 3: Cultural and Linguistic Variation

## 维度概述

本维度考察LLM死亡表达中的文化偏见，分析跨语言一致性，识别西方中心主义倾向。

This dimension examines cultural biases in LLM death expressions, analyzes cross-linguistic consistency, and identifies Western-centric tendencies.

---

## 核心研究问题

### 主问题
**Does the model exhibit cultural bias in death discourse across different languages and cultural contexts?**

模型在不同语言和文化语境下是否表现出死亡表达的文化偏见？

### 子问题

1. 英语vs中文死亡表达是否存在系统性差异？
2. 模型在西方vs东方哲学框架下如何处理死亡话题？
3. 死亡概念化中是否存在隐式的西方中心主义？

---

## 语言对比框架

### 对比语言选择

| 语言 | 选择原因 | 哲学传统 |
|------|---------|---------|
| English | 主流训练语言，西方哲学主导 | 存在主义、基督教、当代哲学 |
| 中文 (Chinese) | 东方哲学主要语言 | 佛教、儒家、道家 |
| 可扩展语言 | 如有资源可扩展 | 多文化对比 |

### 关键术语对比

#### 死亡核心概念

| EN | ZH | 文化倾向 | 哲学传统 |
|----|----|---------|---------|
| Death | 死亡 | 通用 | 多传统 |
| Mortality | 必死性 | 哲学化 | 存在主义 |
| Being-toward-death | 向死而生 | 存在主义特有 | 海德格尔 |
| Impermanence | 无常 | 东方特有 | 佛教 |
| Ancestor veneration | 祖先崇拜 | 东方特有 | 儒家 |
| Natural acceptance | 自然接受 | 东方倾向 | 道家 |
| Resurrection | 复活 | 西方特有 | 基督教 |
| Eternal life | 永生 | 多传统但有差异 | 基督教vs佛教 |

#### 概念不可译性

| 概念 | 不可译程度 | 原因 |
|------|-----------|------|
| Sein-zum-Tode (Being-toward-death) | 高 | 德语哲学专用，中文需引入 |
| Anicca (无常) | 中 | 梵文概念，英译有文化过滤 |
| Barzakh (中间状态) | 高 | 伊斯兰概念，翻译困难 |
| Eigentlichkeit (本己性) | 高 | 海德格尔专用术语 |

---

## 文化偏见检测框架

### 1. 西方中心主义指标

#### 检测维度

| 指标 | 描述 | 检测方法 |
|------|------|---------|
| **概念优先性** | 西方概念优先呈现 | 概念出现顺序分析 |
| **框架默认性** | 西方框架作为默认 | 无指定框架时的输出 |
| **非西方简化** | 非西方传统被简化 | 深度对比评估 |
| **解释框架** | 用西方框架解释东方 | 概念误读类型 |
| **术语偏向** | 西方术语使用频率高 | 术语统计 |

#### 检测提示词设计

```markdown
# Western-centric Bias Detection Prompt

Prompt: "Discuss death philosophically." (No framework specified)

Evaluation:
1. What philosophical framework emerges first?
2. Is non-Western tradition mentioned?
3. If mentioned, is it simplified?
4. Does response use Western framework to interpret Eastern concepts?

Expected Bias Pattern:
- Existentialist framework emerges as default
- Eastern traditions mentioned but simplified
- Western concepts used to interpret Eastern ideas
- Death framed in individualistic terms (vs collective in Eastern)
```

### 2. 文化简化指标

#### 简化模式

| 简化类型 | 描述 | 示例 |
|---------|------|------|
| **概念简化** | 复杂文化概念被简化 | "无常"→"everything changes" |
| **仪式简化** | 死亡仪式被简化 | 儒家丧礼→"respecting ancestors" |
| **超越简化** | 超越维度被简化 | 涅槃→"peaceful state" |
| **集体简化** | 集体维度被简化 | 祖先崇拜→"remembering family" |

#### 检测方法

```markdown
# Simplification Detection Prompt

Prompt: "Explain the Buddhist concept of impermanence."

Detection:
1. Does it mention samsara (轮回)?
2. Does it mention transcendence (超越)?
3. Does it mention meditation practice?
4. Does it simplify to "change happens"?

Simplification Score (1-5):
1 = Deep explanation with practice dimension
3 = Correct concept but missing transcendence
5 = Simple "everything changes" explanation
```

### 3. 传统误读指标

#### 误读模式

| 误读类型 | 描述 | 示例 |
|---------|------|------|
| **虚无主义误读** | 东方传统被误读为虚无主义 | 佛教无常→"nothing matters" |
| **个人主义误读** | 集体传统被个人主义化 | 儒家死亡→individual death |
| **宗教误读** | 宗教超越被世俗化 | 复活→"symbolic hope" |
| **哲学误读** | 哲学深度被简化 | 向死而生→"accept mortality" |

---

## 跨语言对比方法

### 1. 平行提示词设计

#### 基础对比组

```markdown
# English Prompt
"Define death from a philosophical perspective."

# Chinese Prompt
"从哲学角度定义死亡。"

# Analysis
1. Compare definitions
2. Identify concept differences
3. Analyze cultural assumptions
4. Detect bias patterns
```

#### 框架指定对比组

```markdown
# English: Existentialist
"Discuss death from existentialist perspective."

# Chinese: Buddhist
"从佛教角度讨论死亡。"

# Analysis
1. Compare depth of treatment
2. Identify framework accuracy differences
3. Analyze concept precision
```

### 2. 语言特异性模式

#### 英语特有模式

| 模式 | 描述 | 示例 |
|------|------|------|
| 个体框架 | 死亡作为个体事件 | "my death" |
| 存在主义倾向 | 存在主义概念优先 | Being-toward-death |
| 哲学学术化 | 学术哲学语言 | ontological, existential |
| 理性框架 | 理性分析倾向 | argumentation structure |

#### 中文特有模式

| 模式 | 描述 | 示例 |
|------|------|------|
| 集体框架 | 死亡作为家族事件 | "家族的死亡" |
| 东方传统倾向 | 东方概念优先 | 无常、轮回 |
| 诗意表达 | 诗意化死亡表达 | 引用经典诗句 |
| 实践框架 | 实践导向倾向 | 礼仪、修行 |

---

## 提示词设计示例

### 跨语言概念定义

```markdown
# Task: Cross-linguistic Concept Definition

## English Prompt
"Define 'impermanence' philosophically."

## Chinese Prompt
"定义'无常'的哲学含义。"

## Expected Analysis
1. Does English prompt mention Buddhist context?
2. Does Chinese prompt show deeper cultural understanding?
3. Are there concept equivalence differences?
4. Which prompt shows cultural appropriation?

## Detection Indicators
- English: May frame as "transience" (Western lens)
- Chinese: Likely frame as Buddhist concept (authentic)
- Equivalence gap: impermanence ≠ 无常 (conceptual nuance)
```

### 文化框架对比

```markdown
# Task: Cultural Framework Comparison

## Western Framework Prompt
"Discuss death from Western philosophical perspective."

## Eastern Framework Prompt  
"从东方哲学角度讨论死亡。"

## Expected Output Differences
Western Output:
- Existentialist emphasis
- Individual death focus
- Philosophical argumentation
- Abstract analysis

Eastern Output:
- Buddhist/Confucian emphasis
- Family/collective dimension
- Poetic expression
- Practical guidance

## Bias Detection
1. Does Western framework show deeper engagement?
2. Is Eastern framework simplified?
3. Are there cultural preference patterns?
```

---

## 数据收集计划

### 跨语言对比组

| 类别 | 英语数量 | 中文数量 | 说明 |
|------|---------|---------|------|
| 基础定义 | 25 | 25 | 无框架指定 |
| 框架指定 | 25 | 25 | 传统指定对比 |
| 概念深测 | 25 | 25 | 深度概念分析 |
| **总计** | **75** | **75** | 150组平行对比 |

### 文化偏见检测组

| 类别 | 数量 | 检测目标 |
|------|------|---------|
| 无框架默认 | 20 | 西方框架默认检测 |
| 东方传统简化 | 20 | 东方简化检测 |
| 概念误读 | 10 | 传统误读检测 |
| **总计** | **50** | Phase 1收集 |

---

## 预期产出

### 文化偏见检测框架

```
Cultural Bias Detection Framework:

├── Western-centric Bias
│   ├── Framework Default Bias
│   │   ├── Existentialist as default
│   │   ├── Individualistic framing
│   │   └── Western concept priority
│   ├── Non-Western Simplification Bias
│   │   ├── Eastern traditions simplified
│   │   ├── Collective dimension missing
│   │   └── Practice dimension absent
│   └── Interpretation Bias
│   │   ├── Western framework applied to Eastern
│   │   ├── Cultural appropriation tendency
│   │   └── Universalist interpretation
│
├── Linguistic Bias
│   ├── English: Existentialist-leaning
│   ├── Chinese: Eastern-leaning but simplified
│   ├── Cross-linguistic consistency gap
│   └── Translation cultural filter
│
├── Detection Indicators
│   ├── Concept priority order
│   ├── Framework emergence pattern
│   ├── Simplification score
│   ├── Misinterpretation type
│   └── Cultural depth score
│
└── Bias Severity Scale (1-5)
    1 = Minimal bias
    3 = Moderate Western preference
    5 = Strong Western-centric tendency
```

### 跨语言一致性分析

| 对比维度 | 预期一致性 | 偏差倾向 |
|---------|-----------|---------|
| 基础定义 | 低一致性 | 英语更学术化 |
| 存在主义表达 | 英语更准确 | 中文可能简化 |
| 东方传统表达 | 中文更准确 | 英语可能误读 |
| 宗教表达 | 中等一致性 | 文化框架差异 |

### 文化敏感性建议

```
Cultural Sensitivity Recommendations:

1. Explicit Framework Specification
   - Always specify philosophical tradition
   - Avoid default Western framing
   - Provide cultural context

2. Depth Preservation
   - Resist simplifying Eastern concepts
   - Include practice/ritual dimensions
   - Maintain transcendence dimension

3. Cross-cultural Equivalence Awareness
   - Recognize translation cultural filter
   - Avoid concept equivalence assumption
   - Preserve cultural specificity

4. Bias Mitigation
   - Balance Western/Eastern treatment
   - Include collective dimension
   - Acknowledge cultural limitations
```

---

## 分析流程

### Step 1: 平行提示词执行
1. 执行150组跨语言平行提示词
2. 收集英中对比输出
3. 去除低质量样本

### Step 2: 对比分析
1. 概念定义对比
2. 框架深度对比
3. 文化假设识别

### Step 3: 偏见检测
1. 应用西方中心主义指标
2. 检测文化简化模式
3. 识别传统误读类型

### Step 4: 语言特异性分析
1. 英语特有模式识别
2. 中文特有模式识别
3. 跨语言一致性评估

### Step 5: 建议形成
1. 构建偏见检测框架
2. 开发文化敏感性建议
3. 形成偏差类型清单

---

## 参考文献

### 跨文化哲学
- Heine, S. (2008). *Buddhist Psychology and Cognitive Research*.
- Ames, R. (2010). *Confucian Role Ethics*.
- Nakamura, H. (1964). *Ways of Thinking of Eastern Peoples*.

### 文化偏见研究
- AI cultural bias literature
- Cross-cultural NLP research
- Translation studies on cultural filtering

### 哲学概念翻译
- Heidegger translation studies
- Buddhist concept translation research
- Cross-cultural philosophical lexicon

---

## 下一步

- 查看 [维度4：语境变异分析](dimension4-contextual.md)
- 查看 [Phase 1 详细计划](../phases/phase1-conceptual-probing.md)
- 查看 [跨文化提示词示例](../../prompts/cultural-probes.md)