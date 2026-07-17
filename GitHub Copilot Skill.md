1. 先确定 Skill 的使用场景

一个好的 GitHub Copilot Skill 应该解决一个重复问题。

不推荐：
Software Engineer Helper

太泛。

推荐：
React Component Reviewer
API Security Auditor
Database Migration Assistant
Unit Test Generator
PR Review Assistant


2. Skill 的基本结构

一个典型 skill 可以类似：
```
.github/
└── skills/
    └── api-review/
        ├── SKILL.md
        ├── examples/
        │   └── example.md
        └── templates/
            └── review-template.md
```
核心文件：
``
SKILL.md
```

3. SKILL.md 推荐结构

例如：
```
# API Review Skill

## Purpose

Review REST APIs for design quality, security,
performance and maintainability.

## When to use

Use this skill when:
- Reviewing API changes
- Reviewing OpenAPI specifications
- Reviewing backend PRs

Do not use when:
- Writing frontend code
- Reviewing documentation only


## Instructions

Follow these steps:

1. Analyze API endpoints.
2. Check request/response models.
3. Validate authentication.
4. Identify breaking changes.
5. Suggest improvements.


## Review Checklist

Security:
- Authentication required
- Authorization validated
- Input validation present

Performance:
- Pagination supported
- Avoid unnecessary queries

API Design:
- Correct HTTP methods
- Consistent naming


## Output Format

Return:

## Summary

## Issues Found

| Severity | Location | Problem | Recommendation |

## Suggested Changes


## Examples

Input:
"Review this API change"

Output:
...

4. 给 Copilot 明确“什么时候用”

这是 skill 成功率最高的因素。

例如：

不好： Help with APIs.

好：
```
Use this skill when:
- A user asks for API review
- A pull request modifies controller code
- OpenAPI files are changed
- Backend endpoints are added

```

5. 给 Copilot 一个执行流程

不要只写： Review code quality.

应该：
```
Process:

Step 1:
Identify changed files.

Step 2:
Classify changes:
- API
- Database
- UI
- Infrastructure

Step 3:
Apply relevant checklist.

Step 4:
Generate findings.

Step 5:
Suggest patches if possible.
```
Copilot 对 workflow 很敏感。

6. 利用 Repository Context

GitHub Copilot 最大优势是理解 repo。

Skill 应该告诉它如何使用：

例如：
```
Before making recommendations:

1. Read:
   - README.md
   - package.json
   - architecture docs

2. Identify:
   - Framework version
   - Coding conventions
   - Existing patterns

3. Follow existing style.
```

否则 Copilot 容易生成“正确但不适合项目”的代码。


7. 加入 Coding Rules

例如：
```
Coding standards:

Always:
- Use TypeScript strict mode
- Add unit tests
- Avoid any type
- Use existing utility functions

Never:
- Introduce new dependencies without approval
- Duplicate existing logic
```

8. 给 Example（非常重要）

Copilot 从例子学习非常快。

例如：
```
Example:

User:
Create a new API endpoint.

Bad response:
"Add endpoint in controller."

Good response:
1. Add route
2. Add validation schema
3. Add service layer method
4. Add tests
5. Update OpenAPI docs
```

9. Skill 不要写成“大百科”

常见错误：

❌ 2000 行规则
❌ 包含所有公司的技术文档
❌ 重复 README
❌ 把 API 文档全部复制进去

更好的方式：

Skill: 告诉 Copilot 怎么工作

Documentation: 告诉 Copilot 项目是什么

10. 高质量 GitHub Copilot Skill 模板
```
# Skill Name

## Goal
What this skill accomplishes.

## Trigger Conditions
Use when:
- 
-

## Context Required
Read:
-
-

## Workflow

1.
2.
3.

## Rules

Always:
-

Never:
-

## Tools Available

- Search repository
- Modify files
- Run tests

## Output

Expected response format.

## Examples

Example input/output.

```

11. 建议优先创建的 Copilot Skills

代码质量
1. PR Review Skill
2. Refactoring Skill
3. Test Generation Skill

架构
1. System Design Reviewer
2. API Design Reviewer
3. Database Migration Reviewer

DevOps
1. CI/CD Troubleshooter
2. Kubernetes Debugger
3. Terraform Reviewer

企业开发
1. Security Compliance Checker
2. Documentation Generator
3. Incident Report Generator
