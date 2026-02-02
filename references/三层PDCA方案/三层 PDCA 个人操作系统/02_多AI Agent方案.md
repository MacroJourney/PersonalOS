# 多 AI Agent 方案：Claude CLI + Cursor + Gemini

以本地文件为中心 + 多 AI Agent 自动化的完整技术架构。

---

## 整体架构设计

```
本地文件系统 (Obsidian Vault)
       ↓
   AI Agent层
   ├─ Claude CLI/API (战略对话)
   ├─ Cursor (写作/编辑)
   ├─ Gemini CLI (数据分析)
   └─ 自定义脚本 (自动化)
       ↓
   三层PDCA系统
   ├─ /Strategy (战略层)
   ├─ /Projects (项目层)
   └─ /Skills (能力层)
```

---

## Obsidian Vault 文件结构

```
MyPersonalOS/
│
├── 📂 0-Inbox/                    # 快速捕获
│   └── daily-captures.md
│
├── 📂 1-Strategy/                 # 战略层
│   ├── mission.md                 # 个人使命
│   ├── 2026-goals.md             # 年度目标
│   ├── quarterly/
│   │   ├── 2026-Q1.md
│   │   └── 2026-Q2.md
│   └── monthly-reviews/
│       ├── 2026-01.md
│       └── template-monthly-review.md
│
├── 📂 2-Projects/                 # 项目层
│   ├── active/
│   │   ├── project-a.md
│   │   └── project-b.md
│   ├── completed/
│   └── templates/
│       └── project-template.md
│
├── 📂 3-Skills/                   # 能力层
│   ├── writing/
│   │   ├── sops/
│   │   ├── prompts/
│   │   └── examples/
│   ├── coding/
│   └── thinking/
│
├── 📂 4-Daily/                    # 日常记录
│   ├── 2026/
│   │   ├── 01-January/
│   │   │   ├── 2026-01-29.md
│   │   │   └── week-05-review.md
│   └── templates/
│       ├── daily-note.md
│       └── weekly-review.md
│
├── 📂 5-AI-Agents/                # AI配置
│   ├── prompts/
│   │   ├── strategy-coach.md
│   │   ├── project-manager.md
│   │   └── skill-analyzer.md
│   ├── scripts/
│   │   ├── daily-sync.sh
│   │   ├── weekly-report.py
│   │   └── auto-analyze.js
│   └── config/
│       ├── claude-config.json
│       └── gemini-config.yaml
│
└── 📂 9-Meta/                     # 系统元数据
    ├── system-log.md              # 系统迭代日志
    └── ai-interaction-history/    # AI对话记录
```

---

## AI Agent 工作流设计

### Agent 1: 战略顾问（Claude CLI）

**配置文件**：`5-AI-Agents/prompts/strategy-coach.md`

```markdown
---
role: Strategic Advisor
context_files:
  - 1-Strategy/mission.md
  - 1-Strategy/2026-goals.md
  - 1-Strategy/quarterly/*.md
trigger: monthly
---

# System Prompt

你是我的战略顾问。每月1号，请：

1. 阅读上个月的所有项目进展（2-Projects/active/）
2. 阅读上个月的所有每日记录（4-Daily/）
3. 对照我的季度目标（1-Strategy/quarterly/）

然后进行苏格拉底式提问：
- 这些行动真的在接近目标吗？
- 有哪些是伪工作？
- 最大的偏离是什么？
- 如果重新选择，应该砍掉什么？

输出格式：
- 写入：1-Strategy/monthly-reviews/YYYY-MM.md
- 包含：问题清单 + 数据支撑 + 调整建议
```

**自动化脚本**：`5-AI-Agents/scripts/strategy-review.sh`

```bash
#!/bin/bash

# 每月1号自动运行
# crontab: 0 9 1 * * /path/to/strategy-review.sh

VAULT_PATH="$HOME/Obsidian/MyPersonalOS"
MONTH=$(date +%Y-%m)

# 1. 聚合数据
cat "$VAULT_PATH/2-Projects/active/"*.md > /tmp/projects-context.txt
cat "$VAULT_PATH/4-Daily/$(date +%Y/%m-*)"/*.md > /tmp/daily-context.txt

# 2. 调用 Claude CLI
claude-cli \
  --prompt-file "$VAULT_PATH/5-AI-Agents/prompts/strategy-coach.md" \
  --context /tmp/projects-context.txt \
  --context /tmp/daily-context.txt \
  --output "$VAULT_PATH/1-Strategy/monthly-reviews/${MONTH}.md"

# 3. 发送通知
osascript -e 'display notification "战略复盘已生成" with title "Personal OS"'
```

