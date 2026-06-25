# git-commit

把 Git 最佳实践编码为可复用的提交流程，告别 `git add -A && git commit -m "update"` 一把梭。

## 解决了什么问题

**AI 写代码很快，提交信息却很烂。** 常见的自动化提交工具就是全部暂存、信息敷衍、不拆分，出来的 Git 历史完全没法看 —— 回滚找不到 commit、blame 看不懂原因、review 不知道改了什么。

这个规范把人工提交的标准动作固定下来：先看改了什么、按逻辑拆分、写清楚为什么改、编译通过再提交。

## 完整流程

### 1. 先看再动

```bash
git status
git diff --stat
git diff
```

搞清楚改了什么、动了哪些文件、有没有混入无关改动。**禁止不看就直接 `git add`。**

### 2. 逐文件暂存

```bash
git add 具体文件路径
```

- 禁止 `git add -A` / `git add .`
- 只提交当前任务相关的文件
- 不提交临时文件（AI 生成的计划文件、缓存等）

### 3. 提交信息：说原因不说过程

**中文，一行说清为什么改，不超过 50 字。**

```
# 好：说原因，看了就知道为什么
修复登录页在 token 过期后直接白屏的问题
重构日期工具类，统一按东八区处理

# 差：说过程，diff 里已经能看到的
改了 Login.tsx
修了个 bug
```

diff 已经能看出改了什么代码，提交信息写的是**动机和原因**。

### 4. 正文：只在说不清的时候写

```
重构认证模块，jwt 改为 session 模式

原 jwt 方案在多节点部署时 token 同步延迟超过 5 秒，
改为 redis session 后延迟降到 10ms 以内。
```

非显而易见的设计决策、breaking change、大范围影响才写正文。一行能说清的别啰嗦。

### 5. 常见场景参考

| 场景 | 格式 |
|---|---|
| 修 bug | 修复 xxx 场景下 xxx 的问题 |
| 新功能 | 新增 xxx 功能，支持 xxx |
| 重构 | 重构 xxx，提取/统一 xxx |
| 文档 | 补充 xxx 模块文档 / 更新 xxx 说明 |
| 改配置 | 调整 xxx 配置，解决 xxx |
| 删代码 | 移除 xxx，已废弃/不再使用 |
| 性能 | 优化 xxx，xxx 场景从 N 降到 N |

### 6. 原子提交

一次只提交一件事：

- **原因不同 → 不同 commit。** 改了登录页又修了白屏 bug = 2 个 commit
- **原因相同 → 同一个 commit。** 新增接口 + 对应的 service + mapper = 1 个 commit
- **依赖变动单独提交。** `pom.xml` 加依赖是一个 commit，用依赖的功能代码是另一个

判断标准：写提交信息时如果用了「和」「以及」「同时」，就该拆。

### 7. 提交顺序

先低风险后高风险，出问题好精确定位和回滚：

```
文档 → 测试 → 改配置 → 修 bug → 新功能 → 重构
```

### 8. 提交前检查

- Java 项目：`mvnw compile -q` 编译通过
- 改动文件都是本次任务相关，没混入无关修改
- 新依赖的 `pom.xml` / `requirements.txt` 改动已单独拆出

### 9. 推送

```bash
git log --oneline -5   # 先看一眼提交记录
git push origin <分支名>
```

## 禁止项

- `git add -A` / `git add .`
- `git commit --no-verify`
- 提交临时文件（`.claude/plans/`、`docs/superpowers/` 等）
- 提交信息里加 `Co-Authored-By` 尾注
- 提交密钥、token、密码等敏感信息

## 安装

```bash
git clone https://github.com/huzhw/git-commit-skill.git ~/.claude/skills/git-commit
```

安装后在 AI 编码助手里说「提交代码」即可触发完整流程。

## 许可

MIT
