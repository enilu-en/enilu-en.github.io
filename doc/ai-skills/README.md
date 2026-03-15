# AI Skills 说明

本目录包含 AI 工具（如 Claude、Codex）在处理本项目时应遵循的任务执行规范。

## 目录结构

```
doc/ai-skills/
├── common/          # 跨工具复用的通用 skills
│   ├── blog-post/   # 博客文章相关任务的 skill
│   ├── code-quality/ # 代码质量优化与规范
│   └── site-config/  # 网站配置管理
└── claude/          # Claude 专属 skills（如有）
```

## 执行流程

1. 任务开始前，AI 应先扫描本目录下的 skills
2. 命中相关 skill 后，先执行 skill 流程再实施改动
3. skill 信息缺失时，先向用户确认再继续
4. 命中异常时，按通用规则执行

## 公共规则

- 所有 skills 内容聚焦流程与约束，不堆砌项目背景
- 目录名保持稳定，避免频繁改名
- 复杂说明拆到 references/ 目录
- 可执行辅助脚本放 scripts/ 目录
