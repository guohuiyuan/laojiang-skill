# 老蒋.skill · 商业评论写作法

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](LICENSE)

> **把「老蒋巨靠谱」的判断方式，整理成一套可执行的写作方法。**
>
> 不是学他说话，是学他怎么把一件热事拆到机制层，再落回普通人身上。

---

## 这是什么

一个给 AI agent 用的 Skill。加载后，它能按同一套骨架写中文商业/社会评论：

- 从一个具体事件切入，不写综述
- 给一个**可被反驳**的判断，不打太极
- 分三层拆到机制，讲清钱怎么分、成本转给谁
- 用类比把陌生机制翻译成日常经验
- 收尾给一个普通人明天能做的动作

素材来源是 **149 篇单口视频的文字稿，137 万字，64.6 小时**，全部通过 Whisper 转写、逐篇校对后归档。

## 核心数据

| 指标 | 数值 |
|---|---|
| 单口视频 | **149 篇**（已剔除 61 篇多人/播客、11 篇 vlog） |
| 文稿总字数 | **137 万字** |
| 总时长 | **64.6 小时** |
| 平均语速 | 352.7 字/分钟 |
| 平均句长 | 38 字（中位 29，P90 65） |
| 每千字「我」/「你」 | 15.2 / 7.3 次 |
| 时间跨度 | 2019-07 ～ 2026-11 |

六个可复用的判断模型 + 12 条决策启发式，全部标注了可核查的原始篇目。

## 安装

### 克隆到 skills 目录

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

### 作为参考资料

不支持 Agent Skills 的 runtime，也可以直接把 `SKILL.md` 贴进对话——它本质就是 markdown + YAML frontmatter。

## 怎么用

### 写稿

> 「写一期讲『AI 生成内容挤压中腰部创作者』的稿子，20 分钟量级。」

会先按 `01-选题与角度` 定角度（不是「AI 太强」，而是「平台把成本转给了谁」），再用 `02-开篇六式` 的第四式开场，按 `03-论证推进` 搭三层结构，最后用 `05-收尾` 收。

### 审稿

> 「这是我写的稿子，帮我看看为什么读起来很空。」

按 `03` 的四问自检：有没有机制层？有没有代价层？类比是不是只在装饰？有没有交代谁付钱？

### 拆解

> 「这条视频为什么立得住？」

用 `06-心智模型` 里的六个模型逐条套：它的反常在哪、位置交代了吗、有没有落到个体。

### 核查

> 「老蒋真的这么说过吗？」

在 `references/transcripts/` 里 grep 原句，给文件名和上下文。文稿带 `[hh:mm:ss]` 时间戳，可以直接跳到原视频位置核对。

## 文件结构

```
laojiang-skill/
├── README.md                          # 你在这里
├── SKILL.md                           # 主指令：流程、底线、语感校准
├── references/
│   ├── 01-选题与角度.md               # 六个选题池、反常识四法、标题形态
│   ├── 02-开篇六式.md                 # 六种开场 + 组合模板 + 三不要
│   ├── 03-论证推进.md                 # 五层模型、四种硬料、三个必用动作
│   ├── 04-语言与口癖.md               # 句长、代词、口癖分级、AI 味清除表
│   ├── 05-收尾与自我定位.md           # 三固定件、五种收尾
│   ├── 06-心智模型与启发式.md         # 6 个模型 + 12 条启发式
│   └── transcripts/                   # 149 篇原文稿（带时间戳）
├── assets/
│   └── examples/
│       └── 三段开场拆解.md            # 逐句拆三个真实开头
└── data/
    ├── catalog.md                     # 全量索引（发布/时长/播放/字数）
    ├── stats.json                     # 统计口径原始数据
    ├── ritual.json                    # 仪式化特征命中率
    └── skeleton.md                    # 149 篇结构骨架（开头/转折/收尾）
```

## 素材是怎么来的

1. **抓清单**：B 站空间 wbi 接口，拿到 221 个投稿（2019-07 ～ 2026-11）
2. **筛单口**：用联合投稿 staff + 标题规则 + 人工逐条判断，剔除 61 篇多人/播客/访谈、11 篇外拍 vlog，留下 149 篇
3. **下载音轨**：yt-dlp 4 路并发，原始 m4a 不转码
4. **转写**：faster-whisper large-v3-turbo，批量推理 16 窗口 + 词级时间戳重建句子，50x 实时
5. **校对**：热词提示修正专有名词（字节系、红果短剧等），半角标点转全角
6. **提炼**：统计 + 结构骨架 + 逐篇阅读，归纳模型

采集与转写只依赖公开工具（yt-dlp、faster-whisper）和 B 站公开接口，本仓库不包含音视频文件，只保留文字稿。

## 已知局限

- **转写会有错字**。人名、产品名尤其，稿子里保留原样，核查时以视频为准
- **风格是归纳的，不是他本人授权的**。这六个模型是我从他 149 篇稿子里读出来的，不是他声明过的框架
- **只有单口**。他的对谈、访谈、播客（49.7 小时）全部剔除，因为那些是对话，不是他的完整输出
- **不包含 2026-11 之后的投稿**。采集截止到 2026-11-16
- **不适合**资讯播报、产品测评、严肃研究报告——这套方法的核心是「有立场」，那几类需要的是中立

## 版权

- **文稿版权**属于原作者「老蒋巨靠谱」。本仓库仅收录其公开视频的文字转写，用于个人学习与研究，不用于商业用途。如原作者认为不妥，请联系删除。
- **本仓库的代码与文档**（`SKILL.md`、`references/` 中的方法论章节、`data/` 中的统计产物、README 等）采用 **GNU Affero General Public License v3.0** 授权。

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
