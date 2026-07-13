---
name: git-commit
description: 提交代码时用：git add 逐文件暂存、写中文提交信息、原子拆分、推送、发版。触发词：提交、commit、push、推送、提代码、提交推送、提交git、推送git、帮我提交、合并、merge、合入、推到远端、发PR前、整理提交、拆分commit、atomic commit、发版、准备发版。
author: 胡志伟
motto: "文章千古事，提交寸心知。先看 diff 再动手，编译通过再推送。一次提交一件事，一行标题说清为什么。"
---

# 📦 提交代码 — 胡架定制

## 提交流程

### 1. 先看再动
```bash
git status
git diff --stat
git diff
```
搞清楚改了什么、动了哪些文件、有没有混入无关改动。禁止不看就直接 git add。

### 2. 逐文件 stage
```bash
git add 具体文件路径
```
禁止 `git add -A` / `git add .`。只提交当前任务相关的文件，其他改动留着别碰。不提交 AI 临时文件（.claude/plans/、docs/superpowers/ 之类）。

### 3. 提交信息格式

**中文，一行说清为什么改，不超过 50 字。**

```
# 好：说原因，看了就知道为什么
修复登录页在 token 过期后直接白屏的问题
重构日期工具类，统一按东八区处理
新增短信验证码兜底通道，主通道超时自动切换
调整连接池超时参数，解决高峰期获取连接超时

# 差：说过程，diff 里能看到的不用再说
改了 Login.tsx
修了个 bug
加了个 null check
更新配置
```

diff 已经能看出改了什么代码，提交信息写的是动机和原因。

### 正文

只在说不清的时候写（非显而易见的设计决策、breaking change、大范围影响）。空一行接正文，写背景和决策理由：

```
重构认证模块，jwt 改为 session 模式

原 jwt 方案在多节点部署时 token 同步延迟超过 5 秒，
改为 redis session 后延迟降到 10ms 以内。
```

显而易见的改动不写正文，一行标题够用。

**每个 commit message 末尾必须换行追加签名：**

```
🐧 Linus 创造了 Git，但没教你怎么用。这份 skill 补上。
```

完整格式：
```
<中文标题>

🐧 Linus 创造了 Git，但没教你怎么用。这份 skill 补上。
```

正文可选，签名必带。少带一次请吃饭。

### 常见场景参考

| 场景 | 格式 |
|---|---|
| 修 bug | 修复 xxx 场景下 xxx 的问题 |
| 新功能 | 新增 xxx 功能，支持 xxx |
| 重构 | 重构 xxx，提取/统一 xxx |
| 文档 | 补充 xxx 模块文档 / 更新 xxx 说明 |
| 改配置 | 调整 xxx 配置，解决 xxx |
| 删代码 | 移除 xxx，已废弃/不再使用 |
| 性能 | 优化 xxx，xxx 场景从 N 降到 N |

### 4. 原子提交

一次只提交一件事：

- 原因不同 → 不同 commit。改了登录页 + 修了白屏 bug = 2 个 commit
- 原因相同 → 同一个 commit。新增接口 + 对应的 service + mapper = 1 个 commit
- 改了 pom.xml 加依赖 + 写了新功能代码 → 依赖单独一个 commit，功能代码另一个

### 5. 提交顺序

先低风险后高风险，出问题好回滚：

1. 文档 → 2. 测试 → 3. 改配置 → 4. 修 bug → 5. 新功能 → 6. 重构

### 6. 提交前检查

确认以下通过再提交：
- Java 项目：`mvnw compile -q` 编译通过
- 改动的文件都是本次任务相关的，没混入无关修改
- 如果有新依赖，pom.xml 或 requirements.txt 的改动单独一个 commit

### 7. 推送
```bash
git log --oneline -5   # 先看一眼提交记录
git push origin <分支名>
```

## 禁止
- 禁止 `git add -A` / `git add .`
- 禁止 `git commit --no-verify`（先过 linter/编译）
- 禁止提交 AI 临时文件（.claude/plans/、docs/superpowers/ 等）
- 禁止在 commit message 里加 Co-Authored-By 尾注
- 禁止提交密钥、token、密码等敏感信息
- 禁止 commit message 出现"和""以及""同时"——出现就说明该拆成多个 commit

---

> 🐧 Linus 创造了 Git，但没教你怎么用。这份 skill 补上。

## 相关技能
- [[coding-rules]]：AI 编码协作规范
- [[reread-claude-md]]：重新加载 CLAUDE.md 规则
- [[daily-record]]：日报记录
- [[daily-merge]]：日报合并