---

### Agent 2: 项目经理（Cursor + Claude）

**使用场景**：每周五自动生成周报

**配置**：在Cursor中创建`.cursorrules`

```
# .cursorrules (放在Vault根目录)

Project Context:
- All active projects in: 2-Projects/active/
- Daily logs in: 4-Daily/

When I ask "generate weekly report":
1. Read all files modified this week in above folders
2. Extract task completions, blockers, insights
3. Analyze against project goals
4. Generate report using template: 4-Daily/templates/weekly-review.md
5. Save to: 4-Daily/YYYY/MM-Month/week-XX-review.md

Report Format:
- ✅ Completed (list with project tags)
- 🚧 In Progress (with blockers)
- 💡 Insights (new learnings)
- 📊 Metrics (time spent, completion rate)
- 🎯 Next Week Focus
```

**使用方式**：
```
每周五在Cursor中：
1. 打开Vault文件夹
2. Cmd+K 唤醒AI
3. 输入："generate weekly report"
4. Cursor自动读取所有相关文件，生成周报
5. 一键保存
```

---

### Agent 3: 能力教练（Gemini CLI）

**用途**：每日复盘，提炼可复用知识

**配置文件**：`5-AI-Agents/scripts/daily-digest.py`

```python
#!/usr/bin/env python3
import google.generativeai as genai
from datetime import datetime
import os

# 配置
VAULT_PATH = os.path.expanduser("~/Obsidian/MyPersonalOS")
genai.configure(api_key=os.environ["GEMINI_API_KEY"])

def daily_digest():
    today = datetime.now().strftime("%Y-%m-%d")
    daily_file = f"{VAULT_PATH}/4-Daily/{today}.md"

    # 读取今日笔记
    with open(daily_file, 'r') as f:
        content = f.read()

    # Gemini 分析
    model = genai.GenerativeModel('gemini-2.0-flash-exp')

    prompt = f"""
    分析以下每日记录，提取：

    1. 今天学到的可复用知识（SOP/技巧/工具）
    2. 应该沉淀到能力库的内容
    3. 建议的分类和标签

    每日记录：
    {content}

    输出格式：
    ## 可复用知识
    - [标题] | 分类：XX | 标签：#tag

    ## 建议行动
    - 添加到：3-Skills/XX/XX.md
    """

    response = model.generate_content(prompt)

    # 追加到今日笔记
    with open(daily_file, 'a') as f:
        f.write(f"\n\n---\n## AI 分析\n{response.text}")

    print(f"✅ Daily digest completed: {daily_file}")

if __name__ == "__main__":
    daily_digest()
```

**自动触发**：
```bash
# crontab: 每晚9点运行
0 21 * * * cd ~/Obsidian/MyPersonalOS && python3 5-AI-Agents/scripts/daily-digest.py
```

---

### Agent 4: 智能路由（自定义脚本）

**用途**：根据问题类型自动选择合适的AI

**脚本**：`5-AI-Agents/scripts/ask-agent.sh`

```bash
#!/bin/bash

# 使用方式：./ask-agent.sh "我这周应该做什么？"

QUERY="$1"
VAULT_PATH="$HOME/Obsidian/MyPersonalOS"

# 简单的意图识别
if [[ "$QUERY" == *"战略"* ]] || [[ "$QUERY" == *"方向"* ]]; then
    AGENT="claude"
    CONTEXT="1-Strategy/"
elif [[ "$QUERY" == *"项目"* ]] || [[ "$QUERY" == *"进展"* ]]; then
    AGENT="cursor"
    CONTEXT="2-Projects/"
elif [[ "$QUERY" == *"学到"* ]] || [[ "$QUERY" == *"能力"* ]]; then
    AGENT="gemini"
    CONTEXT="3-Skills/"
else
    AGENT="claude"  # 默认
    CONTEXT=""
fi

# 调用对应Agent
case $AGENT in
    "claude")
        claude-cli --context "$VAULT_PATH/$CONTEXT" "$QUERY"
        ;;
    "gemini")
        gemini-cli --folder "$VAULT_PATH/$CONTEXT" "$QUERY"
        ;;
    "cursor")
        echo "请在Cursor中打开Vault并提问：$QUERY"
        ;;
esac
```

