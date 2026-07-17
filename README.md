# skill-guider
1. 先定义 Skill 的边界（最重要）

一个好的 skill 通常满足：

一个 skill = 一个稳定目标 + 一套明确流程 + 一个可验证输出

```
Skill 名称：
Sales Pipeline Analyzer

目标：
分析销售机会数据，输出风险、预测收入和下一步行动

输入：
CSV/XLSX 销售数据

输出：
1. Pipeline summary
2. Deal risk list
3. Forecast
4. Recommended actions
```


2. 设计 Skill 的触发条件
应该明确：

When to use

例如：
```
Use this skill when:
- 用户提供销售数据
- 用户要求预测收入
- 用户询问 pipeline 健康度
- 用户要求生成销售报告
```

3. 写清楚输入格式
好的 skill 会告诉模型：
用户可能提供什么：
```
Inputs:

Required:
- Dataset containing:
  - opportunity name
  - stage
  - amount
  - close date

Optional:
- sales owner
- region
- historical conversion rate
```
避免模型猜。

4. 给出执行流程（Workflow）
不要只告诉 AI：“分析数据”

应该告诉它：
```
Process:

Step 1:
Validate input columns.

Step 2:
Calculate:
- total pipeline
- weighted pipeline
- win probability

Step 3:
Identify:
- stalled deals
- high-value risks

Step 4:
Generate recommendations.
```


5. 定义输出格式
这是提升质量最大的地方。
例如：

不要：Provide a report.

改：
```
Output:

## Executive Summary

## Key Metrics
| Metric | Value |

## Risks
- Deal:
- Issue:
- Impact:

## Recommendations
1.
2.
3.
```

6. 加入判断规则
优秀 skill 不只是流程，而是有“决策逻辑”。
例如：
```
If:
Close date < 30 days
AND
No activity >14 days

Then:
Mark as HIGH RISK
```
或者：
```
If confidence < 50%:
Do not include in forecast.
```

7. 提供失败处理
现实里输入经常不完整。

加入：
```
If required data is missing:

1. Identify missing fields.
2. Ask user only for those fields.
3. Do not generate assumptions.
```

8. 给 Skill 一个角色定位
例如：

不好： You are an assistant.

更好： You are a senior financial analyst specializing in SaaS revenue forecasting.

角色应该影响：

判断标准
语言风格
优先级

9. 使用示例（非常重要）
Skill 最好包含：

Example input
```
Upload:
Q3_sales.xlsx
```

Example output
```
Pipeline decreased 18%.

Main risk:
Enterprise deals delayed due to procurement.
```
模型通过 example 学习最快。
 
10.一个好的 Skill 模板
```
# Skill Name

## Purpose
This skill helps users...

## When to use
Use when:
- 
-

## Inputs
Required:
-

Optional:
-

## Workflow

1.
2.
3.

## Decision Rules

If:
Then:

## Output Format

## Limitations

## Examples

```





常见失败原因
❌ 太泛

“帮助用户管理项目”

↓

改：

“生成软件项目 sprint planning 文档”

❌ 没有输出格式

导致每次结果不同。

❌ 没有边界

模型不知道什么时候该用这个 skill。

❌ 依赖隐藏知识

例如：

“根据公司流程处理”

但没有提供流程。

❌ Skill 太长

不是越长越好。

通常：

目标：几句话
流程：10～30 行
规则：明确条件
示例：2～3 个

效果最好。
