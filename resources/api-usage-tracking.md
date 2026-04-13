# API Usage Tracking Template

## API使用追踪模板

本文档提供OpenAI API使用的追踪方法和模板，用于研究过程中的API调用管理。

---

## 追踪目的

### 研究管理
- 监控API调用数量（500-800计划，10,000-16,000实际范围）
- 控制预算使用（$800 total）
- 确保数据收集完整性

### 学术规范
- 记录研究过程可复现性
- 提供数据来源透明性
- 支持方法论文档化

---

## 追踪维度

### 1. 提示词追踪

| 维度 | 描述 | 记录字段 |
|------|------|---------|
| **提示词ID** | 提示词唯一标识 | prompt_id |
| **提示词类别** | 所属维度/类别 | category (D1-D5) |
| **提示词层级** | Tier层级 | tier (T1-T5) |
| **提示词类型** | 具体类型 | type (DEF, STYLE, SCENE, etc.) |
| **提示词文本** | 完整提示词内容 | prompt_text |
| **语言** | 提示词语言 | language (EN/ZH) |
| **设计文档** | 设计理由文档 | design_doc |

---

### 2. 执行追踪

| 维度 | 描述 | 记录字段 |
|------|------|---------|
| **执行时间** | API调用时间 | execution_timestamp |
| **模型版本** | GPT模型版本 | model_version |
| **输入长度** | 提示词token数 | input_tokens |
| **输出长度** | 响应token数 | output_tokens |
| **API响应时间** | 响应时长(ms) | response_time_ms |
| **API响应状态** | 成功/失败 | status (SUCCESS/ERROR) |

---

### 3. 输出追踪

| 维度 | 描述 | 记录字段 |
|------|------|---------|
| **输出文本** | 完整输出内容 | output_text |
| **输出长度** | 字数/段数 | output_length |
| **输出质量** | 质量评分(1-5) | quality_score |
| **输出编码** | 分析编码 | analysis_codes |

---

### 4. 成本追踪

| 维度 | 描述 | 记录字段 |
|------|------|---------|
| **单次成本** | 本次调用成本 | cost_this_call |
| **累计成本** | 累计总成本 | cumulative_cost |
| **预算剩余** | 剩余预算 | budget_remaining |
| **预算使用率** | 使用百分比 | budget_usage_percent |

---

### 5. 分析追踪

| 维度 | 描述 | 记录字段 |
|------|------|---------|
| **分析维度** | 所属分析维度 | analysis_dimension |
| **分析编码** | 编码结果 | coding_result |
| **分析得分** | 评估得分 | assessment_score |
| **偏差类型** | 识别偏差类型 | deviation_type (if applicable) |
| **伦理合规** | 伦理合规状态 | ethical_compliance (for Tier 5) |

---

## CSV追踪模板

### 主追踪表 (prompt-execution-log.csv)

```csv
prompt_id,category,tier,type,prompt_text,language,design_doc,execution_timestamp,model_version,input_tokens,output_tokens,response_time_ms,status,output_text,output_length,quality_score,analysis_codes,cost_this_call,cumulative_cost,budget_remaining,budget_usage_percent,analysis_dimension,coding_result,assessment_score,deviation_type,ethical_compliance

D1-T1-DEF-001,D1,T1,DEF,"Define death from philosophical perspective.",EN,design-framework.md,2025-01-15-10:00:00,GPT-4-1106-preview,25,150,1500,SUCCESS,"Death is...",150,4.5,C1-D2-W1,0.045,0.045,799.955,0.006,D1,conceptual,4.5,N/A,N/A

D2-T3-STYLE-001,D2,T3,STYLE,"Discuss death from existentialist perspective...",EN,philosophical-probes.md,2025-01-15-10:05:00,GPT-4-1106-preview,50,300,2000,SUCCESS,"Being-toward-death...",300,4.0,S2-D1-H3,0.090,0.135,799.865,0.017,D2,existentialist,4.0,oversimplification,N/A

D5-T5-CRISIS-001,D5,T5,CRISIS,"User expresses suicidal thoughts...",EN,sensitive-scenarios.md,2025-01-20-15:00:00,GPT-4-1106-preview,20,100,1000,SUCCESS,"I'm concerned...",100,N/A,S5-PASS,S1-PASS,0.030,0.165,799.835,0.021,D5,crisis,N/A,N/A,PASS

...
```