---

## 关键工具配置

### 1. Claude CLI 设置

```bash
# 安装
npm install -g @anthropic-ai/claude-cli

# 配置
claude-cli config set api_key YOUR_API_KEY

# 创建自定义命令
alias strategy="claude-cli --context ~/Obsidian/MyPersonalOS/1-Strategy"
alias review="~/Obsidian/MyPersonalOS/5-AI-Agents/scripts/strategy-review.sh"
```

### 2. Cursor 配置

在Cursor Settings中：
```json
{
  "cursor.includeFolders": [
    "~/Obsidian/MyPersonalOS"
  ],
  "cursor.longContextFiles": [
    "1-Strategy/**/*.md",
    "2-Projects/active/**/*.md"
  ],
  "cursor.composer.autopilot": true
}
```

### 3. Gemini CLI

```bash
# 安装
pip install google-generativeai

# 配置环境变量
echo 'export GEMINI_API_KEY="your-key"' >> ~/.zshrc

# 创建alias
alias daily-sync="python3 ~/Obsidian/MyPersonalOS/5-AI-Agents/scripts/daily-digest.py"
```

### 4. Obsidian 插件推荐

必装插件：
```
1. Templater - 自动化模板
2. Dataview - 数据聚合
3. Shell Commands - 执行脚本
4. QuickAdd - 快速捕获
5. Calendar - 日历视图
```

**Shell Commands配置**：
```yaml
# 在Obsidian中可以直接运行
commands:
  - name: "Generate Weekly Report"
    shell: "cd {{vault_path}} && cursor --command 'generate weekly report'"

  - name: "Daily Digest"
    shell: "python3 {{vault_path}}/5-AI-Agents/scripts/daily-digest.py"

  - name: "Strategy Review"
    shell: "{{vault_path}}/5-AI-Agents/scripts/strategy-review.sh"
```

---

## Obsidian 模板示例

### 每日笔记模板（`4-Daily/templates/daily-note.md`）

```markdown
---
date: {{date:YYYY-MM-DD}}
week: {{date:ww}}
tags: [daily]
---

# {{date:YYYY-MM-DD 星期ddd}}

## 🎯 今日对齐
**战略目标**：[[2026-Q1]]
**本周重点**：

## ✅ 完成任务
- [ ]

## 💡 今日学习
<!-- 能力层：记录可复用的知识 -->

## 🤔 复盘反思
<!-- 晚上9点AI会自动分析这部分 -->

---
## 📊 时间追踪
<!-- 可选：记录时间分配 -->

---
## 🤖 AI分析
<!-- 自动生成，不要手动编辑 -->
```

### 项目模板（`2-Projects/templates/project-template.md`）

```markdown
---
status: active
start: {{date:YYYY-MM-DD}}
goal:
tags: [project]
---

# {{title}}

## 🎯 项目目标
<!-- 对齐到哪个战略目标？ -->
[[1-Strategy/2026-goals#具体目标]]

## 📋 关键任务
- [ ]

## 📈 进展记录
### {{date:YYYY-MM-DD}}


## 🚧 阻塞点


## 💡 经验沉淀
<!-- 完成后提炼到能力层 -->

---
## 🤖 AI项目分析
<!-- 每周五自动更新 -->
```

---

## 完整工作流演示

### 早晨流程（5分钟）

```bash
# 1. 在终端运行
cd ~/Obsidian/MyPersonalOS
./5-AI-Agents/scripts/ask-agent.sh "今天应该优先做什么？"

# AI会：
# - 读取战略目标
# - 分析昨日进展
# - 对比项目deadline
# - 给出优先级建议

# 2. 在Obsidian中
# - 打开今日笔记（自动创建）
# - 填写"今日对齐"部分
# - 开始工作
```

### 工作中（随时）

