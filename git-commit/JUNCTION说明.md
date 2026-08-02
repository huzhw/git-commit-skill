# JUNCTION 说明 — git-commit

> 本目录已与全局 skill 目录建立 junction，**实时双向同步，改哪边都一样**。

## 指向关系

| 项 | 路径 |
|----|------|
| 全局路径（junction） | `C:\Users\Administrator\.claude\skills\git-commit` |
| 实际目录（F 仓库） | `F:\idea-workspase-skills\claude-git-commit-skill\git-commit` |
| 创建日期 | 2026-08-02 |

## 说明

- ⚠️ **特殊：junction 指向的是 F 仓库 `claude-git-commit-skill` 的 `git-commit/` 子目录，不是仓库根目录**。
  原因：该仓库结构里 SKILL.md 位于 `git-commit/` 子目录下，全局 `git-commit` skill 需要 SKILL.md 在根，所以只能指到子目录。
- 修改本 skill 时，文件实际位于 `F:\idea-workspase-skills\claude-git-commit-skill\git-commit\` 下。
- 仓库根目录的 `README.md` 不在 junction 范围内（全局 git-commit 目录看不到它）。

## 检查是否正常

```bash
cmd /c dir "C:\Users\Administrator\.claude\skills" | findstr git-commit
```

正常应显示 `<JUNCTION>  ...  git-commit`。

## 回滚方法（恢复成独立副本）

```bat
rd "C:\Users\Administrator\.claude\skills\git-commit"
xcopy "F:\idea-workspase-skills\_skills_backup_20260802\git-commit" "C:\Users\Administrator\.claude\skills\git-commit" /E /I /Y
```

> 注意：`rd` 不要加 `/s`，否则可能递归进 F 源目录。

## 本 skill 特殊差异

- junction 前已确认：F `git-commit/SKILL.md` 与全局 `git-commit/SKILL.md` 内容完全一致（md5 相同，4032B），无丢失。
- 全局 git-commit 目录原本只有 SKILL.md 一个文件。
- 备份位置：`F:\idea-workspase-skills\_skills_backup_20260802\git-commit`（1 个文件）。