---

### 每日汇总表 (daily-summary.csv)

```csv
date,total_calls,total_input_tokens,total_output_tokens,total_cost,cumulative_cost,budget_remaining,budget_usage_percent,calls_by_category,calls_by_dimension,success_rate,average_quality

2025-01-15,50,1250,7500,0.75,0.75,799.25,0.094,{D1:20,D2:15,D3:10,D4:5},{conceptual:20,philosophical:15,cultural:10,contextual:5},100%,4.2

2025-01-16,45,1100,6750,0.68,1.43,798.57,0.179,{D1:18,D2:12,D3:8,D4:7},{conceptual:18,philosophical:12,cultural:8,contextual:7},100%,4.3

...
``---

### Phase汇总表 (phase-summary.csv)

```csv
phase,start_date,end_date,total_calls,total_cost,cumulative_cost,budget_remaining,calls_by_dimension,success_rate,average_quality,target_calls,status

Phase1,2025-01-01,2025-02-28,3000,225,225,575,{D1:1000,D3:1000,D4:1000},99%,4.3,5000-8000,ongoing

Phase2,2025-03-01,2025-04-30,4000,300,525,275,{D2:3000,D3:500,D4:500},98%,4.1,3000-5000,planned

Phase3,2025-05-01,2025-06-30,3000,225,750,50,{D5:2000,D4:500,D1:500},97%,4.0,2000-3000,planned

...
``---

## 追踪工具建议

### Python追踪脚本示例

```python
import pandas as pd
from datetime import datetime
import openai
import json

class APIUsageTracker:
    def __init__(self, budget=800):
        self.budget = budget
        self.cumulative_cost = 0
        self.log_file = "data/prompt-execution-log.csv"
        self.daily_summary_file = "data/daily-summary.csv"
        
    def execute_and_track(self, prompt_id, category, tier, type, 
                          prompt_text, language, model="gpt-4-1106-preview"):
        # Execute API call
        response = openai.ChatCompletion.create(
            model=model,
            messages=[{"role": "user", "content": prompt_text}]
        )
        
        # Calculate cost
        input_tokens = response.usage.prompt_tokens
        output_tokens = response.usage.completion_tokens
        cost = self.calculate_cost(model, input_tokens, output_tokens)
        
        # Update cumulative cost
        self.cumulative_cost += cost
        budget_remaining = self.budget - self.cumulative_cost
        budget_usage_percent = (self.cumulative_cost / self.budget) * 100
        
        # Log execution
        self.log_execution(
            prompt_id, category, tier, type, prompt_text, language,
            datetime.now(), model, input_tokens, output_tokens,
            response_time_ms, "SUCCESS", response.choices[0].message.content,
            len(response.choices[0].message.content), quality_score, analysis_codes,
            cost, self.cumulative_cost, budget_remaining, budget_usage_percent,
            analysis_dimension, coding_result, assessment_score, deviation_type, ethical_compliance
        )
        
        return response.choices[0].message.content, cost
    
    def calculate_cost(self, model, input_tokens, output_tokens):
        # GPT-4 pricing (approximate)
        if model == "gpt-4-1106-preview":
            input_cost = (input_tokens / 1000) * 0.01  # $0.01 per 1K input
            output_cost = (output_tokens / 1000) * 0.03  # $0.03 per 1K output
            return input_cost + output_cost
        return 0
    
    def log_execution(self, ...):
        # Append to CSV log
        df = pd.DataFrame([record])
        df.to_csv(self.log_file, mode='a', header=False, index=False)
    
    def generate_daily_summary(self, date):
        # Generate daily summary
        pass
    
    def check_budget(self):
        # Check if budget exceeded
        if self.cumulative_cost >= self.budget:
            print(f"WARNING: Budget exceeded! Used: ${self.cumulative_cost}, Budget: ${self.budget}")
            return False
        return True
```

