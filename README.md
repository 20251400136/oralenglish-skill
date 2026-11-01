# oralenglish-skill

专四口语（TEM-4 Oral）思辨话题陪练技能：AI 担任陪练教练，先抛出一个英文思辨话题（Topic）并给出一正一反两句纯英文参考句型，等待用户口头作答；作答后对用户口述做「转写 → 优化 → 点评」；随后用户可选择【继续】进行同话题深度追问，或【重新回答】重答当前话题，逐轮推进训练。

## 项目解决什么问题

专四口试（TEM-4 Oral）常考思辨类话题，要求考生即兴开口、有观点、表达地道。考生独自练习时普遍面临三个问题：

1. **没人出题**——自己练不知道该说什么话题，无法模拟考场"被提问后立刻作答"的压力；
2. **中式英语无人纠正**——开口后说不出哪里不地道，直译语序、中式搭配反复出现却无人指正；
3. **没有改进闭环**——练完没有"哪里错、怎么改、下一轮怎么练"的结构化反馈，练了等于白练。

本技能让 AI 充当随叫随到的陪练教练，形成「出题 → 开口 → 纠错 → 优化 → 再开口」的完整闭环，帮助用户在对话中完成真实的口语思辨训练。

## 主要功能

- **思辨话题出题**：每轮抛出一个英文 Topic（附一行中文释义），覆盖教育、科技、环保、社会、校园等专四常考领域，且逐轮避免重复；
- **参考句型引导**：每轮给出一正一反两句纯英文参考句型，用户开口前即可套用；
- **原句转写**：①【我的原句】原样保留用户口述，一字不改（含语法错误、口头语、口头缩写）；
- **表达优化**：②【优化句】仅生成 1 版，优先修正中式英语（直译语序、中式搭配、逻辑断层、母语负迁移），拒绝浅层同义词替换，核心改动加粗标出，适配口头表达；
- **针对性点评**：③【简短点评】点明本次中式英语问题，并简述逻辑、句式、用词地道度；
- **逐轮推进**：【继续】基于当前话题深度追问并开启新一轮；【重新回答】不换话题重答、循环反馈，直到用户满意。

## 目录结构

```
oralenglish-skill/
├── SKILL.md            # 技能定义与训练协议（入口）
├── agents/
│   └── openai.yaml     # OpenAI 格式技能元数据
├── LICENSE             # MIT 许可证
└── README.md           # 本说明
```

## 安装方法

本项目是**纯文本指令型技能**：只包含 SKILL.md 与 openai.yaml，无脚本、无依赖、无外部 API 调用，因此安装非常简单——让支持 Skill 的 AI Agent 能读到本目录即可：

1. **复制目录**：将本项目整体复制/放入你所使用 Agent 的技能（skills）目录，例如 Claude Code、OpenAI Codex / Agents SDK 或豆包等桌面 Agent 的用户技能目录（如 `workspace/.user_skills`）。具体路径以你所用 Agent 的 Skill 文档为准。
2. **重启会话**：重启或新建会话，让 Agent 重新扫描技能目录，之后即可通过技能描述自动触发。
3. **无需额外步骤**：不需要安装依赖、不需要构建、不需要配置 API Key。

**最小用法**：不想安装也没关系——把 `SKILL.md` 的内容直接作为指令粘贴给任意 AI 助手，同样可以按协议进行训练。

## 使用方法

1. 对助手说 **"开始专四口语思辨训练"**（或直接表达想练思辨话题）；
2. 助手输出 **Topic + 两句参考句型**（一正一反，纯英文），然后停下等你作答；
3. 你**口头作答**（英文，怎么想就怎么说）；
4. 助手输出 **①【我的原句】②【优化句】③【简短点评】** 三段反馈；
5. 输入 **【继续】**（同话题深度追问，进入新一轮）或 **【重新回答】**（同话题重答，循环反馈），逐轮推进。

## 输入 / 输出示例

**输入（用户）：** 开始训练

**输出（AI）：**

> **Topic:** Should college students take part-time jobs during the semester?（在校大学生该不该在学期中兼职？）
>
> **参考句型：**
> - 肯定：Taking a part-time job can help students ... because ...
> - 否定：Although part-time jobs may ..., they can also ..., which means ...

**输入（用户作答）：**

> I think student should do part-time job, because it can train our ability and reduce family burden. Also can get some working experience.

**输出（AI 反馈）：**

> ①【我的原句】I think student should do part-time job, because it can train our ability and reduce family burden. Also can get some working experience.
>
> ②【优化句】I believe **taking a part-time job** can **develop practical skills** and **ease the financial burden on our families**. **Besides, it gives us a chance to gain some working experience.**
>
> ③【简短点评】主要中式英语问题：中式搭配（train our ability / reduce family burden）与第二句缺主语（Also can get...）。逻辑上理由并列生硬，句式单调，用词偏直译；develop practical skills、ease the burden 更地道，也更适合口头表达。
>
> 【继续】继续当前话题的深度追问 · 【重新回答】换个角度重新回答同一话题

**输入（用户）：** 继续

**输出（AI，同话题深度追问，开启新一轮）：**

> **Topic:** Some people argue that part-time jobs actually improve students' time management and independence. How would you respond?（有人说兼职反而能锻炼时间管理和独立性，你如何回应？）
>
> **参考句型：**
> - 肯定：Admittedly, part-time jobs can ..., but ...
> - 否定：It is true that ..., yet the cost of ... should not be ignored.

## 不支持范围

- 网页抓取（不联网检索、不引用外部资料）
- PDF 或其他文件处理
- 图形界面 / 浏览器操作
