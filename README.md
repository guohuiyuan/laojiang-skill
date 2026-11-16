# 老蒋.skill · 一套可以运行的思维方式

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](LICENSE)

> **把 B 站 UP 主「老蒋巨靠谱」怎么判断一件事，整理成一套能直接跑起来的视角。**
>
> 不是学他说话，是学他怎么把一件热事拆到机制层，再落回普通人身上。

## 这是什么

一个给 AI agent 用的人物 Skill，按 [女娲 · Skill 造人术](https://github.com/alchaincyf/nuwa-skill) 的方法蒸馏。
加载之后，它会用「我」以老蒋的视角回答问题——遇到一件争议、一个商业模式、一次分赃不均，它会：

- 先数这条链上有几个角色，是不是同一个人
- 先交代自己站在哪，再给判断
- 把判断压成能数得清的几句，逐句展开
- 替你把反对意见说完，再打掉
- 最后给一个明天能做的动作

**素材底盘**：149 篇单口视频，64.6 小时，137 万字，2019-07 至 2026-11 全量转写并逐篇校对。

## 装

```bash
git clone https://github.com/guohuiyuan/laojiang-skill.git ~/.workbuddy/skills/laojiang
```

Claude Code、Codex、Cursor 等 runtime 换对应目录：

| Runtime | 路径 |
|---|---|
| WorkBuddy | `~/.workbuddy/skills/laojiang/` |
| Claude Code | `~/.claude/skills/laojiang/` |
| Codex CLI | `~/.codex/skills/laojiang/` |
| Cursor | `~/.cursor/skills/laojiang/` |

不支持 Agent Skills 的 runtime，也可以直接把 `SKILL.md` 贴进对话——它本质就是 markdown + YAML frontmatter。

## 用

**问观点**

> 「用老蒋的视角看：短视频平台给创作者的激励越来越少，这事儿怨谁？」
>
> → 它会先拆这条链上版权、制作、分发、分账是不是同一家，再谈「怨谁」。

**拆一件事**

> 「老蒋会怎么看『年轻人不愿意和邻居打交道』？」
>
> → 它会把它重新描述成成本与不确定性问题，给出代价层，再用一个具体作品做类比——而不是说「社恐」。

**审自己的稿子**

> 「这是我写的评论，帮我看看为什么读起来很空。」
>
> → 按招式自检：有没有机制层？有没有代价层？类比是不是只在装饰？有没有交代谁付钱？

**核查**

> 「老蒋真的这么说过吗？」
>
> → 在 `references/sources/transcripts/` 里 grep 原句，给文件名和 `[hh:mm:ss]`，可以直接跳到原片位置。

## 里面有什么

```
laojiang-skill/
├── SKILL.md                        # 核心：运行纪律 + 招式 + 心智模型 + 声音 + 案例索引 + 边界
├── FIDELITY.md                     # 验证结果与已知薄弱项
└── references/
    ├── casebook.md                 # 14 张案例卡（处境 / 他做了什么 / 原话 / 后来 / 可类比到 / 出处）
    ├── voice.md                    # 10 段原话，按场合分组
    ├── research/                   # 调研底稿
    │   ├── 00-prior.md             # 动手前的先验快照（复盘补写，非盲写）
    │   ├── 01-writings.md          # 149 篇系统输出：六个选题池、系列谱系、五层推进
    │   ├── 02-conversations.md     # 12 篇访谈/圆桌：他怎么提问、怎么即兴
    │   ├── 03-expression-dna.md    # 全量统计：句长、代词、口癖命中率
    │   ├── 04-external-views.md    # 他者视角（最薄的一路，如实标注）
    │   ├── 05-decisions.md         # 12 个决策记录与行动
    │   ├── 06-timeline.md          # 时间线、播放前十、转折点
    │   └── holdout.md              # 3 件封存件（验证用，内容不进 Skill）
    └── sources/
        └── transcripts/            # 149 篇原文稿，带时间戳
```

另有 `data/` 存全量统计的原始数值（`stats.json`、`ritual.json`、`catalog.md`、`skeleton.md`），可复算。

## 六个心智模型

| 模型 | 一句话 |
|---|---|
| 机制优先于道德 | 先问规则谁定、钱怎么分，再问对错 |
| 位置决定观点 | 不交代位置的观点默认不可信 |
| 反常即结构 | 习以为常的事里讲不通的地方，就是结构裂缝 |
| 圈层内部逻辑优先 | 先用它自己的规则解释它，别用外部道德审判 |
| 整体结论 ≠ 个体命运 | 数据成立不等于每个人都成立 |
| 表达的边界感 | 可以说狠话，但要清楚边界在哪，并且说出来 |

每个模型都写了**什么时候不灵**，而且用的是他自己栽过的例子（比如讲 ASOUL 那年真的「入脑」了，同化之后就没有判断距离）。

## 八个招式

先数这条链上有几个角色 → 开口先交代我站在哪 → 先替对方把逻辑讲通 → 找那个「本来应该却没有」的反常 → 把判断压成能数得清的几句 → 替你把反对意见说完再打掉 → 主动交出我最大的漏洞 → 最后给一个明天能做的动作。

每个招式都有触发情境、可照做的动作、和一处带时间点的出处。

## 素材是怎么来的

1. **抓清单**：B 站空间 wbi 接口，拿到 221 个投稿（2019-07 ～ 2026-11）
2. **筛单口**：用联合投稿 staff + 标题规则 + 人工逐条判断，剔除 61 篇多人/播客/访谈、11 篇外拍 vlog，留下 149 篇
3. **下载音轨**：yt-dlp 4 路并发，原始 m4a 不转码
4. **转写**：faster-whisper large-v3-turbo，批量推理 16 窗口 + 词级时间戳重建句子，约 50x 实时
5. **校对**：热词提示修正专有名词（字节系、红果短剧等），半角标点转全角
6. **蒸馏**：先写先验快照 → 六路底稿 → 封存 3 件考题 → 提炼招式/模型/案例卡 → 机检 → 对照测试

采集与转写只依赖公开工具（yt-dlp、faster-whisper）和 B 站公开接口，本仓库不包含任何音视频文件，只保留文字稿。

## 已知局限

- **转写会有错字**。人名、产品名尤其，稿子里已按音校正明显错字，但核查时仍以原片为准
- **他者视角几乎是空的**。没有采集评论区、弹幕、第三方报道，所以「别人怎么看他」只有他自己的转述（见 `references/research/04-external-views.md`）
- **只有单口为主**。他的对谈、访谈、播客（49.7 小时）只用了 12 篇样稿
- **不包含 2026-11 之后的内容**。采集截止 2026-11-16
- **风格是归纳的，不是他本人授权的**。六个模型是从他 149 篇稿子里读出来的，不是他声明过的框架
- **不适合**拿它做行业专业判断（医疗、法律、硬科技），它是一个评论者的视角

## 版权与许可

- **文稿版权**属于原作者「老蒋巨靠谱」。本仓库仅收录其公开视频的文字转写，用于个人学习与研究，不用于商业用途。如原作者认为不妥，请联系删除。
- **本仓库的代码与文档**（`SKILL.md`、`references/` 中的方法论章节与数据产物、README 等）采用 **GNU Affero General Public License v3.0** 授权。

## License

[AGPL-3.0](LICENSE)

```
Copyright (C) 2026 guohuiyuan

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
```

选择 AGPL 而非 MIT：这是一套会被拿去直接生成内容的规则集合，AGPL 要求衍生作品（包括以网络服务形式提供）同样开源，能避免被闭源包装后再分发。
