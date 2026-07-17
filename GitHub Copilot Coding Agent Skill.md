# PR Code Review Skill, 帮助 Copilot 自动审查 Pull Request

1. Repository 目录结构

在你的 repo 中创建：
```
.github/
└── skills/
    └── pr-review/
        ├── SKILL.md
        ├── checklist.md
        └── examples/
            └── review-example.md
```

2. SKILL.md 完整示例
```
---
name: pr-review
description: Reviews pull requests for code quality, security, performance, and maintainability.
---

# PR Review Skill

## Purpose

This skill helps review code changes in pull requests.
It focuses on finding bugs, security issues, performance problems,
and maintainability concerns.

The goal is to provide actionable feedback that developers can apply.

---

## When to Use

Use this skill when:

- Reviewing a pull request
- Analyzing changed source code
- Checking code quality before merge
- Reviewing architectural impact of changes

Do not use this skill for:

- Writing new features from scratch
- Explaining basic programming concepts
- Generating documentation only

---

# Review Process

Follow these steps.

## Step 1: Understand Repository Context

Before reviewing:

1. Read:
   - README.md
   - package.json / pom.xml / requirements.txt
   - Architecture documentation if available

2. Identify:
   - Programming language
   - Framework
   - Coding conventions
   - Existing patterns


---

## Step 2: Analyze Changes

Review:

### Correctness

Check:

- Logic errors
- Edge cases
- Null handling
- Error handling
- Race conditions


### Security

Check:

- Authentication
- Authorization
- Input validation
- Sensitive data exposure
- Injection risks


### Performance

Check:

- Database queries
- Memory usage
- Unnecessary API calls
- Algorithm complexity


### Maintainability

Check:

- Code readability
- Duplication
- Naming
- Test coverage
- Dependency changes


---

# Coding Rules

Follow repository conventions.

Always:

- Prefer existing utilities over new implementations
- Add tests for behavior changes
- Keep changes focused
- Explain the reason behind findings


Avoid:

- Suggesting unnecessary rewrites
- Introducing new dependencies without justification
- Changing unrelated code


---

# Output Format

Return review comments using this format:


## Summary

Brief overview of the PR.


## Findings


| Severity | File | Location | Issue | Recommendation |
|---|---|---|---|---|
| High | file.ts | line 20 | Problem | Fix |


Severity levels:

Critical:
Security vulnerability or production outage risk.

High:
Bug or major maintainability issue.

Medium:
Potential issue or improvement.

Low:
Style or minor suggestion.


## Positive Observations

Mention good practices found.


## Suggested Next Steps

List recommended actions.
```

3. Checklist 文件

.github/skills/pr-review/checklist.md
```
# PR Review Checklist


## Security

- [ ] Authentication verified
- [ ] Authorization checked
- [ ] User input validated
- [ ] Secrets not exposed


## Reliability

- [ ] Error handling exists
- [ ] Failure scenarios handled
- [ ] Logging is sufficient


## Performance

- [ ] No unnecessary database calls
- [ ] No inefficient loops
- [ ] Pagination considered


## Testing

- [ ] Unit tests added
- [ ] Existing tests updated
- [ ] Edge cases covered


## Maintainability

- [ ] Naming is clear
- [ ] Code follows project style
- [ ] No duplicated logic
```

4. Example 文件

.github/skills/pr-review/examples/review-example.md
```
# Example Review


## Input

A PR changes:

src/payment/service.ts


## Output


## Summary

The payment validation logic was improved,
but there is a missing authorization check.


## Findings


| Severity | File | Location | Issue | Recommendation |
|-|-|-|-|-|
| High | service.ts | 45 | Missing ownership validation | Verify user owns payment before processing |


## Positive Observations

- Error handling was improved.
- Unit tests were added.
```

5. 更高级：加入自动修复能力

如果你希望 Copilot 不只是 review，而是修复：

增加：
```
## Auto Fix Rules

When a safe fix is obvious:

1. Explain the issue.
2. Generate a patch.
3. Run relevant tests.
4. Summarize changes.

Do not modify:
- Authentication logic
- Database schema
- Production configuration
without confirmation.
```

6. 另一个常用 Skill：Test Generator

结构：
```
.github/
└── skills/
    └── test-generator/
        └── SKILL.md
```
用途：

1. 自动分析 class/function
2. 创建 unit test
3. Mock dependencies
4. Cover edge cases

7. 企业团队推荐 Skill 组合

```
.github/
└── skills/

    ├── pr-review/
    │
    ├── security-review/
    │
    ├── test-generator/
    │
    ├── api-design-review/
    │
    ├── migration-helper/
    │
    └── documentation-generator/
```

设计经验总结

一个优秀 Copilot Skill 通常包含：

|部分	| 作用|
|----| ---|
|Frontmatter	|告诉 Copilot 这是什么|
|Purpose	|定义目标|
|When to use	|控制触发|
|Context	|告诉它读什么|
|Workflow	|规定步骤|
|Rules	|限制行为|
|Output format	|保证一致性|
|Examples	|提高准确率|

如果你要做生产级 GitHub Copilot Skill，下一步通常是加入：

1. agents.md（项目级行为规范）
2. copilot-instructions.md（仓库级规则）
3. 多个 skills 的路由设计

这三者组合起来，效果会比单个 SKILL.md 强很多。
