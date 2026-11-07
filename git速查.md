# Git 两课速查（读者席训练笔记原料）

> 2026-10-29 晚，亲手跑通的全部命令。建议：别只收藏，自己重抄一遍、每行加上自己的注释，那才是你的笔记。

## 第一课 · 存档基础

| 命令 | 作用 | 备注 |
|---|---|---|
| `git init` | 在当前文件夹建立仓库 | 一生一次 |
| `git status` | 看状态：谁改了、谁没存 | 最常用，没事就敲 |
| `git add 文件名` | 把文件放进暂存区 | 一次一个，或 `git add .` 全加 |
| `git commit -m "说明"` | 正式存档 | 说明写"为什么存" |
| `git log` | 看历史存档 | 加 `--oneline` 变缩写版 |
| `git diff` | 看这次到底改了什么 | 绿字 + 号 = 新增 |
| `git restore 文件名` | 救回"改了没存档"的改动 | 时间倒流，只救没存的 |

一次性配置（装好 git 后做一次，以后不用管）：

| 命令 | 作用 |
|---|---|
| `git config --global user.name "你的名字"` | 登记署名 |
| `git config --global user.email "你的邮箱"` | 登记署名 |
| `git config --global core.quotepath false` | 让中文文件名正常显示 |

## 第二课 · 分支与回退

| 命令 | 作用 | 备注 |
|---|---|---|
| `git branch` | 列出分支，`*` 是你站的那条 | |
| `git switch -c 分支名` | 创建分支并跳过去 | -c = create |
| `git switch 分支名` | 切换到已有分支 | |
| `git merge 分支名` | 把该分支并进当前分支 | 没分叉时显示 Fast-forward |
| `git reset --hard HEAD~1` | 回退一个存档点，连文件一起 | HEAD = 当前，~1 = 退一步 |
| `git branch -d 分支名` | 安全删除，未合并会拒绝 | 安全门 |
| `git branch -D 分支名` | 强制删除，无视警告 | 破门锤 |

## 核心概念（用自己的话背出来才算会）

- **三区模型**：工作区（正在写）→ 暂存区（add，圈定要存什么）→ 仓库（commit，装订入库）。
- **commit = 快照**：每次存档拍一张全貌照，随时读档。
- **HEAD**：你现在站着的那个 commit。`HEAD~1` = 后退一步，`HEAD~2` = 后退两步。
- **Fast-forward**：主线没动过时，merge 直接快进到支线位置，无冲突。
- **分工口诀**：restore 救"没存的"，reset 救"存错的"。
- **删除口诀**：`-d` 是安全门（先检查未合并的改动），`-D` 是破门锤（无视警告）。永远先用 `-d`。

## 亲手遇到过的报错（每个都是知识点）

| 报错 | 含义 | 解法 |
|---|---|---|
| `fatal: not a git repository` | 不在仓库里敲命令 | cd 到有 .git 的文件夹 |
| `Please tell me who you are` | 没登记身份 | 配 user.name / user.email |
| `fatal: you must specify path(s) to restore` | restore 没写文件名 | 补上路径 |
| `error: the branch 'X' is not fully merged` | 该分支有没并进来的改动 | 确认不需要后改 `-D` |
| `LF will be replaced by CRLF` | 换行符翻译警告 | 无害，不用管 |
| 文件名显示成 `\350\257\273...` | 中文名转义显示 | 配 core.quotepath false |

## 已预告、还没练（排队中）

- **冲突（conflict）**：下节课的大轴——两条线改同一行，git 判不了，要人工裁决。
- **`.gitignore`**：告诉 git 哪些文件别管，一行一个规则。
- **remote / push / pull / clone**：Gitee 云端联动四条，阶段 4–5 学。
- **stash / tag / reflog**：知道存在即可，reflog 是"后悔药的后悔药"。