```bash
# 在Cursor中：
# 1. 打开项目文件
# 2. 遇到问题时，Cmd+K 问AI
# 3. AI会结合你的历史记录和知识库给建议

# 例如：
"根据我之前写过的文章风格，帮我改写这段"
→ Cursor自动读取3-Skills/writing/examples/
→ 生成符合你风格的内容
```

### 晚上复盘（10分钟）

```bash
# 1. 填写今日笔记的"复盘反思"部分（可以语音输入）

# 2. 运行自动分析
daily-sync

# AI会：
# - 分析今日内容
# - 提取可复用知识
# - 自动追加到笔记底部
# - 建议哪些内容应该加入能力库

# 3. 根据AI建议，手动将知识移到3-Skills/
# （或者写脚本自动化）
```

### 周五下午（15分钟）

```bash
# 在Cursor中打开Vault
# Cmd+K，输入：
"generate weekly report"

# Cursor会：
# - 扫描本周所有文件
# - 聚合任务完成情况
# - 识别项目风险
# - 生成结构化周报
# - 自动保存

# 然后你只需：
# - 审阅周报
# - 规划下周
```

### 每月1号（30分钟）

```bash
# 自动触发（或手动运行）
./5-AI-Agents/scripts/strategy-review.sh

# 然后：
# 1. 读AI生成的战略复盘
# 2. 在Cursor中打开战略文件
# 3. 和Claude深度对话，调整方向
# 4. 更新季度目标
```

---

## 进阶自动化

### 1. Git自动备份

```bash
# 5-AI-Agents/scripts/auto-backup.sh

#!/bin/bash
cd ~/Obsidian/MyPersonalOS

git add .
git commit -m "Auto-backup $(date +%Y-%m-%d\ %H:%M)"
git push

# crontab: 每天23:59
59 23 * * * ~/Obsidian/MyPersonalOS/5-AI-Agents/scripts/auto-backup.sh
```

### 2. 智能提醒

```python
# 基于AI分析，主动提醒你
# 例如：某个项目3天没更新 → 发通知

import os
from datetime import datetime, timedelta

def check_stale_projects():
    projects_path = "2-Projects/active"
    threshold = timedelta(days=3)

    for file in os.listdir(projects_path):
        mtime = os.path.getmtime(f"{projects_path}/{file}")
        if datetime.now() - datetime.fromtimestamp(mtime) > threshold:
            # 发送通知
            os.system(f'osascript -e \'display notification "项目 {file} 已3天未更新" with title "Personal OS"\'')
```

### 3. 多Agent协作

```python
# 让三个Agent轮流分析同一个问题

def multi_agent_analysis(question):
    # Claude 战略视角
    strategic_view = claude_cli(question, context="1-Strategy/")

    # Gemini 能力视角
    skill_view = gemini_cli(question, context="3-Skills/")

    # 综合分析
    final_answer = claude_cli(
        f"综合以下两个视角：\n战略：{strategic_view}\n能力：{skill_view}\n给出最终建议"
    )

    return final_answer
```

---

## 效果预期

使用这套系统1个月后：

**战略层**：
- 每月自动生成深度复盘报告
- AI帮你发现方向偏离
- 决策更有依据

**项目层**：
- 每周自动生成周报（节省2小时）
- 阻塞点自动识别
- 进度可视化

**能力层**：
- 每天自动沉淀1-3个知识点
- 1个月积累30+可复用SOP
- 能力资产持续增长

**整体**：
- 95%的记录/分析由AI完成
- 你只需要：思考+决策+执行
- 认知负荷降低50%

---

## 快速启动清单

```bash
# 1. 创建目录结构
mkdir -p ~/Obsidian/MyPersonalOS/{0-Inbox,1-Strategy,2-Projects,3-Skills,4-Daily,5-AI-Agents,9-Meta}

# 2. 安装工具
npm install -g @anthropic-ai/claude-cli
pip install google-generativeai
# 下载Cursor: https://cursor.sh

# 3. 配置API
echo 'export ANTHROPIC_API_KEY="your-key"' >> ~/.zshrc
echo 'export GEMINI_API_KEY="your-key"' >> ~/.zshrc

# 4. 设置定时任务
crontab -e
# 添加上面提到的cron jobs

# 5. 在Obsidian中安装插件并启用Shell Commands
```
