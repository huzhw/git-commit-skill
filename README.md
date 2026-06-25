# git-commit

中文 Git 提交规范 —— 逐文件暂存、原子拆分、说人话的提交信息。

## 干什么

- **逐文件暂存** — 禁止 `git add -A`，只看改动再 stage
- **中文提交信息** — 写原因不写过程，一句话说清为什么改
- **原子拆分** — 一件事一个 commit，不混入无关改动
- **提交前检查** — 编译通过、无无关文件、密钥不上传
- **禁止项** — 不要 Co-Authored-By、不要 `--no-verify`

## 为什么干

大多数 AI 提交工具就是 `git add -A && git commit -m "update"` 一把梭，出来的历史没法看。这个把人工提交的规范编码好，提交信息说人话、一个 commit 一件事、改前先看、改完检查。

## 安装

```bash
git clone https://github.com/huzhw/git-commit-skill.git ~/.claude/skills/git-commit
```

## 许可

MIT