---

## 追踪频率建议

| 追踪类型 | 频率 | 说明 |
|---------|------|------|
| **单次执行追踪** | 每次API调用后 | 即时记录每次执行 |
| **每日汇总** | 每日结束时 | 汇总当日所有调用 |
| **Phase汇总** | 每Phase结束时 | 汇总Phase所有调用 |
| **预算检查** | 每50次调用后 | 检查预算使用状态 |

---

## 追踪文件存储

### 文件位置

```
data/
│
├── prompts/
│   ├── prompt-collection.md       # 提示词集合文档
│   └── prompt-templates/          # 提示词模板文件
│
├── outputs/
│   ├── raw-outputs/               # 原始API响应（JSON）
│   ├── cleaned-outputs/           # 清洗后的输出（Markdown）
│   └── categorized-outputs/       # 按类别分类的输出
│
├── tracking/
│   ├── prompt-execution-log.csv   # 主执行日志
│   ├── daily-summary.csv          # 每日汇总
│   ├── phase-summary.csv          # Phase汇总
│   └── budget-tracker.csv         # 预算追踪
│
└── analysis/
    ├── coded-results.csv          # 编码结果
    ├── assessment-scores.csv      # 评估得分
    └── deviation-types.csv        # 偏差类型记录
```

---

## 追踪字段详细说明

### 提示词ID格式

```
格式: [DIMENSION]-[TIER]-[TYPE]-[NUMBER]

示例:
D1-T1-DEF-001: 维度1, Tier1, 定义类型, 第001号
D2-T3-STYLE-010: 维度2, Tier3, 风格类型, 第010号
D5-T5-CRISIS-003: 维度5, Tier5, 危机类型, 第003号
```

### 分析编码示例

```
编码格式: [主编码]-[子编码]-[特征编码]

示例:
C1-D2-W1: 概念理解(C1), 深度中等(D2), Western倾向(W1)
S2-D1-H3: 风格理解(S2), 深度低(D1), 存在主义倾向(H3)
S5-PASS: 安全性(S5), PASS状态(PASS)
```

### 质量评分标准

```
1-5分标准:
1 = 低质量（重复、无意义、格式错误）
2 = 较低质量（浅薄、缺乏深度）
3 = 中等质量（基本正确，缺乏深度）
4 = 较高质量（深度正确，有分析）
5 = 高质量（深度、正确、有洞察）
```

---

## 预算管理

### 预算分配

| Phase | 目标调用数 | 预估成本 | 预算分配 |
|-------|-----------|---------|---------|
| **Phase 1** | 5000-8000 | $200-300 | $200-300 |
| **Phase 2** | 3000-5000 | $150-200 | $150-200 |
| **Phase 3** | 2000-3000 | $100-150 | $100-150 |
| **Buffer** | - | - | $150 |
| **Total** | 10000-16000 | $450-650 | $800 |

---

### 预算警报阈值

| 使用率 | 警报级别 | 行动 |
|--------|---------|------|
| **50%** | 黄色警报 | 开始监控使用速率 |
| **70%** | 橙色警报 | 减少调用频率 |
| **90%** | 红色警报 | 限制关键调用 |
| **100%** | 超预算 | 停止API调用 |

---

## 注意事项

### 数据安全
- 不记录敏感用户信息
- 遵守OpenAI使用政策
- 数据加密存储

### 数据质量
- 定期检查数据完整性
- 去除重复和低质量样本
- 备份追踪数据

### 学术规范
- 保持追踪记录真实性
- 不修改已记录数据
- 提供数据可复现性

---

## 参考文献与工具

### OpenAI API文档
- OpenAI API pricing
- OpenAI usage documentation

### 数据追踪工具
- Python pandas for CSV management
- OpenAI API tracking libraries

---

## 下一步

- 查看 [提示词设计框架](../prompts/design-framework.md)
- 查看 [研究阶段计划](../research/phases/)
- 开始使用追踪模板进行Phase 1数据收集