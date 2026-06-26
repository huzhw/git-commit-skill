# 项目说明

一个 Git 提交规范技能，按中文习惯写提交信息，逐文件暂存，原子拆分。

## 目录结构

```
git-commit/
  SKILL.md      ← 技能本体，Claude 读取的指令
README.md       ← 人类看的说明
```

## 修改技能

编辑 `git-commit/SKILL.md`，保持 YAML 前页（name、description）不动，改下面的指令正文。

## 发布

改完提交推送即可，安装者下次 `git pull` 自动更新。

## 测试

本地安装到用户目录测试：

```bash
git clone https://github.com/huzhw/git-commit-skill.git ~/.claude/skills/git-commit
```

在任意项目中说「提交代码」触发，验证流程正确后推送发版。
