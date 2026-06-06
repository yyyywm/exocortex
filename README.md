# Exocortex

个人外接大脑皮层（Exocortex），基于 Obsidian + Quartz + GitHub Pages 构建。

## 快速开始

1. 阅读 `_system/00-README.md` 了解系统全貌
2. 阅读 `_system/06-初始化检查清单.md` 完成环境搭建
3. 在 Obsidian 中打开本文件夹，开始记笔记

## 目录结构

```
exocortex/
├── _system/          # 系统规范文档（操作手册）
├── content/          # 笔记内容（Quartz 源）
├── templates/        # Obsidian 模板
├── sources/          # 外部代码库（Git 子模块）
└── .github/          # GitHub Actions 工作流
```

## 规范文档

| 文档 | 说明 |
|------|------|
| [_system/01-架构规范.md](_system/01-架构规范.md) | 目录结构、命名、分类体系 |
| [_system/02-笔记规范.md](_system/02-笔记规范.md) | frontmatter、内容标准 |
| [_system/03-AI-操作规范.md](_system/03-AI-操作规范.md) | Claude Code 的 SOP |
| [_system/04-发布规范.md](_system/04-发布规范.md) | Quartz 配置与发布流程 |
| [_system/05-依赖与工具.md](_system/05-依赖与工具.md) | 软件清单与环境要求 |
| [_system/06-初始化检查清单.md](_system/06-初始化检查清单.md) | 从零复现步骤 |

## 使用方式

### 日常记录
打开 Obsidian，在 `content/` 下创建或编辑笔记。

### AI 辅助
```bash
cd ~/exocortex
claude
```
然后下达指令，如："执行 SOP-01，主题：XXX"。

### 发布博客
1. 在 `content/80-Blog/drafts/` 下写草稿
2. 完善后执行 SOP-04 发布
3. 或手动移动到 `posts/` 并设置 `draft: false`
4. `git push` 后自动部署到 GitHub Pages

## 博客地址

https://yourname.github.io/exocortex/

（请将 `yourname` 替换为你的 GitHub 用户名）
